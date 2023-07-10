---
title: How does UVM's run_test search testcase ?
date: 2022-06-08 00:53:36
tags:
- uvm
- systemverilog
categories:
- digital
---

It depends on the simulator:

- QuestaSim, Xcelium: You have to `import` pkg or ``include`  file in top testbench
- VCS:  VCS automatically search testcase in other Compilation Units

```verilog
// test_pkg.sv
package sim_pkg;
	import uvm_pkg::*;
	`include "uvm_macros.svh"

	class my_test extends uvm_test;
		`uvm_component_utils(my_test)
		
		function new(string name, uvm_component parent);
			super.new(name, parent);
		endfunction : new

		task run_phase(uvm_phase phase);
			`uvm_info(get_type_name(), "this is run_phase of my_test", UVM_LOW)
		endtask : run_phase
	endclass : my_test

	class its_test extends uvm_test;
		`uvm_component_utils(its_test)
		
		function new(string name, uvm_component parent);
			super.new(name, parent);
		endfunction : new

		task run_phase(uvm_phase phase);
			`uvm_info(get_type_name(), "this is run_phase of its_test", UVM_LOW)
		endtask : run_phase
	endclass : its_test

endpackage : sim_pkg
```

```verilog
// tb_top.sv
module tb_top;
	import uvm_pkg::*;
	//import sim_pkg::*;

	initial begin
		run_test();
	end
endmodule
```

| simulator | cmd                                                          | result  |
| --------- | ------------------------------------------------------------ | ------- |
| VCS       | `vcs -sverilog -ntb_opts uvm-1.2 test_pkg.sv tb_top.sv`<br />`./simv +UVM_TESTNAME=my_test` | &check; |
| Xcelium   | `xrun -64 -uvmhome CDNS-1.2 test_pkg.sv tb_top.sv +UVM_TESTNAME=my_test` | &cross; |
| QuestaSim | `vlog test_pkg.sv tb_top.sv -L $QUESTA_HOME/uvm-1.2`<br />`vsim -c -do "run -all;exit" +UVM_TESTNAME=my_test work.tb_top -L $QUESTA_HOME/uvm-1.2` | &cross; |

*Xcelium log:*

> `UVM_WARNING @ 0: reporter [BDTYP] Cannot create a component of type 'my_test' because it is not registered with the factory.
> UVM_FATAL @ 0: reporter [INVTST] Requested test from command line +UVM_TESTNAME=my_test not found.
> UVM_INFO /home/EDA/Cadence/XCELIUM2109/tools/methodology/UVM/CDNS-1.2/sv/src/base/uvm_report_catcher.svh(705) @ 0: reporter [UVM/REPORT/CATCHER]` 

*QuestaSim log:*

> `# UVM_INFO verilog_src/questa_uvm_pkg-1.2/src/questa_uvm_pkg.sv(277) @ 0: reporter [Questa UVM] QUESTA_UVM-1.2.3`
> `# UVM_INFO verilog_src/questa_uvm_pkg-1.2/src/questa_uvm_pkg.sv(278) @ 0: reporter [Questa UVM]  questa_uvm::init(+struct)`
> `# UVM_WARNING @ 0: reporter [BDTYP] Cannot create a component of type 'my_test' because it is not registered with the factory.`
> `# UVM_FATAL @ 0: reporter [INVTST] Requested test from command line +UVM_TESTNAME=my_test not found.`
> `# UVM_INFO verilog_src/uvm-1.2/src/base/uvm_report_server.svh(847) @ 0: reporter [UVM/REPORT/SERVER]`

**solution:**

uncomment `//import sim_pkg::*;` in *tb_top.sv*



