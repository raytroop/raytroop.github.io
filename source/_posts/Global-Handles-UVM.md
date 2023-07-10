---
title: Global Handles in UVM
date: 2022-02-23 22:33:05
tags:
categories:
- digital
---

#### Mechanism in  UVM-1.1

```verilog
function void test_base::start_of_simulation_phase(uvm_phase phase);
	super.start_of_simulation_phase(phase);
	uvm_top.print_topology(); // Will not compile in UVM-1.2
	factory.print(); // Will not compile in UVM-1.2
endfunction
```

> Global handles uvm_top and factory in uvm_pkg have been removed in UVM-1.2 and later

#### Mechanism in UVM-1.1 and UVM-1.2

Call the **get() method of the class** to retrieve the singleton handle.

```verilog
function void test_base::start_of_simulation_phase(uvm_phase phase);
	super.start_of_simulation_phase(phase);
	uvm_root::get().print_topology(); // Works in UVM-1.1 & UVM-1.2
	uvm_factory::get().print(); // Works in UVM-1.1 & UVM-1.2
endfunction
```
#### Mechanism Only in UVM-1.2

```verilog
function void test_base::start_of_simulation_phase(uvm_phase phase);
	uvm_coreservice_t cs = uvm_coreservice_t::get();
	cs.get_root().print_topology();
	cs.get_factory().print();
endfunction
```

**uvm_coreservice_t** is the uvm-1.2 mechanism for accessing all the central UVM services such as
**uvm_root**,**uvm_factory**, **uvm_report_server**, etc.

```verilog
// Using the uvm_coreservice_t:
uvm_coreservice_t cs;
uvm_factory f;
uvm_root top;
cs = uvm_coreservice_t::get();
f = cs.get_factory();
top = cs.get_root();
```
