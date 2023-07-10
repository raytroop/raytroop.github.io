---
title: Precedence Rule of UVM uvm_config_db::set 
date: 2022-03-23 18:48:41
tags:
categories:
- digital
---

[https://vlsiverify.com/uvm/uvm_config_db-in-uvm#Precedence_Rule](https://vlsiverify.com/uvm/uvm_config_db-in-uvm#Precedence_Rule)

#### Two Precedence rules

There are two precedence rules applicable to `uvm_config_db`. In the `build_phase`,

1. A `set()` call in **a context higher up the component hierarchy** takes precedence over a `set()` call that occurs lower in the hierarchical path.
2. On having **same context field**, **the last** `set()` call takes precedence over the earlier `set()` call.

#### Example for rule - 1

```verilog
`include "uvm_macros.svh"
import uvm_pkg::*;

class component_A extends uvm_component;
  int id;
  `uvm_component_utils(component_A)
  
  function new(string name = "component_A", uvm_component parent = null);
    super.new(name, parent);
    id = 1;
  endfunction
  
  function display();
    `uvm_info(get_type_name(), $sformatf("inside component_A: id = %0d", id), UVM_LOW);
  endfunction
endclass

class component_B extends component_A;
  int receive_value;
  int id;
  
  `uvm_component_utils(component_B)
  
  function new(string name = "component_B", uvm_component parent = null);
    super.new(name, parent);
    id = 2;
  endfunction
  
  function void build_phase(uvm_phase phase);
    super.build_phase(phase);
    if(!uvm_config_db #(int)::get(this, "*", "value", receive_value))
      `uvm_fatal(get_type_name(), "get failed for resource in this scope");    
  endfunction
  
  function display();
    `uvm_info(get_type_name(), $sformatf("inside component_B: id = %0d, receive_value = %0d", id, receive_value), UVM_LOW);
  endfunction
endclass

class env extends uvm_env;
  `uvm_component_utils(env)
  component_A comp_A;
  component_B comp_B;
  
  function new(string name = "env", uvm_component parent = null);
    super.new(name, parent);
  endfunction
  
  function void build_phase(uvm_phase phase);
    super.build_phase(phase);
    comp_A = component_A ::type_id::create("comp_A", this);
    comp_B = component_B ::type_id::create("comp_B", this);
    
    uvm_config_db #(int)::set(this, "*", "value", 200);
  endfunction
  
  task run_phase(uvm_phase phase);
    super.run_phase(phase);
    void'(comp_A.display());
    void'(comp_B.display());
  endtask
endclass

class my_test extends uvm_test;
  bit control;
  `uvm_component_utils(my_test)
  env env_o;
  
  function new(string name = "my_test", uvm_component parent = null);
    super.new(name, parent);
  endfunction
  
  function void build_phase(uvm_phase phase);
    super.build_phase(phase);
    ////////////////////////////////////////////////////
      env_o = env::type_id::create("env_o", this);				// line 99
    
      uvm_config_db #(int)::set(null, "*", "value", 100);		// line 101
	////////////////////////////////////////////////////
  endfunction
   
  function void end_of_elaboration_phase(uvm_phase phase);
    super.end_of_elaboration_phase(phase);
    uvm_top.print_topology();
  endfunction
endclass

module tb_top;
  initial begin
    run_test("my_test");
  end
endmodule
```

```
UVM_INFO /xcelium20.09/tools//methodology/UVM/CDNS-1.2/sv/src/base/uvm_root.svh(605) @ 0: reporter [UVMTOP] UVM testbench topology:
--------------------------------------
Name          Type         Size  Value
--------------------------------------
uvm_test_top  my_test      -     @1810
  env_o       env          -     @1877
    comp_A    component_A  -     @1922
    comp_B    component_B  -     @1953
--------------------------------------

UVM_INFO testbench.sv(14) @ 0: uvm_test_top.env_o.comp_A [component_A] inside component_A: id = 1
UVM_INFO testbench.sv(36) @ 0: uvm_test_top.env_o.comp_B [component_B] inside component_B: id = 2, receive_value = 100
```

> As you can see , the `uvm_config_db::set` is after the factory `type_id::create`,  but **receive_value** is still **100**, I believe that `build_phase` of upper hierarchy finish first before create lower components.
>
> But the recommendation in literature and many web is place `uvm_config_db::set` before `create`



#### Simple Example for rule - 2

```verilog
    uvm_config_db #(int)::set(null, "*", "value", 100);
    uvm_config_db #(int)::set(null, "*", "value", 200);
```

[[complete code]](https://www.edaplayground.com/x/jgvh)

```
UVM_INFO /xcelium20.09/tools//methodology/UVM/CDNS-1.2/sv/src/base/uvm_root.svh(605) @ 0: reporter [UVMTOP] UVM testbench topology:
--------------------------------------
Name          Type         Size  Value
--------------------------------------
uvm_test_top  my_test      -     @1810
  env_o       env          -     @1877
    comp_A    component_A  -     @1924
    comp_B    component_B  -     @1955
--------------------------------------

UVM_INFO testbench.sv(14) @ 0: uvm_test_top.env_o.comp_A [component_A] inside component_A: id = 1
UVM_INFO testbench.sv(36) @ 0: uvm_test_top.env_o.comp_B [component_B] inside component_B: id = 2, receive_value = 200
```

### Another Example for rule - 2

The `set` in  `super.build_phase` and `set` in current `build_phase` are at the **same hierarchy**, so **rule-2** apply

base_test

```verilog
class base_test extends uvm_test;

  // component macro
  `uvm_component_utils(base_test)

  router_tb tb;

  // component constructor
  function new(string name, uvm_component parent);
    super.new(name, parent);
  endfunction : new

  // UVM build_phase()
  function void build_phase(uvm_phase phase);
    super.build_phase(phase);
    uvm_config_int::set(this, "*", "recording_detail", 1);
    uvm_config_wrapper::set(this, "tb.yapp.tx_agent.sequencer.run_phase", 
                                                      "default_sequence",
                                                      yapp_5_packets::get_type());
    tb = router_tb::type_id::create("tb", this);
  endfunction : build_phase

endclass : base_test
```

#### test2 - One

> `yapp_incr_payload_seq` override the `yapp_5_packets`  in `super.build_phase(phase)`, **yapp_incr_payload_seq** is used.

```verilog
class test2 extends base_test;

  // component macro
  `uvm_component_utils(test2)

  // component constructor
  function new(string name, uvm_component parent);
    super.new(name, parent);
  endfunction : new

  function void build_phase(uvm_phase phase);
    yapp_packet::type_id::set_type_override(short_yapp_packet::get_type());
    super.build_phase(phase);
    uvm_config_wrapper::set(this, "tb.yapp.tx_agent.sequencer.run_phase", 
                                                      "default_sequence",
                                                      yapp_incr_payload_seq::get_type());
  endfunction : build_phase

endclass : test2
```

```
---------------------------------------------------------------------------------------------------------------------                   
Name                           Type               Size  Value
---------------------------------------------------------------------------------------------------------------------                   
req                            short_yapp_packet  -     @3045
  length                       integral           6     'h5
  addr                         integral           2     'h1
  payload                      da(integral)       5     -
    [0]                        integral           8     'h0
    [1]                        integral           8     'h1
    [2]                        integral           8     'h2
    [3]                        integral           8     'h3
    [4]                        integral           8     'h4
  parity                       integral           8     'h11
  parity_type                  parity_t           1     GOOD_PARITY
  packet_delay                 integral           32    'd19
  begin_time                   time               64    0
  depth                        int                32    'd2
  parent sequence (name)       string             21    yapp_incr_payload_seq                                                           
  parent sequence (full name)  string             61    uvm_test_top.tb.yapp.tx_agent.sequencer.yapp_incr_payload_seq                   
  sequencer                    string             39    uvm_test_top.tb.yapp.tx_agent.sequencer                                         
---------------------------------------------------------------------------------------------------------------------
```

#### test2 - Two

> the `yapp_5_packets`  in `super.build_phase(phase)`  overide `yapp_incr_payload_seq`  in test2's `build_phase`, **yapp_5_packets** is used

```verilog
class test2 extends base_test;

  // component macro
  `uvm_component_utils(test2)

  // component constructor
  function new(string name, uvm_component parent);
    super.new(name, parent);
  endfunction : new

  function void build_phase(uvm_phase phase);
    yapp_packet::type_id::set_type_override(short_yapp_packet::get_type());
    uvm_config_wrapper::set(this, "tb.yapp.tx_agent.sequencer.run_phase", 
                                                      "default_sequence",
                                                      yapp_incr_payload_seq::get_type());
    super.build_phase(phase);
  endfunction : build_phase

endclass : test2
```



```
--------------------------------------------------------------------------------------------------------------                          
Name                           Type               Size  Value
--------------------------------------------------------------------------------------------------------------                          
req                            short_yapp_packet  -     @3176
  length                       integral           6     'h6
  addr                         integral           2     'h1
  payload                      da(integral)       6     -
    [0]                        integral           8     'h4f
    [1]                        integral           8     'hbe
    [2]                        integral           8     'hb
    [3]                        integral           8     'h1d
    [4]                        integral           8     'h72
    [5]                        integral           8     'hc5
  parity                       integral           8     'h49
  parity_type                  parity_t           1     GOOD_PARITY
  packet_delay                 integral           32    'd0
  begin_time                   time               64    40
  depth                        int                32    'd2
  parent sequence (name)       string             14    yapp_5_packets                                                                  
  parent sequence (full name)  string             54    uvm_test_top.tb.yapp.tx_agent.sequencer.yapp_5_packets                          
  sequencer                    string             39    uvm_test_top.tb.yapp.tx_agent.sequencer                                         
-------------------------------------------------------------------------------------------------------------- 
```



