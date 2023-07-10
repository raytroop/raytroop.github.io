---
title: questasim sim flow
date: 2022-02-02 16:41:21
tags:
categories:
- digital
---

```
vlib work
vlog -f filelist tb.sv
# "-c": command line mode
vsim -voptargs=+acc -c -do "run 100ns; exit" work.topmodule
```

> `-voptargs=+acc`:  Add the option `-voptargs=+acc` to the *vsim* command, This enables full visibility into every aspect of the design. 


```verilog
module topmodule;
    ...
endmodule
```

**uvm**:

```
> vlog test_pkg.sv tb_top.sv -L $QUESTA_HOME/uvm-1.2
> vsim -c -do "run -all;exit" +UVM_TESTNAME=my_test work.tb_top  -L $QUESTA_HOME/uvm-1.2
```



**reference**:

A Short Intro to ModelSim Verilog Simulator URL: [https://users.ece.cmu.edu/~jhoe/doku/doku.php?id=a_short_intro_to_modelsim_verilog_simulator](https://users.ece.cmu.edu/~jhoe/doku/doku.php?id=a_short_intro_to_modelsim_verilog_simulator)
