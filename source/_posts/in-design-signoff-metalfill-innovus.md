---
title: In-design Sign-off Metal Fill Flow in Innovus
date: 2022-03-05 18:18:37
tags:
- metalfill
- dummy metal
categories:
- innovus
---

Before inserting sign-off metal fill, stream out a GDSII stream file of the current database. Specify the mapping file and units that match with the rule deck you specify while inserting metal fill. If necessary, include the detailed-cell (`-merge` option) Graphic Database System (GDS).

**PVS:**

```tcl
streamOut -merge $GDSFile -mode ALL -units $GDSUNITS -mapFile $GDSMAP -outputMacros pvs.fill.gds
run_pvs_metal_fill -ruleFile $DUMMYRULE -defMapFile $DEFMAP -gdsFile pvs.fill.gds -cell [dbgDesignName]
```

**Pegasus:**
```tcl
streamOut -merge $GDSFile -mode ALL -units $GDSUNITS -mapFile $GDSMAP -outputMacros pegasus.fill.gds
run_pegasus_metal_fill -ruleFile $DUMMYRULE -defMapFile $DEFMAP -gdsFile pegasus.fill.gds -cell [dbgDesignName]
```

> Just replace `run_pvs_metal_fill` with `run_pegasus_metal_fill`

**Note**: Innovus metal fill (e.g. `addMetalFill`, `addViaFill`, etc.) does not support 20nm and below node design rules. We strongly  recommend the Pegasus/PVS metal fill solution for 20nm and below. If you have sign-off metal fill rule deck for 28nm and above available, we recommend you to move to Pegasus/PVS solution too.

> 1. `trimMetalFillNearNet` does not check DRC rules. It only removes the metal fill with specified spacing
>
> 2. **Do not** perform ECO operations after dump in sign-off metal fill (by `run_pvs_metal_fill` or `run_pegasus_metal_fill`), especially, at 20nm and below nodes. 
>
> 3. If you perform an ECO action, the tool cannot get DRC clean because `trimMetalFill` does not support 20nm and below node design rules.
> 4. The sign-off metal fill typically does not cause DRC issues with regular wires. 



The `run_pvs_metal_fill` command does the following:

- Runs PVS with the fill rules to create a GDSII output file.
- Converts the GDSII to a DEF format file based on the GDSII to DEF layermap provided.
- **Loads the resulting DEF file into Innovus**.

Pegasus is similar to  PVS, shown as below,

The `run_pegasus_metal_fill` command does the following:

- Runs Pegasus with the fill rules to create a GDSII output file.
- Converts the GDSII to a DEF format file based on the GDSII to DEF layermap provided.
- Loads the resulting DEF file into Innovus.

**Reference:**

Innovus User Guide, Product Version 21.12, Last Updated in November 2021

