---
title: plusargs in verilog
date: 2022-06-04 12:29:28
tags:
- plusargs
- runtime
categories:
- digital
---

**plusargs** are command-line switches supported by the simulator. As per SystemVerilog LRM arguments beginning with the `+` character will be available using the `$test$plusargs` and `$value$plusargs` **PLI APIs**.

```verilog
$test$plusargs (user_string)

$value$plusargs (user_string, variable)
```

#### Example

```verilog
// tb.v
module tb;
        int a;
        initial begin
                if($test$plusargs("RUNSIM")) begin
                        $display("There is RUNSIM plusargs");
                end else begin
                        $display("There is NO $test$plusargs");
                end
                if($value$plusargs("SEED=%d",a)) begin
                        $display("SEED=%d",a);
                end else begin
                        $display("There is NO $value$plusargs");
                end
        end
endmodule
```

- compile

  ```
  $ vlib work
  $ vlog -sv tb.v
  ```

- simulate (*QuestaSim*)

  - with**out** plusargs

    ```
    $ vsim work.tb -c -do "run; exit"
    ```

    ```
    # //
    # Loading sv_std.std
    # Loading work.tb(fast)
    # run
    # There is NO $test$plusargs
    # There is NO $value$plusargs
    #  exit
    # End time: 13:04:23 on Jun 04,2022, Elapsed time: 0:00:01
    # Errors: 0, Warnings: 0
    ```

  - with plusargs

    ```
    $ vsim work.tb -c -do "run; exit" +SEED=31 +RUNSIM
    ```

    > `+SEED=31 +RUNSIM`

    ```
    # //
    # Loading sv_std.std
    # Loading work.tb(fast)
    # run
    # There is RUNSIM plusargs
    # SEED=         31
    #  exit
    # End time: 13:04:55 on Jun 04,2022, Elapsed time: 0:00:01
    # Errors: 0, Warnings: 0
    ```



#### reference

systemverilog-command-line-input URL: [https://www.chipverify.com/systemverilog/systemverilog-command-line-input](https://www.chipverify.com/systemverilog/systemverilog-command-line-input)

PLUSARGS IN SYSTEMVERILOG URL:[https://www.theartofverification.com/plusargs-in-systemverilog/](https://www.theartofverification.com/plusargs-in-systemverilog/)
