---
title: MOS Capacitor
date: 2022-09-24 00:29:21
tags:
categories:
- analog
mathjax: true
---

![image-20241120201536599](MOS-Cap/image-20241120201536599.png)

---



## MOS capacitances

- **oxide capacitance** (aka **gate-channel capacitance**) between the *gate* and the *channel* $C_1=WLC_{ox}$
  - divided between $C_{GS}$ and $C_{GD}$
- **depletion capacitance** between the *channel* and the *substrate* $C_2$
- **overlap capacitance**: direct overlap and fringing field
- **junction capacitance** between the *source/drain* areas and the *substrate*
  - The value of $C_{SB}$ and $C_{DB}$ is a function of the source and drain voltages with respect to the substrate

![image-20240727134110758](MOS-Cap/image-20240727134110758.png)

![image-20240727134150216](MOS-Cap/image-20240727134150216.png)



> The **gate-bulk capacitance** is usually neglected in the triode and saturation regions because the inversion layer acts as a "shield" between the gate and the bulk.

---

classification with **Intrinsic** and **Extrinsic** MOS capacitor

[[Circuit Insights - 11-CI: Fundamentals 4 Tsinghua Nan Sun](https://youtu.be/sAQqkdpvsZA?si=oTnYVNmPY7yMhBPt)]



![image-20241120201251573](MOS-Cap/image-20241120201251573.png)

![image-20241120201118276](MOS-Cap/image-20241120201118276.png)

![image-20241120201127218](MOS-Cap/image-20241120201127218.png)

![image-20241120201309635](MOS-Cap/image-20241120201309635.png)



![image-20250621113254648](MOS-Cap/image-20250621113254648.png)

> ![image-20250621122921814](MOS-Cap/image-20250621122921814.png)

![image-20241120201603222](MOS-Cap/image-20241120201603222.png)




## FinFET Parasitic Fringing Capacitance

![image-20241120201725441](MOS-Cap/image-20241120201725441.png)

![image-20241120201739690](MOS-Cap/image-20241120201739690.png)



## Temperature Dependence of Junction Diode CV

![image-20240901234200243](MOS-Cap/image-20240901234200243.png)



where *TCJ* and *TCJSW* are positive



> https://cmosedu.com/cmos1/BSIM4_manual.pdf
>
> ![image-20240901235359149](MOS-Cap/image-20240901235359149.png)
>
> ![image-20240901235425992](MOS-Cap/image-20240901235425992.png)
>
> ![image-20240901235543033](MOS-Cap/image-20240901235543033.png)



## varactor

### D=S=B varactor

![image-20220924003223575](MOS-Cap/image-20220924003223575.png)





![image-20250622205317309](MOS-Cap/image-20250622205317309.png)



###  Inversion-mode (I-MOS)

![image-20220924003314979](MOS-Cap/image-20220924003314979.png)

---

![image-20250622211213169](MOS-Cap/image-20250622211213169.png)



### Accumulation-mode (A-MOS)

![image-20250622211513994](MOS-Cap/image-20250622211513994.png)



![image-20250622212138953](MOS-Cap/image-20250622212138953.png)



> NMOS in NWELL, aka **NMOS in N-Well varactor**
>
> **Notice: S/D and NWELL are connected togethor** in layout

![image-20230504221234639](MOS-Cap/image-20230504221234639.png)

![image-20230504221313785](MOS-Cap/image-20230504221313785.png)

![image-20220924004206116](MOS-Cap/image-20220924004206116.png)



### PDK varactor

> nmoscap: NMOS in **N-Well** varactor

![image-20240703224101060](MOS-Cap/image-20240703224101060.png)

> - Base Band MOSCAP model (nmoscap) is built without effective series resistance (ESR) and effective series inductance (ESL) calibrations, which is for capacitance simulation only
> - LC-Tank MOSCAP model (moscap_rf) is for frequency-dependent Q factor and capacitance simulations



## MOS Device as Capacitor

![image-20240115225644183](MOS-Cap/image-20240115225644183.png)



![image-20240115225928617](MOS-Cap/image-20240115225928617.png)

![image-20240115225853721](MOS-Cap/image-20240115225853721.png)

---



## Voltage dependence

![image-20240115230113523](MOS-Cap/image-20240115230113523.png)

![image-20231103213004806](MOS-Cap/image-20231103213004806.png)

- capacitance of MOS gate varies **nonmonotonically** with $V_{GS}$

- "accumulation-mode" varactor varies **monotonically** with $V_{GS}$



## capacitance simulation



### VCO varactor

> Two methods: 1. pss + pac; 2. pss+psp

#### PSS + PAC

![image-20220510192206354](MOS-Cap/image-20220510192206354.png)

pss time domain

![image-20220510192351590](MOS-Cap/image-20220510192351590.png)

using the **0-harmonic**

![image-20220510192447040](MOS-Cap/image-20220510192447040.png)

#### PSS + PSP

![image-20220510192753324](MOS-Cap/image-20220510192753324.png)

using **Y11** of `psp`

![image-20220510192639080](MOS-Cap/image-20220510192639080.png)

#### comparison

![image-20220510193036717](MOS-Cap/image-20220510193036717.png)

> which are same

### inverter input

R-C, ***series*** equivalent circuit

![invCap](MOS-Cap/invCap.png)


### inverter output

R-C, ***parallel*** equivalent circuit



---

#### AC simulation

![image-20250628112910588](MOS-Cap/image-20250628112910588.png)

@vi = 0

![image-20250628104042741](MOS-Cap/image-20250628104042741.png)

sweep vi from 0 to 800mV (vdd)

![image-20250628105510374](MOS-Cap/image-20250628105510374.png)



---

#### SP simulation

![image-20250628112857124](MOS-Cap/image-20250628112857124.png)

![image-20250628112620876](MOS-Cap/image-20250628112620876.png)



> EEStream. Cadence - How to find device capacitance - DC simulation, SP simulation and Large-signal SP simulation [[https://www.youtube.com/watch?v=M3zP6eJnONk](https://www.youtube.com/watch?v=M3zP6eJnONk)]
>
> ![image-20250628114414562](MOS-Cap/image-20250628114414562.png)



## reference

Aditya Varma Muppala. MOS Varactors | Oscillators 15 | MMIC 27 [[https://youtu.be/LYCLZPQvIz0?si=yoSBZSD2j_wEx0zZ](https://youtu.be/LYCLZPQvIz0?si=yoSBZSD2j_wEx0zZ)]

R. L. Bunch and S. Raman, "Large-signal analysis of MOS varactors in CMOS -G/sub m/ LC VCOs," in IEEE Journal of Solid-State Circuits, vol. 38, no. 8, pp. 1325-1332, Aug. 2003, doi: 10.1109/JSSC.2003.814416.

T. Soorapanth, C. P. Yue, D. K. Shaeffer, T. I. Lee and S. S. Wong, "Analysis and optimization of accumulation-mode varactor for RF ICs," 1998 Symposium on VLSI Circuits. Digest of Technical Papers (Cat. No.98CH36215), 1998, pp. 32-33, doi: 10.1109/VLSIC.1998.687993. URL: [http://www-smirc.stanford.edu/papers/VLSI98s-chet.pdf](http://www-smirc.stanford.edu/papers/VLSI98s-chet.pdf)

R. Jacob Baker, 6.1 MOSFET Capacitance Overview/Review, CMOS Circuit Design, Layout, and Simulation, Fourth Edition

B. Razavi, Design of Analog CMOS Integrated Circuits 2nd

Bing Sheu, TSMC. "Circuit Design using FinFETs" [[https://www.nishanchettri.com/isscc-slides/2013%20ISSCC/TUTORIALS/ISSCC2013Visuals-T4.pdf](https://www.nishanchettri.com/isscc-slides/2013%20ISSCC/TUTORIALS/ISSCC2013Visuals-T4.pdf)]

