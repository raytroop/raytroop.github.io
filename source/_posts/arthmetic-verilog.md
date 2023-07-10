---
title: Arithmetic in Verilog
date: 2022-05-29 16:01:08
tags:
- verilog
- arithmetic
- signed
- overflow
- underflow
categories:
- digital
---

#### unsigned + unsigned = unsigned

```verilog
function [7:0] satadd_uuu8b;   // unsigned + unsigned = unsigned
    input [7:0] a;
    input [7:0] b;

    reg [8:0] t;   // extend 1b
    begin
        t = {1'b0, a} + {1'b0, b};
        satop_uuu16b = t[8] ? {8{1'b1}} : t[7:0];
    end
endfunction
```

> `1'b1`: overflow

#### signed + signed = signed

```verilog
function [7:0] satadd_sss8b;    // signed + signed = signed
    input signed    [7:0] a;
    input signed    [7:0] b;

    reg signed [8:0] t; // extend 1b
    begin
        t = a + b;  // extend sign bit automatically
        satadd_sss8b =  (t[8:7] == 2'b01) ? {1'b0, 7{1'b1}} : // up sat
                        (t[8:7] == 2'b10) ? {1'b1, 7{1'b0}} : // dn sat
                                            t[7:0];
    end
endfunction
```

> `2'b01`: overflow
>
> `2'b10`: underflow

#### signed + unsigned = unsigned

```verilog
function [7:0] satadd_suu8b;    // signed + unsigned = unsigned
    input signed    [7:0] a;
    input           [7:0] b;

    reg signed [8:0] t; // extend 1b
    begin
        t = {a[7], a} + {1'b0, b};
        satadd_ssu8b =  (t[8:7] == 2'b10) ? {8{1'b1}} : // up saturate for unsigned
                        (t[8:7] == 2'b11) ? {8{1'b0}} : // dn saturate for unsigned
                                            t[7:0];
    end
endfunction
```



#### signed + unsigned = signed

```verilog
function signed [7:0] satop_sus8b;    //signed +/- unsigned = signed
    input signed    [7:0] a;
    input           [7:0] b;
    input plus;

    reg signed [8:0] t;    // extend 1b
    begin
        if(plus) begin
            t = {a[7], a} + {1'b0, b};
            satop_sus8b = (t[8:7]==2'b01) ? {1'b0, {7{1'b1}}}   // up saturate for signed
                                             : t[7:0];
        end else begin
            t = {a[7], a} - {1'b0, b};
            satop_sus8b = (t[8:7]==2'b10) ? {1'b1, {7{1'b0}}}   // dn saturate for signed
                                             : t[7:0];
        end
    end
endfunction
```
