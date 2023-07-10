---
title: UVM project topology
date: 2022-03-21 15:34:34
tags:
- uvm
- sv
categories:
- digital
---

Most user-defined UVM classes are placed in *separate files*

Classes can only be compiled from a *module* or *package scope*

Recommendation:

- Include related class files into a package
- Import the package into modules where required

The UVM library is supplied in the package `uvm_pkg`

- Import package to access library
- The macro file `uvm_macros.svh` must be included separately

yapp_packet.sv

```verilog
class yapp_packet extends uvm_sequence_item;
    ...
endclass : yapp_packet   
```



yapp_pkg.sv

```verilog
package  yapp_pkg;
	import uvm_pkg::*;
	`include "uvm_macros.svh"

	`include "yapp_packet.sv"
endpackage : yapp_pkg
```



run.f for `xrun`

```bash
// 64 bit option for AWS labs
-64

 -uvmhome CDNS-1.2

// include directories
-incdir ../sv

// compile files
../sv/yapp_pkg.sv
./top.sv
```

