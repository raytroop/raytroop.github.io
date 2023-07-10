---
title: Understanding the save parameter in spectre
date: 2022-09-23 23:14:10
tags:
- spectre
- virtuoso
categories:
- cad
---

**none**: 

​	Does not save any data (currently does save one node chosen at random)

**selected**: 

​	Saves only signals specified with save statements. The default setting.

**lvlpub**:

 	Saves all signals that are normally useful up to nestlvl deep in the subcircuit hierarchy. This option is equivalent to allpub for subcircuits.

**lvl**:

​	Saves all signals up to nestlvl deep in the subcircuit hierarchy. This option is relevant for subcircuits.

**allpub**:

​	Saves only signals that are normally useful.

**all**:

​	 Saves all signals.

> Signals that are "normally useful" include the shared node voltages and currents through voltage sources and iprobes, and exclude the internal nodes on devices (the internal collector, base, emitter on a BJT, the internal drain, source on a FET, and so on). It also excludes currents through inductors, controlled sources, transmission lines, transformers, etc.
>
> If you use **lvl** or **all** instead of **lvlpub** or **allpub**, you will also get internal node voltages and currents through other components that happen to compute current. 
>
> Thus, using **\*pub** excludes internal nodes on devices (the internal collector, base, emitter on a BJT, the internal drain and source on a FET, etc). It also excludes the currents through inductors, controlled sources, transmission lines, transformers, etc.



> **nestlvl**
>
> This variable is used to save groups of signals as results and when signals are saved in subcircuits. The nestlvl parameter also specifies how many levels deep into the subcircuit hierarchy you want to save signals.

