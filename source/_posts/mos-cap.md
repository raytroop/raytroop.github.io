---
title: MOS Capacitor
date: 2022-09-24 00:29:21
tags:
categories:
- analog
mathjax: true
---

![image-20250917184927874](mos-cap/image-20250917184927874.png)

---



## MOS capacitances

- **oxide capacitance** (aka **gate-channel capacitance**) between the *gate* and the *channel* $C_1=WLC_{ox}$
  - divided between $C_{GS}$ and $C_{GD}$
- **depletion capacitance** between the *channel* and the *substrate* $C_2$
- **overlap capacitance**: direct overlap and fringing field
- **junction capacitance** between the *source/drain* areas and the *substrate*
  - The value of $C_{SB}$ and $C_{DB}$ is a function of the source and drain voltages with respect to the substrate

![image-20240727134110758](mos-cap/image-20240727134110758.png)

![image-20240727134150216](mos-cap/image-20240727134150216.png)



> The **gate-bulk capacitance** is usually neglected in the triode and saturation regions because the inversion layer acts as a "shield" between the gate and the bulk.

---

classification with **Intrinsic** and **Extrinsic** MOS capacitor

[[Circuit Insights - 11-CI: Fundamentals 4 Tsinghua Nan Sun](https://youtu.be/sAQqkdpvsZA)]



![image-20250917185006503](mos-cap/image-20250917185006503.png)

![image-20250917185041255](mos-cap/image-20250917185041255.png)

![image-20250917185106474](mos-cap/image-20250917185106474.png)

![image-20250917185146601](mos-cap/image-20250917185146601.png)



![image-20250621113254648](mos-cap/image-20250621113254648.png)

> ![image-20250621122921814](mos-cap/image-20250621122921814.png)

![image-20250917185223939](mos-cap/image-20250917185223939.png)


## FinFET Parasitic Fringing Capacitance

![image-20241120201725441](mos-cap/image-20241120201725441.png)

![image-20241120201739690](mos-cap/image-20241120201739690.png)



## Temperature Dependence of Junction Diode CV

![image-20240901234200243](mos-cap/image-20240901234200243.png)



where *TCJ* and *TCJSW* are positive



> https://cmosedu.com/cmos1/BSIM4_manual.pdf
>
> ![image-20240901235359149](mos-cap/image-20240901235359149.png)
>
> ![image-20240901235425992](mos-cap/image-20240901235425992.png)
>
> ![image-20240901235543033](mos-cap/image-20240901235543033.png)



## Integrated varactors

### D=S=B varactor

![image-20220924003223575](mos-cap/image-20220924003223575.png)





![image-20250622205317309](mos-cap/image-20250622205317309.png)



###  Inversion-mode (I-MOS)

![image-20220924003314979](mos-cap/image-20220924003314979.png)

---

![image-20250622211213169](mos-cap/image-20250622211213169.png)



### Accumulation-mode (A-MOS)

![image-20250622211513994](mos-cap/image-20250622211513994.png)



![image-20250622212138953](mos-cap/image-20250622212138953.png)



> NMOS in NWELL, aka **NMOS in N-Well varactor**
>
> **Notice: S/D and NWELL are connected togethor** in layout

![image-20230504221234639](mos-cap/image-20230504221234639.png)

![image-20230504221313785](mos-cap/image-20230504221313785.png)

![image-20220924004206116](mos-cap/image-20220924004206116.png)

### I-MOS vs . A-MOS

> P. Andreani and S. Mattisson, "On the use of MOS varactors in RF VCOs," in *IEEE Journal of Solid-State Circuits*, vol. 35, no. 6, pp. 905-910, June 2000 [[https://sci-hub.se/10.1109/4.845194](https://sci-hub.se/10.1109/4.845194)]

![image-20250917193743547](mos-cap/image-20250917193743547.png)

### varactor losses

channel resistance & gate resistance

![image-20251010204657625](mos-cap/image-20251010204657625.png)



### PDK varactor

> nmoscap: NMOS in **N-Well** varactor

![image-20240703224101060](mos-cap/image-20240703224101060.png)

> - Base Band MOSCAP model (nmoscap) is built without effective series resistance (ESR) and effective series inductance (ESL) calibrations, which is for capacitance simulation only
> - LC-Tank MOSCAP model (moscap_rf) is for frequency-dependent Q factor and capacitance simulations







## MOS Device as Capacitor

![image-20240115225644183](mos-cap/image-20240115225644183.png)



![image-20240115225928617](mos-cap/image-20240115225928617.png)

![image-20240115225853721](mos-cap/image-20240115225853721.png)

---



## Voltage dependence

![image-20240115230113523](mos-cap/image-20240115230113523.png)

![image-20231103213004806](mos-cap/image-20231103213004806.png)

- capacitance of MOS gate varies **nonmonotonically** with $V_{GS}$

- "accumulation-mode" varactor varies **monotonically** with $V_{GS}$





## reference

Aditya Varma Muppala. MOS Varactors | Oscillators 15 | MMIC 27 [[https://youtu.be/LYCLZPQvIz0](https://youtu.be/LYCLZPQvIz0)]

Adam Teman. Practice 7: CMOS Capacitance [[note](https://uc88e07b4a3835d8c0d3e2786c3e.dl-eu.dropboxusercontent.com/cd/0/inline2/C-zlIcjGeAbVbzJOEmJ9Dj8ZrpuKycgw5wWzDfxM6UOx09dIhQokP7tW3WK2mqCr3jCPl_Gr0yY6UoSnqphm3i5idrIn5NeBDPQKJWYKCc_9t-hGe-rJYLMcXLR8I3u4pf5Ef4X-gm7S1rCQd7sdoyZdIBWFlobeh7EukHXfeRtbH84bucc6ajjqnutC3Mi3h4tpR2wI7CpjJ68Njlb6PFldYrHxvG4KtJzYCw7Zti6dEo5UsN_4imC-z9lX8F7VOxSH4aVchw8yPb2fw5zBjAPYpgJsllythGQWH-jNfH-mRpjC9x_0kg0N1pcdLSsJ4ER0d5W8KyLiPj3c1BeDh34jJwiBQWQbvnlM9r3KDCux-rvURkoTS7MflM7CBrHoVQI/file),[problem](https://uc14eb8b192323ffbf669a703c6f.dl-eu.dropboxusercontent.com/cd/0/inline2/C-wv65-nC7NXNTkeFxsL_zmPCt5EAngIoomakzPv21RMsvDGdbIWJguQyUED6juxd4IxmgGWHrP7p1VSUHyq7Yl5Z1iEDheeZukStHuVSSQHd5CR9LIX8L-xSDYG_JBYJuI4Hb0XzEGbHD0bH7tML4j5GLQEG4CvaOGdHeOmHbZxcajQgnnj6h9qPUSyWyybVGjJErH_yrBRtZS_kKx0ZF72juP4WJ12s-HToW6FIFmvRphJpSiRNECm1tNfmJ7Uv0LLwG9Dqdw2EqJ3u8t0_DZT3hDrI-FkBfTPKOF0i3tBEJmmigiz9XhVY2r9_KhfDaGHOkOjlcrMG6T2YhLju31KOqLGM8KnmofDzINkfs9iPQM1v83rKh_tvzEV-2sa9gs/file)]

R. L. Bunch and S. Raman, "Large-signal analysis of MOS varactors in CMOS -G/sub m/ LC VCOs," in IEEE Journal of Solid-State Circuits, vol. 38, no. 8, pp. 1325-1332, Aug. 2003 [[https://sci-hub.jp/10.1109/JSSC.2003.814416](https://sci-hub.jp/10.1109/JSSC.2003.814416)]

T. Soorapanth, C. P. Yue, D. K. Shaeffer, T. I. Lee and S. S. Wong, "Analysis and optimization of accumulation-mode varactor for RF ICs," 1998 Symposium on VLSI Circuits. Digest of Technical Papers (Cat. No.98CH36215), 1998, pp. 32-33, doi: 10.1109/VLSIC.1998.687993. URL: [http://www-smirc.stanford.edu/papers/VLSI98s-chet.pdf](http://www-smirc.stanford.edu/papers/VLSI98s-chet.pdf)

R. Jacob Baker, 6.1 MOSFET Capacitance Overview/Review, CMOS Circuit Design, Layout, and Simulation, Fourth Edition

B. Razavi, Design of Analog CMOS Integrated Circuits 2nd

Bing Sheu, TSMC. "Circuit Design using FinFETs" [[https://www.nishanchettri.com/isscc-slides/2013%20ISSCC/TUTORIALS/ISSCC2013Visuals-T4.pdf](https://www.nishanchettri.com/isscc-slides/2013%20ISSCC/TUTORIALS/ISSCC2013Visuals-T4.pdf)]

