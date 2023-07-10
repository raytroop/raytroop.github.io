---
title: Antenna Effect
date: 2023-08-08 09:41:13
tags:
categories:
- analog
mathjax: true
---


The **antenna effect** is a common name for the effects of *charge accumulation* in *isolated nodes* of an integrated circuit *during its processing*.

> This effect is also sometimes called "Plasma Induced Damage", "Process Induced Damage" (PID) or "charging effect".



## antenna ratio

The antenna rule specifies the maximum tolerance for the ratio of a metal line area to the area of connected gates.


## metal jumping

Long metal can be taken to *higher metal* routing layer. This is known as **metal jumping**. 

> This metal jumping will break the long interconnect and hence the charge collected on the long interconnect will not discharge through gate oxide because the higher metal layer is not yet fabricated. 

> so, if the gate immediately connects to the highest level by jump-up metals, large amount of charges can not be collected, while the poly finally connected to the diffusion part by highest level, thus no antenna violation will normally occure.

## Diode Insertion

Diode helps dissipate charges accumulated on metal. Diode should be placed as near as possible to the gate of device on low level of metal.

> Diode should always be connected in *reverse bias*, with cathode connected to gate electrode and anode connected to ground potential.


## reference

Tuvia Liran, Antenna effect (PID): Do the design rules really protect us? [[link](https://www.eetimes.com/antenna-effect-do-the-design-rules-really-protect-us/)]

Upma Pawan Kumar, Sunandan Chaubey, Antenna Effect in 16nm Technology Node [[link](https://www.design-reuse.com/articles/48227/antenna-effect-in-16nm-technology-node.html)]

pulsic.com, Analog layout – Stop the antenna effect from destroying your circuit [[link](https://pulsic.com/analog-layout-stop-the-antenna-effect-from-destroying-your-circuit/)]

BuBuChen, 積體電路的天線效應 (Antenna Effect in IC) [[link](https://www.bubuchen.com/2020/04/Antenna-Effect.html)]

EDN, Antenna violations resolved using new method [[link](https://www.edn.com/antenna-violations-resolved-using-new-method/)]

edaboard.com, why jump up metal can solve the antenna effect? [[link](https://www.edaboard.com/threads/why-jump-up-metal-can-solve-the-antenna-effect.177890/post-745696)]

siliconvlsi.com, Antenna effect [[link](https://siliconvlsi.com/antenna-effect/)]

Prof. Adam Teman, Digital VLSI Design. Lecture-10-The-Manufacturing-Process [[pdf](https://www.eng.biu.ac.il/temanad/files/2017/02/Lecture-10-The-Manufacturing-Process.pdf)]

