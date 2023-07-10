---
title: Efficient Sequence Objection in UVM
date: 2022-02-21 21:55:05
tags:
categories:
- digital
---

Objections are handled in **pre/post body** decalared in a base sequence class

This is efficient for all sequence execution options:

- Default sequences use body objections

- Test sequences use test objections

- Subsequences use objections of the root sequence which calls them

```verilog
class yapp_base_seq extends uvm_sequence#(yapp_packet);
…
    task pre_body();
        if(starting_phase != null);
        	starting_phase.raise_objection(this, get_type_name());
    endtask
    task post_body();
    	if(starting_phase != null);
    		starting_phase.drop_objection(this, get_type_name());	
    endtask
…
class yapp012 extends yapp_base_seq;
…
```

**Set as default sequence of sequencer:**

A default sequence is a root sequence, so the **pre/post body** methods are executed and objection are raised/dropped there

**Test sequence:**

A test sequence is a root sequence, so the **pre/post body** methods are executed. However, for a test sequence, `starting_phase` is `null` and so the objection is not handled in the sequence. The test must raise and drop objections

**Subsequence:**

Not a root sequence,  so **pre/post body** methods are not executed. The root sequence which ultimately called the subsequence handles the objections, using one of the two options above.



> If a **sequence** is call via a **`uvm_do** variant, the it is defined as a subsequence and its **pre/post_body()** methods are not executed.

**objection change in UVM1.2**

Raising or dropping objections directly from `starting_phase` is deprecated

- must use `get_starting_phase()` method

- prevents modification of phase during sequence

```verilog
task pre_body();
    uvm_phase sp = get_starting_phase();
    if (sp != null)
        sp.raise_objection(this, get_type_name());
endtask
```
