---
title: Mixing Signed and Unsigned in Verilog
date: 2022-05-07 16:23:26
tags:
- verilog
- signed
categories:
- digital
---

Sign Extension

1) Calculate the necessary minimum width of the sum so that it contains all input possibilities
2) Extend the inputs' sign bits to the width of the answer
3) Add as usual
4) Ignore bits that ripple to the left of the answer's MSB

1. **signed**

|               | inA (signed) | inB (signed) | outSum<br />(signed/unsigned) |
| ------------- | ------------ | ------------ | ----------------------------- |
|               | 0101 (5)     | 1111 (-1)    |                               |
| *extend sign* | **0**0101    | **1**1111    |                               |
| *sum result*  |              |              | 00100                         |
```verilog
module tb;
	reg signed [3:0] inA;
	reg signed [3:0] inB;
    reg signed [4:0] outSumSg;	// signed result
    reg [4:0] outSumUs;			// unsigned result

	initial begin
		inA = 4'b0101;
		inB = 4'b1111;
		outSumUs = inA + inB;
		outSumSg = inA + inB;

		$display("signed out(%%d): %0d", outSumSg);
		$display("signed out(%%b): %b", outSumSg);

		$display("unsigned out(%%d): %0d", outSumUs);
		$display("unsigned out(%%b): %b", outSumUs);
	end
endmodule
```
2. **mixed**

|               | inA (signed) | inB (unsigned) | outSum<br />(signed/unsigned) |
| ------------- | ------------ | -------------- | ----------------------------- |
|               | 0101 (5)     | 1111 (15)      |                               |
| *extend sign* | **0**0101    | **0**1111      |                               |
| *sum result*  |              |                | 10100                         |
```verilog
reg signed [3:0] inA;
reg [3:0] inB;
```
|               | inA (unsigned) | inB (signed) | outSum<br />(signed/unsigned) |
| ------------- | -------------- | ------------ | ----------------------------- |
|               | 0101 (5)       | 1111 (-1)    |                               |
| *extend sign* | **0**0101      | **0**1111    |                               |
| *sum result*  |                |              | 10100                         |

```verilog
module tb;
	reg [3:0] inA;
	reg signed [3:0] inB;
	reg signed [4:0] outSumSg;
	reg [4:0] outSumUs;

	initial begin
		inA = 4'b0101;
		inB = 4'b1111;
		outSumUs = inA + inB;
		outSumSg = inA + inB;

		$display("signed out(%%d): %0d", outSumSg);
		$display("signed out(%%b): %b", outSumSg);

		$display("unsigned out(%%d): %0d", outSumUs);
		$display("unsigned out(%%b): %b", outSumUs);
	end
endmodule
```

**xcelium**

```
xcelium> run
signed out(%d): -12
signed out(%b): 10100
unsigned out(%d): 20
unsigned out(%b): 10100
xmsim: *W,RNQUIE: Simulation is complete.
xcelium> exit
```

**vcs**

```
Compiler version S-2021.09-SP2-1_Full64; Runtime version S-2021.09-SP2-1_Full64;  May  7 17:24 2022
signed out(%d): -12
signed out(%b): 10100
unsigned out(%d): 20
unsigned out(%b): 10100
           V C S   S i m u l a t i o n   R e p o r t
```

### observation

> When *signed* and *unsigned* is **mixed**, the result is by default **unsigned**. 
>
> Prepend to operands with **0**s instead of extending sign, even though the operands is signed
>
> LHS **DONT** affect how the simulator operate on the operands but what the results represent, signed or unsigned



Therefore, although `outSumUs` is declared as signed, its result is unsigned

#### subtraction example

In logic arithmetic, addition and subtraction are commonly used for digital design. Subtraction is similar to addition except that the subtracted number is 2's complement. By using 2's complement for the subtracted number, both addition and subtraction can be unified to using addition only.

##### operands are signed

|               | inA (signed) | inB (signed) | outSub<br />(signed/unsigned) |
| ------------- | ------------ | ------------ | ----------------------------- |
|               | 1111 (-1)    | 0010 (2)     |                               |
| *extend sign* | **1**1111    | **0**0010    |                               |
| *sub result*  |              |              | 11101                         |

```verilog
module tb;
	reg signed [3:0] inA;
	reg signed [3:0] inB;
	reg signed [4:0] outSubSg;
	reg [4:0] outSubUs;

	initial begin
		inA = 4'b1111;
		inB = 4'b0010;
		outSubUs = inA - inB;
		outSubSg = inA - inB;

		$display("signed out(%%d): %0d", outSubSg);
		$display("signed out(%%b): %b", outSubSg);

		$display("unsigned out(%%d): %0d", outSubUs);
		$display("unsigned out(%%b): %b", outSubUs);
	end
endmodule
```

```
Compiler version S-2021.09-SP2-1_Full64; Runtime version S-2021.09-SP2-1_Full64;  May  7 17:46 2022
signed out(%d): -3
signed out(%b): 11101
unsigned out(%d): 29
unsigned out(%b): 11101
           V C S   S i m u l a t i o n   R e p o r t
```

```
xcelium> run
signed out(%d): -3
signed out(%b): 11101
unsigned out(%d): 29
unsigned out(%b): 11101
xmsim: *W,RNQUIE: Simulation is complete.
```

##### operands are mixed

|               | inA (signed) | inB (unsigned) | outSub<br />(signed/unsigned) |
| ------------- | ------------ | -------------- | ----------------------------- |
|               | 1111 (-1)    | 0010 (2)       |                               |
| *extend sign* | **0**1111    | **0**0010      |                               |
| *sub result*  |              |                | 01101                         |

```verilog
module tb;
	reg signed [3:0] inA;
	reg [3:0] inB;
	reg signed [4:0] outSubSg;
	reg [4:0] outSubUs;

	initial begin
		inA = 4'b1111;
		inB = 4'b0010;
		outSubUs = inA - inB;
		outSubSg = inA - inB;

		$display("signed out(%%d): %0d", outSubSg);
		$display("signed out(%%b): %b", outSubSg);

		$display("unsigned out(%%d): %0d", outSubUs);
		$display("unsigned out(%%b): %b", outSubUs);
	end
endmodule
```

```
Compiler version S-2021.09-SP2-1_Full64; Runtime version S-2021.09-SP2-1_Full64;  May  7 17:50 2022
signed out(%d): 13
signed out(%b): 01101
unsigned out(%d): 13
unsigned out(%b): 01101
           V C S   S i m u l a t i o n   R e p o r t 
```

```
xcelium> run
signed out(%d): 13
signed out(%b): 01101
unsigned out(%d): 13
unsigned out(%b): 01101
xmsim: *W,RNQUIE: Simulation is complete.
xcelium> exit
```



### Danger Sign

[https://projectf.io/posts/numbers-in-verilog/](https://projectf.io/posts/numbers-in-verilog/)

> Verilog has a nasty habit of treating everything as unsigned unless all variables in an expression are signed. To add insult to injury, most tools won’t warn you if signed values are being ignored.
>
> If you take one thing away from this post:
>
> **Never mix signed and unsigned variables in one expression!**

```verilog
module signed_tb ();
    logic [7:0] x;  // 'x' is unsigned
    logic signed [7:0] y;  // 'y' is signed
    logic signed [7:0] x1, y1;
    logic signed [3:0] move;

    always_comb begin
        x1 = x + move;  // !? DANGER: 'x' is unsigned but 'move' is signed
        y1 = y + move;
    end

    initial begin
        #10
        $display("Coordinates (7,7):");
        x = 8'd7;
        y = 8'd7;
        #10
        $display("x : %b  %d", x, x);
        $display("y : %b  %d", y, y);

        #10
        $display("Move +4:");
        move = 4'sd4;  // signed positive value
        #10
        $display("x1: %b  %d  *LOOKS OK*", x1, x1);
        $display("y1: %b  %d", y1, y1);

        #10
        $display("Move -4:");
        move = -4'sd4;  // signed negative value
        #10
        $display("x1: %b  %d  *SURPRISE*", x1, x1);     // 0000_0111 + {0000}_1100 = 0001_0011
        $display("y1: %b  %d", y1, y1);                 // 0000_0111 + {1111}_1100 = 0000_0011
    end
endmodule
```

```
Chronologic VCS simulator copyright 1991-2021
Contains Synopsys proprietary information.
Compiler version S-2021.09-SP2-2_Full64; Runtime version S-2021.09-SP2-2_Full64;  Nov 19 11:02 2022                                     
Coordinates (7,7):
x : 00000111    7
y : 00000111            7
Move +4:
x1: 00001011           11  *LOOKS OK*
y1: 00001011           11
Move -4:
x1: 00010011           19  *SURPRISE*
y1: 00000011            3
           V C S   S i m u l a t i o n   R e p o r t
Time: 60
CPU Time:      0.260 seconds;       Data structure size:   0.0Mb
```



### reference

Lee WF. Learning from VLSI Design Experience  [electronic Resource] / by Weng Fook Lee. 1st ed. 2019. Springer International Publishing; 2019. doi:10.1007/978-3-030-03238-8

[Bevan Baas, VLSI Digital Signal Processing, EEC 281 - VLSI Digital Signal Processing](https://www.ece.ucdavis.edu/~bbaas/281/)



