---
title: Layout Tricks Part 1 - compact, drain and source sharing
date: 2022-02-19 22:24:22
tags:
- layout
- finfet
- mos
categories:
- analog
---

All credits to my colleague, Zhang Wenpian.

### Planar process vs. FinFet process

![local_Interconnect.drawio](layout-tricks-part1/local_Interconnect.drawio.svg)

### Standard Cell  Tapcell
![tapcell.drawio](layout-tricks-part1/tapcell.drawio.svg)

### Guard Ring in Custom block

Place well tie and substrate tie where they are needed. Redundant guard ring consume area and increase the routing of critical signal net.

![guardring_stypes.drawio](layout-tricks-part1/guardring_stypes.drawio.svg)

### Continuous OD

#### Performance & Matching 

![image-20220219223723289](layout-tricks-part1/image-20220219223723289.png)

#### current mirror

split diffusion with dummy transistors

![mirror_continuous_OD_split_with_dummy.drawio](layout-tricks-part1/mirror_continuous_OD_split_with_dummy.drawio.svg)

#### cascode structure

off transistor split diffusion

![cascode_continuous_OD_split_with_dummy.drawio](layout-tricks-part1/cascode_continuous_OD_split_with_dummy.drawio.svg)

#### sharing source & drain

![sharing_SD.drawio](layout-tricks-part1/sharing_SD.drawio.svg)



### Stacked MOSFETs





### reference

A. L. S. Loke et al., "Analog/mixed-signal design challenges in 7-nm CMOS and beyond," 2018 IEEE Custom Integrated Circuits Conference (CICC), 2018, pp. 1-8, doi: 10.1109/CICC.2018.8357060.

Stacked MOSFETs in analog layout [https://pulsic.com/stacked-mosfets-in-analog-layout/](https://pulsic.com/stacked-mosfets-in-analog-layout/ )
