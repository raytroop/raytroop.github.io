---
title: verilog constant part-select and indexed part-select
date: 2022-02-11 20:42:34
tags:
- verilog
categories:
- digital
---

A range of contiguous bits can be selected and is known as **part-select**. There are two types of part-selects, one with a **constant part-select** and another with an **indexed part-select**

```verilog
reg [31:0] addr;
addr [23:16] = 8'h23; //bits 23 to 16 will be replaced by the new value 'h23 -> constant part-select
```

Having a variable part-select allows it to be used effectively in loops to select parts of the vector. Although the starting bit can be **varied**, the width has to be **constant**.

> **[<start_bit +: <width>]	// part-select increments from start-bit**
>
> **[<start_bit -: <width>]	// part-select decrements from start-bit**



**Example**

```verilog
logic [31: 0] a_vect;
logic [0 :31] b_vect;

logic [63: 0] dword;
integer sel;

a_vect[ 0 +: 8] // == a_vect[ 7 : 0]
a_vect[15 -: 8] // == a_vect[15 : 8]
b_vect[ 0 +: 8] // == b_vect[0 : 7]
b_vect[15 -: 8] // == b_vect[8 :15]

dword[8*sel +: 8] // variable part-select with fixed width
```



**ref**

[Verilog scalar and vector](https://www.chipverify.com/verilog/verilog-scalar-vector#:~:text=Part%2Dselects,with%20an%20indexed%20part%2Dselect.&text=Having%20a%20variable%20part%2Dselect,select%20parts%20of%20the%20vector.)

[What is the "+:" operator called in Verilog?](https://electronics.stackexchange.com/questions/74277/what-is-the-operator-called-in-verilog)

