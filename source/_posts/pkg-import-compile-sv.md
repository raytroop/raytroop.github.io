---
title: import package in SystemVerilog compilation
date: 2022-03-24 21:06:54
tags:
categories:
- digital
---

### import and compile order

#### project

**yapp_pkg.sv**

```verilog
package yapp_pkg;
import uvm_pkg::*;
`include "uvm_macros.svh"

 typedef uvm_config_db#(virtual yapp_if) yapp_vif_config;

`include "yapp_packet.sv"
`include "yapp_tx_monitor.sv"
`include "yapp_tx_sequencer.sv"
`include "yapp_tx_seqs.sv"
`include "yapp_tx_driver.sv"
`include "yapp_tx_agent.sv"
`include "yapp_env.sv"

endpackage
```

**yapp_tx_monitor.sv**

```verilog
class yapp_tx_monitor extends uvm_monitor;
  
  // Collected Data handle
  yapp_packet pkt;

  // Count packets collected
  int num_pkt_col;

  // component macro
  `uvm_component_utils_begin(yapp_tx_monitor)
    `uvm_field_int(num_pkt_col, UVM_ALL_ON + UVM_NOCOMPARE)
  `uvm_component_utils_end
/////////////////// virtual interface ////////////////////
  virtual interface yapp_if vif;
/////////////////////////////////////////////////////////
      
  function new (string name, uvm_component parent);
    super.new(name, parent);
  endfunction : new
      ...
     
endclass : yapp_tx_monitor
```

**yapp_tx_driver.sv**

```verilog
class yapp_tx_driver extends uvm_driver #(yapp_packet);

 ////////////////// virtual interface ////////////////////
  virtual interface yapp_if vif;
 /////////////////////////////////////////////////////
      
  int num_sent;

  // component macro
  `uvm_component_utils_begin(yapp_tx_driver)
    `uvm_field_int(num_sent, UVM_ALL_ON + UVM_NOCOMPARE)
  `uvm_component_utils_end

  // Constructor - required syntax for UVM automation and utilities
  function new (string name, uvm_component parent);
    super.new(name, parent);
  endfunction : new

  function void start_of_simulation_phase(uvm_phase phase);
    `uvm_info(get_type_name(), {"start of simulation for ", get_full_name()}, UVM_HIGH)
  endfunction : start_of_simulation_phase
      ...
     
endclass : yapp_tx_driver 
```

**yapp_if.sv**

```verilog
interface yapp_if (input clock, input reset );
timeunit 1ns;
timeprecision 100ps;

import uvm_pkg::*;
`include "uvm_macros.svh"

////////////////// import package //////////////////////
import yapp_pkg::*;
//////////////////////////////////////////////////////    

  // Actual Signals
  logic              in_data_vld;
  logic              in_suspend;
  logic       [7:0]  in_data;

  // signal for transaction recording
  bit monstart, drvstart;

  // local storage for payload
  logic [7:0] payload_mem [0:63];
    ...
    
endinterface : yapp_if
```

> virtual interface is in package;
>
> `yapp_pkg` is imported into interface



> !!! `typedef uvm_config_db#(virtual yapp_if) yapp_vif_config;` is  **forward declaration**
>
> *A forward `typedef` declares an identifier as a type in advance of the full definition of that type*



#### VCS compile

```bash
vcs -full64 -R -sverilog  -ntb_opts uvm-1.2 +UVM_TESTNAME=short_yapp_012_test  -f vcs.f  
```

**vcs.f**

```
-timescale=1ns/1ns

+incdir+../sv

../sv/yapp_if.sv
../sv/yapp_pkg.sv
./clkgen.sv
./hw_top.sv
./tb_top.sv
```

*output ERROR*

```
Error-[SV-LCM-PND] Package not defined
../sv/yapp_if.sv, 18
yapp_if, "yapp_pkg::"
  Package scope resolution failed. Token 'yapp_pkg' is not a package. 
  Originating module 'yapp_if'.
  Move package definition before the use of the package.
```

#### xrun compile

```
xrun -f xrun.f
```

**xrun.f**

```
-64

-uvmhome  CDNS-1.2

// incdir for include files
-incdir ../sv

+UVM_TESTNAME=short_yapp_012_test

-timescale 1ns/1ns

// compile files
../sv/yapp_if.sv
../sv/yapp_pkg.sv
./clkgen.sv
./hw_top.sv
./tb_top.sv
```

*output Error*

```
file: ../sv/yapp_if.sv
import yapp_pkg::*;
              |
xmvlog: *E,NOPBIND (../sv/yapp_if.sv,18|14): Package yapp_pkg could not be bound.
        interface worklib.yapp_if:sv
                errors: 1, warnings: 0
```



#### solution

place `../sv/yapp_pkg.sv` before `../sv/yapp_if.sv`.

> In this particular example, `yapp_pkg` is NOT needed in interface. just delete `import yapp_pkg::*` is enough in `../sv/yapp_if.sv`



### plain example

The order of compilation unit  DON'T matter

#### project

**hw_top.sv**

```verilog
module hw_top;

  // Clock and reset signals
  logic [31:0]  clock_period;
  logic         run_clock;
  logic         clock;
  logic         reset;

  // YAPP Interface to the DUT
  yapp_if in0(clock, reset);

  // CLKGEN module generates clock
  clkgen clkgen (
    .clock(clock),
    .run_clock(1'b1),
    .clock_period(32'd10)
  );

  yapp_router dut(
    .reset(reset),
    .clock(clock),
    .error(),
    // YAPP interface signals connection
    .in_data(in0.in_data),
    .in_data_vld(in0.in_data_vld),
    .in_suspend(in0.in_suspend),
    // Output Channels
    //Channel 0   
    .data_0(),
    .data_vld_0(),
    .suspend_0(1'b0),
    //Channel 1   
    .data_1(),
    .data_vld_1(),
    .suspend_1(1'b0),
    //Channel 2   
    .data_2(),  
    .data_vld_2(),
    .suspend_2(1'b0),
    // Host Interface Signals
    .haddr(),
    .hdata(),
    .hen(),
    .hwr_rd());
    
    ...
        
endmodule
```

**yapp_router.sv**

```verilog
module yapp_router (input clock,                              
                    input reset,                            
                    output error,

                    // Input channel
                    input [7:0] in_data,                           
                    input in_data_vld,                     
                    output in_suspend,
                    // Output Channels
                    output [7:0] data_0,  //Channel 0
                    output reg data_vld_0, 
                    input suspend_0, 
                    output [7:0] data_1,  //Channel 1
                    output reg data_vld_1, 
                    input suspend_1, 
                    output [7:0] data_2,  //Channel 2
                    output reg data_vld_2,
                    input suspend_2,
     
                    // Host Interface Signals
                    input [15:0] haddr,
                    inout [7:0] hdata,
                    input hen,
                    input hwr_rd);                            
...
endmodule    
```

#### compile

place **hw_top.sv** *before or after* **yapp_router.sv**  doesn't matter, the compiler (xrun, vcs) can compile them successfully.



### Conclusion

Always place package before DUT is preferred choice during compiling.



### refernce

[class forward declaration](https://verificationacademy.com/forums/systemverilog/class-forward-declaration#answer-41383)

