---
title: Real Modeling with SystemVerilog using Cadence EE_pkg 101
date: 2022-03-16 22:07:49
tags:
categories:
- cad
---

## What Is Real Number Modeling?

- model analog blocks operation as signal flow model
- only the digital solver is used for high-speed simulation
  - Event-driven
  - No convergence issues, because no analog solver is used
- Five different language standards support real number modeling:
  - **wreal** (wired-real) ports in Verilog-AMS
  - **real** data type in VHDL
  - **real** data type in Verilog
  - **real** variables and **nettypes** in SystemVerilog (SV)
  - **real** types in e

## Benefits of RNM

- Most analog circuits that need to be modeled for MS verification at the SoC level can be described in terms of real-valued voltages or currents
- RNM is a mixed approach, borrowing concepts from both continuous and discrete domains
  - The values are floating-point (real) number.
  - Time is discrete; the real signals change values based on discrete events
- Applicability of RNM is bounded primarily by **signal-flow** model style
- Migrating analog behavior from the analog domain to the event or pseudo-analog domain can bring huge benefits without sacrificing too much accuracy
- Simulation is executed by a digital simulation engine without need for the analog solver
- Hence real-number modeling enables very high performance simulation of mixed-signal systems



## Limitations of RNM

- connecting **real** or **wreal** signals to electrical signals requires careful consideration
  - Too conservative an approach can lead to large numbers of timepoints
  - Too liberal an approach can lead to losing signal accuracy
- Time accuracy limited by the discrete sampling approach and the ``timescale` setting - no continuous signals anymore
- Limited capability for combination of signals by wiring outputs together
  - Requires assumptions about impedances to do simple merging

