---
title: Overflow Detection in Verilog
date: 2022-05-07 21:12:38
tags:
- overflow
- verilog
categories:
- digital
mathjax: true
---



- Arithmetic operations have a potential to run into a condition known as *overflow*.
- Overflow occurs with respect to the **size of the data type** that must accommodate the result.
- Overflow indicates that the result was *too large* or *too small* to fit in the original data type.



## Overflow when adding unsigned number

When two unsigned numbers are added, overflow occurs if

- there is a **carry out** of the leftmost bit.



## Overflow when adding signed numbers

When two signed 2's complement numbers are added, overflow is detected if:

1. both operands are positive and the result is negative, or
2. both operands are negative and the result is positive.

Notice that when operands have **opposite signs**, their sum will never overflow. Therefore, *overflow can only occur when the operands have the same sign*.

| A            | B            | carryout_sum   | overflow  |
| ------------ | ------------ | -------------- | --------- |
| **0**11 (3)  | **0**11 (3)  | 0_**1**10 (6)  | overflow  |
| **1**00 (-4) | **1**00 (-4) | 1_**0**00 (-8) | underflow |
| **1**11 (-1) | **1**10 (-2) | 1_**1**01 (-3) | -         |

> carryout information **ISN'T** needed to detect overflow/underflow for signed number addition



### EXTBIT:MSB

extended 1bit and msb bit can be used to detect overflow or underflow

```verilog
reg signed  [1:0]      acc_inc;
reg signed  [10-1:0]   acc;
wire signed [10  :0]   acc_w;  // extend 1b for saturation
wire signed [10-1:0]   acc_stat;

assign acc_w = acc + acc_inc;   // signed arithmetic

assign acc_stat = (acc_w[10-1 +: 2] == 2'b01) ? {1'b0, {(10-1){1'b1}}} : // up saturation
    (acc_w[10-1 +: 2] == 2'b10) ? {1'b1, {(10-1){1'b0}}}  :   			 // down saturation
    acc_w[10-1:0];
```

> `2'b01` : overflow, up saturation
>
> `2'b10`: underflow, down saturation



##  2's complement negative number

1. Flip all bits
2. Add **1**.

N-bit signed number
$$
A = -M_{N-1}2^{N-1}+\sum_{k=0}^{N-2}M_k2^k
$$
Flip all bits
$$\begin{align}
A_{flip} &= -(1-M_{N-1})2^{N-1} +\sum_{k=0}^{N-2}(1-M_k)2^k \\
&= M_{N-1}2^{N-1}-\sum_{k=0}^{N-2}M_k2^k -2^{N-1}+\sum_{k=0}^{N-2}2^k \\
&= M_{N-1}2^{N-1}-\sum_{k=0}^{N-2}M_k2^k -1
\end{align}$$

Add **1**
$$\begin{align}
A_- &= A_{flip}+1 \\
&= M_{N-1}2^{N-1}-\sum_{k=0}^{N-2}M_k2^k \\
&= -A
\end{align}$$



## reference

Overflow Detection: [http://www.c-jump.com/CIS77/CPU/Overflow/lecture.html](http://www.c-jump.com/CIS77/CPU/Overflow/lecture.html)
