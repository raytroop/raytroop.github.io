---
title: Custom Bindkey of Cadence Virtuoso
date: 2022-04-13 17:21:33
tags:
- virtuoso
- schematic
- layout
categories:
- cad
---

## schBindKeys.il

> schematic

```
alias bk hiSetBindKey
when ( isCallable('schGetEnv')
bk("Schematics" "Ctrl<Key>x" "schHiCreateInst(\"basic\" \"nonConn\" \"symbol\")")
bk("Schematics" "Ctrl<Key>v" "schHiCreateInst(\"analogLib\" \"vdc\" \"symbol\")")
bk("Schematics" "Ctrl<Key>g" "schHiCreateInst(\"analogLib\" \"gnd\" \"symbol\")")
bk("Schematics" "Shift<Key>9" "geDeleteNetProbe()")
bk("Schematics" "<Key>0" "geDeleteAllProbe(getCurrentWindow()t)")
)
unalias bk
```

## leBindKeys.il

> layout

```
alias bk hiSetBindKey
when ( isCallable('leGetEnv)
    bk("Layout" "<Key>1" "leSetEntryLayer(\"M0PO\") leSetAllLayerVisible(nil) leSetEntryLayer(\"M0OD\") leSetEntryLayer(\"VIA0\") leSetEntryLayer(list(\"M1\" \"pin\")) leSetEntryLayer(\"M1\") hiRedraw()" )
    ; M1-VIA1-M2
    bk("Layout" "<Key>2" "leSetEntryLayer(\"M1\") leSetAllLayerVisible(nil) leSetEntryLayer(\"VIA1\") leSetEntryLayer(list(\"M2\" \"pin\")) leSetEntryLayer(\"M2\") hiRedraw()" )
    ; M2-VIA2-M3
    bk("Layout" "<Key>3" "leSetEntryLayer(\"M2\") leSetAllLayerVisible(nil) leSetEntryLayer(\"VIA2\") leSetEntryLayer(list(\"M3\" \"pin\")) leSetEntryLayer(\"M3\") hiRedraw()" )
    ; M3-VIA3-M4
    bk("Layout" "<Key>4" "leSetEntryLayer(\"M3\") leSetAllLayerVisible(nil) leSetEntryLayer(\"VIA3\") leSetEntryLayer(list(\"M4\" \"pin\")) leSetEntryLayer(\"M4\") hiRedraw()" )
    ; M4-VIA4-M5
	; select M4 layer, turn off other layer visibilty, select VIA4 M5_pin M5 and turn on them
    bk("Layout" "<Key>5" "leSetEntryLayer(\"M4\") leSetAllLayerVisible(nil) leSetEntryLayer(\"VIA4\") leSetEntryLayer(list(\"M5\" \"pin\")) leSetEntryLayer(\"M5\") hiRedraw()" )
    ; all visiable
    bk("Layout" "<Key>0" "leSetAllLayerVisible(t) hiRedraw()" )
)
unalias bk
```

