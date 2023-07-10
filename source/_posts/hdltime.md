---
title: time format in Verilog
date: 2023-06-05 22:33:51
tags:
categories:
- digital
---



## realtime vs time

- `$realtime` round the current time to `timeprecision`

- `$time` round the current time to integer

- `%t` will scale the rounded value to represent `timeprecision`,

  i.e.  $[\$\text{realtime}, \$\text{time}]\cdot \$\text{timeunit} / \$\text{timeprecision}$



[https://verificationacademy.com/forums/systemverilog/time-vs-realtime#answer-94062](https://verificationacademy.com/forums/systemverilog/time-vs-realtime#answer-94062)
[https://verificationacademy.com/forums/systemverilog/time-vs-realtime#answer-94096](https://verificationacademy.com/forums/systemverilog/time-vs-realtime#answer-94096)



```verilog
module tb;
  timeunit 10ns;
  timeprecision 1ps;

  initial begin
    $display("$realtime = %g", $realtime);
    $display("$time = %g", $time);
    // $realtime round to timeprecision
    // $time round to integer
    #1.10016
    $display("$realtime = %g", $realtime);
    $display("$time = %g", $time);

    // %t format will scale the rounded value to represent timeprecision
    // 1.1002*10e-9/1e-12 = 11002
    $display("$realtime %%t = %t", $realtime);
    $display("$time %%t = %t", $time);
  end
endmodule
```
output
```
  $realtime = 0
  $time = 0
  $realtime = 1.1002
  $time = 1
  $realtime %t =                11002
  $time %t =                10000
```

## timeunit, timeprecision

The time unit and time precision can be specified in the following two ways:
- Using the compiler directive `` `timescale``
- Using the keywords `timeunit` and `timeprecision`
```verilog
module D (...);
  timeunit 100ps;
  timeprecision 10fs;
  ...
endmodule

module E (...);
  timeunit 100ps / 10fs; // timeunit with optional second argument
  ...
endmodule
```

The minimum of `timeprecision` determine `%t` output, the nearest `timeunit` and `timeprecision` determine
the round of `$realtime` and `$time`. Of course, the simulator follow the time tick shown by `$realtime`.

```verilog
`timescale 1ns/1ns

// Due to minimum of timeprecision is 10ps
module rawplant;
  timeunit 1ns;
  timeprecision 100ps;

  task print;
    /*
    1ns: 1
    100ps:  6
    10ps: 6
    1ps: 6
    */
    #1.666
    $display("raw: $realtime = %g", $realtime);     // 1.7
    $display("raw: $time = %g", $time);             // 2
    $display("raw: $realtime %%t = %t", $realtime); // 1.7*1ns/10ps=170
    $display("raw: $time %%t = %t", $time);         // 2*1ns/10ps = 200
  endtask

endmodule

module fineplant;
  timeunit 100ps;
  timeprecision 10ps;

  task print;
    /*
    100ps: 2
    10ps: 6
    1ps: 6
    */
    #2.66
    $display("fine: $realtime = %g", $realtime);     // 2.7
    $display("fine: $time = %g", $time);             // 3
    $display("fine: $realtime %%t = %t", $realtime); // 2.7*100ps/10ps = 27
    $display("fine: $time %%t = %t", $time);         // 3*100ps/10ps = 30
  endtask

endmodule

module tb;
  rawplant rawblock();
  fineplant fineblock();

  initial begin
  fork
    rawblock.print();
    fineblock.print();
  join
  end
endmodule
```
output
```
fine: $realtime = 2.7
fine: $time = 3
fine: $realtime %t =                   27
fine: $time %t =                   30
raw: $realtime = 1.7
raw: $time = 2
raw: $realtime %t =                  170
raw: $time %t =                  200
```



## questasim cmd

```bash
vlib work
vlog tb.v
vsim -c -do "run -all;exit" work.tb
```

