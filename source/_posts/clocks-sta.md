---
title: primary clock, generated clock and virtual clock in SDC
date: 2022-03-01 19:15:43
tags:
categories:
- digital
---

**primary clocks**

- Primary clocks should be created at input ports and output pins of black boxes.
- Never create clocks on hierarchy pins. Creating clocks on hierarchy will cause problems when reading SDF. The net timing arc becomes segmented at the hierarchy and PrimeTime will be unable to annotate the net successfully.

**generated clocks**

- Generated clocks are generally created for waveform modifications of a primary clock (not including simple inversions). PrimeTime does not simulate a design and thus will **not** derive internally generated clocks automatically - these clocks must be created by the user and applied as a constraint.
- PrimeTime caculate source latency for generated clocks if primary clock is **propagated**, otherwise its source latency is zero.

```tcl
# primary clock
create_clock -period 4 [get_ports Clk]
set_clock_latency -source 2 [get_clocks Clk]
set_propagated_clock [get_clocks Clk]
create_generated_clock -divide_by 2 -name div_clk -source [get_ports Clk] FF3/Q
```

**virtual clocks**

- Are clock objects without a source
- Do not clock sequential devices within the current_design
- Serve as references of input or output delays

```tcl
# create a virtual clock, vclk, for input and output delay constraints
create_clock -period 5 -name vclk
set_input_delay -max 2 -clock vclk [get_ports in1]
set_output_delay -max 1 -clock vclk [get_ports out2]
```

> There is **no** network latency to calculate, even if a virtual clock is propagated.

