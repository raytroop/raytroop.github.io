---
title: "Layout - The Other Half of Analog Design"
date: 2022-11-19 12:52:45
tags:
categories:
- analog
---

## drain and source sharing
### Planar process vs. FinFet process

![local_Interconnect.drawio](layout/local_Interconnect.drawio.svg)

### Standard Cell  Tapcell
![tapcell.drawio](layout/tapcell.drawio.svg)

### Guard Ring in Custom block

Place well tie and substrate tie where they are needed. Redundant guard ring consume area and increase the routing of critical signal net.

![guardring_stypes.drawio](layout/guardring_stypes.drawio.svg)

### Continuous OD

#### Performance & Matching

![image-20220219223723289](layout/image-20220219223723289.png)

#### current mirror

split diffusion with dummy transistors

![mirror_continuous_OD_split_with_dummy.drawio](layout/mirror_continuous_OD_split_with_dummy.drawio.svg)

#### cascode structure

off transistor split diffusion

![cascode_continuous_OD_split_with_dummy.drawio](layout/cascode_continuous_OD_split_with_dummy.drawio.svg)

#### sharing source & drain

![sharing_SD.drawio](layout/sharing_SD.drawio.svg)



### Stacked MOSFETs


## Matching

1. Common Centroid

   The common centroid technique describes that if there are n blocks which are to be matched then the blocks are arranged symmetrically around the common centre at equal distances from the centre. This technique offers best matching for devices as it helps in avoiding cross-chip gradients

   ![HTML5 Icon](layout/figure13.jpeg)

2. Inter-digitation

   Interdigitation reduces the device mismatch as it suffers equally from process variations in X dimension. This technique was used to layout current mirrors and resistors in PTAT and BGR circuits. In the Figure-15 below each brown stick represents a PFET of uniform length. This representation is termed as an inter-digitated layout.

   ![HTML5 Icon](layout/figure14.jpeg)





## reference

Mikael Sahrling, Layout Techniques for Integrated Circuit Designers 1st Edition , Artech House 2022

LAYOUT, [EE6350 VLSI Design Lab](http://www.ee.columbia.edu/~kinget/EE6350_S16/)  SMART TEMPERATURE SENSOR  URL: [https://www.ee.columbia.edu/~kinget/EE6350_S16/06_TEMPSENS_Sukanya_Vani/layout.html](https://www.ee.columbia.edu/~kinget/EE6350_S16/06_TEMPSENS_Sukanya_Vani/layout.html)

A. L. S. Loke et al., "Analog/mixed-signal design challenges in 7-nm CMOS and beyond," 2018 IEEE Custom Integrated Circuits Conference (CICC), 2018, pp. 1-8, doi: 10.1109/CICC.2018.8357060.

Stacked MOSFETs in analog layout [https://pulsic.com/stacked-mosfets-in-analog-layout/](https://pulsic.com/stacked-mosfets-in-analog-layout/)

JED Hurwitz, ISSCC2011 "T4: Layout: The other half of Nanometer CMOS Analog Design" [[slides](https://www.nishanchettri.com/isscc-slides/2011%20ISSCC/TUTORIALS/ISSCC2011Visuals-T4.pdf), [transcript](https://www.nishanchettri.com/isscc-slides/2011%20ISSCC/TUTORIALS/Transcription_T4.pdf)]
