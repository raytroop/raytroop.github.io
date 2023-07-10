---
title: Innovus Fix DRC Violation
date: 2022-02-07 21:21:46
tags:
- pr
categories:
- innovus
---

```
clearDrc
set drc_marker_file calibre_drc_markers.err
loadViolationReport -type Calibre -filename $drc_marker_file

 

foreach marker_id [dbGet -p -e top.markers.userOriginator Calibre] {

 

editSelect -area [dbget $object.box] -layer M4

dbSet [dbGet -p top.nets.name $net ].wires.status routed

editTrim -selected
```