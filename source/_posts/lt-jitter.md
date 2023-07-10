---
title: Long-Term Jitter
date: 2023-09-16 23:48:05
tags:
- jitter
categories:
- analog
mathjax: true
---

**long-term jitter**  is sometimes referred to as the **accumulated jitter**

![image-20230916235523070](lt-jitter/image-20230916235523070.png)

- Cycle-Cycle Jitter
  $$
  \delta(\tau _2 - \tau _1) = \sqrt{2}\times\delta (\tau_1)
  $$
  

- Long Term Jitter
  $$
  \delta(\tau_N) = \sqrt{N}\times\delta (\tau_1)
  $$
  

##  Short Term Jitter

![image-20230916235240675](lt-jitter/image-20230916235240675.png)

![image-20230916235314423](lt-jitter/image-20230916235314423.png)



## Long Term Jitter (LTJ)

![image-20230916235647723](lt-jitter/image-20230916235647723.png)

![image-20230916235709504](lt-jitter/image-20230916235709504.png)



## measuring long-term jitter

![image-20230916235033464](lt-jitter/image-20230916235033464.png)

## Jitter Calculation Examples

![image-20230917003028143](lt-jitter/image-20230917003028143.png)



## references

AN10007 Clock Jitter Definitions and Measurement Methods, SiTime [[pdf](https://www.sitime.com/sites/default/files/hiddenresources/AN10007-Jitter-and-measurement-methods_SIT.pdf)]

SERDES Design and Simulation Using the Analog FastSPICE Platform, Silicon Creations [[pdf](https://www.siliconcr.com/sc-cms/uploads/u2u_presentation_sc_april25.pdf)]

Flexible clocking solutions in advanced processes from 180nm to 5nm, Silicon Creations [[pdf](https://www.siliconcr.com/sc-cms/uploads/siliconcreations_iccad_2019_v2_191020.pdf)]

One-size-fits-all PLLs for Advanced Samsung Foundry Processes, Silicon Creations [[pdf](https://www.siliconcr.com/sc-cms/uploads/siliconcreations_dac_2022_v2_22-07-12.pdf)]

Circuit Design and Verification of 7nm LowPower, Low-Jitter PLLs, Silicon Creations, [[pdf](https://www.siliconcr.com/sc-cms/uploads/u2u-2018-sicr-plls-v3-180509.pdf)]

Lecture 10: Jitter, ECEN720: High-Speed Links Circuits and Systems Spring 2023 [[pdf](https://people.engr.tamu.edu/spalermo/ecen689/lecture10_ee720_jitter.pdf)]
