---
title: How to preserve hand-instantiated cells
date: 2023-02-10 22:41:15
tags:
- sdc
- synthesis
categories:
- digital
---



To preserve the hand-instantiated cells

```
set_dont_touch [get_cells -hierarchical *dont_touch_*]
```

The instances whose name contain "dont_touch_" shall be preserved during synthesis



```verilog
// no performace concerns, rest sync use sync3 is enough

module CN_resetb_sync_cell
(
    input resetb_in,
    input clkdst,
    output resetb_out
);

`ifdef USE_VERILOG
reg [2:0] resetb_dly;
`else
wire [2:0] resetb_dly;
`endif

`ifdef USE_VERILOG
always @(posedge clkdst or negedge resetb_in)
    if (~resetb_in) resetb_dly <= 3'b000;
    else resetb_dly <= {resetb_dly[1:0], 1'b1};
`else
SDFCNQD4 dont_touch_sync_flop0 (
    .SI(1'b0),
    .SE(1'b0),
    .CP(clkdst),
    .CDN(resetb_in),
    .D(1'b1),
    .Q(resetb_dly[0])
);
SDFCNQD4 dont_touch_sync_flop1 (
    .SI(1'b0),
    .SE(1'b0),
    .CP(clkdst),
    .CDN(resetb_in),
    .D(resetb_dly[0]),
    .Q(resetb_dly[1])
);
SDFCNQD4 dont_touch_sync_flop2 (
    .SI(1'b0),
    .SE(1'b0),
    .CP(clkdst),
    .CDN(resetb_in),
    .D(resetb_dly[1]),
    .Q(resetb_dly[2])
);
`endif

assign resetb_out = resetb_dly[2];

endmodule
```

