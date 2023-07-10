---
title: Hierarchical Connections and Exports UVM
date: 2022-04-02 11:24:09
tags:
categories:
- digital
---

`imp` and `port` connectors are sufficient for modeling most connections, but there is third connector, `export`, which is used exclusively in hierarchical connections.

Normally hierarchical routing is not required. A `port` on an UVC monitor can be connected directly to an `imp` in a scoreboard by specifying full hierarchical pathname (e.g., env.agent.monitor.analysis_port). The structure of an UVC is fixed and so the user knows to look in the monitor component for the analysis ports.

However the internal hierarchy of a module UVC is more arbitrary, and it may be convenient to route all the module UVC connectors to the top level to allow use without knowledge of the internal structure.



On the initiator side

- ports are routed up the hierarchy via other port instances

On the target side

- only the component which defines the communication method is allowed to have an `imp` instance. So we need a third object to route connections up the target side hierarchy - `export`



The hierarchical route must be connected at each level in the direction of control flow:

```verilog
initiator.connect(target)
```



Connection rules are as follows:

- `port` initiators can be connected to `port`, `export` or `imp` targets
- `export` initiators can be connected to `export` or `imp` targets
- `imp` cannot be connection initiator. `imp` is target only and is always the last connection object on a route



**uvm_analysis_port**

```verilog
class uvm_analysis_port # (
   	type 	T	 = 	int
) extends uvm_port_base # (uvm_tlm_if_base #(T,T))
```
**uvm_analysis_port**

```verilog
class uvm_analysis_port # (
   	type 	T	 = 	int
) extends uvm_port_base # (uvm_tlm_if_base #(T,T))
```
**uvm_analysis_imp**

```verilog
class uvm_analysis_imp #(
   	type 	T	 = 	int,
   	type 	IMP	 = 	int
) extends uvm_port_base #(uvm_tlm_if_base #(T,T))
```



**QA**

1. What are the three distinct functions of a scoreboard?

   Reference model, expected data storage and comparison

2. To how many consumer components can an analysis port be connected?

   Any number, including zero

3. What are the names of the two declarations made available by the following macro:

   ```verilog
   `uvm_analysis_imp_decl(_possible)
   ```

   Subclass `uvm_analysis_imp_possible`

   Method `write_possible`

4. Why should a scoreboard clone the data received by a `write` method?

   The `write` method only sends a reference, therefore if the sending component uses the same reference for every data item, overwriting of data in the storage function of the scoreboard is possible without cloning.

