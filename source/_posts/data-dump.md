---
title: simulation data dumping
date: 2022-06-04 16:30:47
tags:
categories:
- digital
---

## FSDB

### `$fsdbDumpfile`

It specifies the FSDB file name created by the Novas object files for FSDB dumping. If it is not specified, then the default FSDB file name is "novas.fsdb".

> This command is valid only **before** executing `$fsdbDumpvars` and is ignored if specified after `$fsdbDumpvars`



### `$fsdbSuppress`

The `fsdbSuppress `utility is used to skip dumping of few instances, scopes, modules and signals. The `fsdbSuppress `utility is a system task like other fsdb tasks.

> For `$fsdbSuppress()` to be effective, it needs to be specified/called **before** `$fsdbDumpvars`



### `$fsdbAutoSwitchDumpfile`

Automatically switch to a new dump file when the working FSDB file reaches the specified size or the specified wall time period.

> After the dumping is finished, a **virtual FSDB file (\*.vf)** is automatically created and list all of the generated FSDB files with the correct sequence. Only the **virtual FSDB file**, rather than all of the FSDB files, needs to be loaded to view the simulation results

When specified in the design to switch based on **file size**:

```
$fsdbAutoSwitchDumpfile(File_Size | File_Size_var, "FSDB_Name" |FSDB_Name_var, Number_of_Files | Number_of_Files_var[ ,"log_filename" | ,log_filename_var ], ["+no_overwrite"]);
```

When specified in the design to switch based on **time period**

```
$fsdbAutoSwitchDumpfile(File_Size | File_Size_var, "FSDB_Name" |FSDB_Name_var, Number_of_Files | Number_of_Files_var[ ,"log_filename" | ,log_filename_var ], ["+no_overwrite"], “+by_period”);
```

> `“+by_period”`



### `$fsdbDumpvars`

This command dumps the change in signal value to the FSDB file.

```
$fsdbDumpvars([ depth, | "level=",depth_var, ],[instance | "instance=",instance_var])
```

> For VCS users, to include memory, MDA, packed array and structure information in the generated FSDB file, the `-debug_access` option must be included when VCS is invoked to **compile the design**

- `depth`

  Specify how many sub-scope levels under the given scope you want to dump.

  - Specify this argument as **1** to dump the signals under the given scope
  - Specify this argument as **0** to dump all signals under the given scope and its descendant scopes.

  0: all signals in all scopes.

  1: all signals in current scope.

  2: all signals in the current scope and all scopes one level below.

  n: all signals in the current scope and all scopes n-1 levels below.

  |                             | tb.clk  | tb.u_div2.div2 | tb.u_div2.u_div2neg.div2neg |
  | --------------------------- | ------- | -------------- | --------------------------- |
  | $fsdbDumpvars(0)            | &check; | &check;        | &check;                     |
  | $fsdbDumpvars(1)            | &check; | &cross;        | &cross;                     |
  | $fsdbDumpvars(2)            | &check; | &check;        | &cross;                     |
  | $fsdbDumpvars(1, tb.u_div2) | &cross; | &check;        | &cross;                     |
  | $fsdbDumpvars(0, tb.u_div2) | &cross; | &check;        | &check;                     |

  ```verilog
  module tb;
  	reg clk;

  	divider2 u_div2(clk);

  	initial begin
  		clk = 1'b0;
  		forever #5 clk = ~clk;
  	end

  	initial begin
  		#100;
  		$finish();
  	end

  	initial begin
  		 #10;
  		 $fsdbDumpfile("tb.fsdb");
  		 //$fsdbDumpvars(0);				// same with $fsdbDumpvars(0, tb)
  		 //$fsdbDumpvars(1);				// same with $fsdbDumpvars(1, tb)
  		 //$fsdbDumpvars(2);				// same with $fsdbDumpvars(2, tb)
  		 //$fsdbDumpvars(1, tb.u_div2);
  		 $fsdbDumpvars(0, tb.u_div2);
  		 #80 $finish();
  	end

  endmodule


  module divider2 (
  	input clk
  );
  	reg div2;

  	divider2neg u_div2neg(div2);

  	always@(posedge clk) begin
  		div2 = ~div2;
  	end

  	initial begin
  		div2 = 1'b0;
  	end

  endmodule

  module divider2neg (
  	input clk
  );
  	reg div2neg;

  	always@(negedge clk) begin
  		div2neg = ~div2neg;
  	end

  	initial begin
  		div2neg= 1'b0;
  	end

  endmodule
  ```
  *compile*
  ```
  vcs -full64 -kdb -debug_access+all tb.v
  ```

  *simulate*

  ```
  ./simv
  ```

  *load fsdb*

  ```
  verdi -ssf tb.fsdb
  ```

  ![image-20220604192421888](data-dump/image-20220604192421888.png)

### `$fsdbDumpon, $fsdbDumpoff`

```verilog
$fsdbDumpon(["+fsdbfile+filename"])

$fsdbDumpoff(["+fsdbfile+filename"])
```

These FSDB dumping commands turn dumping on and off. `fsdbDumpon/fsdbDumpoff` has the highest priority and overrides all other FSDB dumping commands.

`fsdbDumpon/fsdbDumpoff` is not restricted to only `fsdbDumpvars`. If there is more than one FSDB file open for dumping at one simulation run, `fsdbDumpon/fsdbDumpoff` may only affect a specific FSDB file by specifying the specific file name.

- `+fsdbfile+filename`: Specify the FSDB file name. If not specified, the default FSDB file name is "novas.fsdb"

### `$fsdbDumpFinish`

This command closes all FSDB files in the current simulation and stops dumping of signals. Although all FSDB files are *closed automatically at the end of simulation*, this dumping command can be invoked to *explicitly* close the FSDB files during the simulation

## VCD

### `$dumpfile`

The declaration onf `$dumpfile` must come before the `$dumpvars` or any other system tasks that specifies dump.

```verilog
$dumpfile("test.vcd");
```

> argument **is necessary**, there is no default value

### `$dumpvars`

The `$dumpvars` is used to specify which variables are to be dumped ( in the file mentioned by `$dumpfile`). The simplest way to use it is without any argument.

```verilog
$dumpvars(<levels> <, <module_or_variable>>* );
```

### `$dumplimit`

It is possible that you inadvertantly generate huge file in Gigabytes ( for examples while dumping a Gigahertz clock for one second). To reduce such occurrences, we may use `$dumplimit`. It usage is

```verilog
$dumplimit(<filesize>);
```

### `$dumpoff and $dumpon`

During the simulation if you are bothered about about only during a certain interval then you can use `$dumpoff` and `$dumpon`. The following example shows its usage. It will dump the changes for first 100 units of time and then between 10200 and 10400 units of time.

```verilog
initial
    $monitor($time, " reset=%b,clk_out=%b",reset,clk_out);
    initial begin
            $dumpfile("clkdiv2n_tb.vcd");
            $dumpvars(0,clkdiv2n_tb);
            #100;
            $dumpoff;
            #10200;
            $dumpon;
            #10400;
            $dumpoff;
    end
```

### demo

stimulus.v

```verilog
`timescale 1ns / 1ps
module stimulus;
	// Inputs
	reg x;
	reg y;
	// Outputs
	wire z;
	// Instantiate the Unit Under Test (UUT)
	comparator uut (
		.x(x),
		.y(y),
		.z(z)
	);

	initial begin
		$dumpfile("test.vcd");
		$dumpvars(0);
		// Initialize Inputs
		x = 0;
		y = 0;

		#20 x = 1;
		#20 y = 1;
		#20 y = 0;
		#20 x = 1;
		#40 ;

	end

	initial begin
		$monitor("t=%3d x=%d,y=%d,z=%d \n",$time,x,y,z, );
	end

endmodule
```



comparator.v

```verilog
module comparator(
	input x,
	input y,
	output z
);

	assign z = (~x & ~y) |(x & y);

endmodule
```

```
$ xrun stimulus.v comparator.v -access +rwc
$ simvision test.vcd
```



## reference

$dumpvars and $dumpfile Verilog, http://www.referencedesigner.com/tutorials/verilog/verilog_62.php
