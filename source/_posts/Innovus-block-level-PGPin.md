---
title: Innovus block level create Power Ground Pin method
date: 2022-02-10 10:52:07
tags:
- pr
categories:
- innovus
---

```tcl
editStretch x ...
selectWire ... VDD
selectWire ... GND
createPGPin -selected -onDie
```
![createPGPin_onDie.drawio](Innovus-block-level-PGPin/createPGPin_onDie.drawio.svg)