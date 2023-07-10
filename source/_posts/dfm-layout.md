---
title: Layout and DFM
date: 2022-11-19 12:52:45
tags:
categories:
- analog
mathjax: true
---



## Wafer Acceptance Test (WAT)

> 温德通. 集成电路制造工艺与工程应用. 机械工业出版社 2018

**Wafer acceptance testing (WAT)** also known as **Process Control Monitoring (PCM)**

![image-20250802091601281](dfm-layout/image-20250802091601281.png)

---

![image-20250802101539555](dfm-layout/image-20250802101539555.png)




## Short Lg Stackgate

> TSMC. VLSI2025 JFS2-1: Analog Cells DTCO (**D**esign and **T**echnology **C**o-**O**ptimization) and Their Impact on Advanced Node CMOS Analog/MixedSignal Circuits

![image-20250719221634273](dfm-layout/image-20250719221634273.png)

> smaller **W\*L\*M,** **X\*Y** for same mismatch with short Lg stackgate

---

![image-20250719221918689](dfm-layout/image-20250719221918689.png)

>  N7/N5 ***4-fin Grid Rule***
>
>  *Same **Fin1/Fin3** or **Fin2/Fin4** Fin Position*

---

![image-20250719222047276](dfm-layout/image-20250719222047276.png)

![image-20250719222146669](dfm-layout/image-20250719222146669.png)

note W/L is different $12/(135*2) \lt 6/(8*8)$



## Current Density (EM)

![image-20250712144939547](dfm-layout/image-20250712144939547.png)

![image-20250712145414052](dfm-layout/image-20250712145414052.png)



## Interconnect Resistance Evolution

![image-20250703232709089](dfm-layout/image-20250703232709089.png)



> White Paper: Microelectronics/Semiconductor Research Community Virtual Workshop  2022 [[https://nnci.net/sites/default/files/inline-files/Microelectronics%202022%20Workshop%20Report%20with%20Slides.pdf](https://nnci.net/sites/default/files/inline-files/Microelectronics%202022%20Workshop%20Report%20with%20Slides.pdf)]



## Copper Pillar Bump vs Solder bump

Cu-pillar bumping is a next-generation flip chip interconnection between chip & packages, especially for fine pitch applications

![img](dfm-layout/pic_Cu-pillarBumping_01.svg)

![img](dfm-layout/pic_Cu-pillarBumping_02.svg)

- On the wafer end, comparing to solder bump, cu-pillar bump provides the advantage of fine pitch; the die size can be reduced about 5~10%. 

- On the package end, the substrate layer can be reduced from 6 layers to 4 layers by fine pitch and bump on trace process and using simplified substrate process. 



![image-20250613233806417](dfm-layout/image-20250613233806417.png)



## Why Your Symmetric Layouts Are Showing Mismatches in SPICE Simulations

> [[https://www.ansys.com/blog/symmetric-layouts-showing-mismatches-spice-simulations](https://www.ansys.com/blog/symmetric-layouts-showing-mismatches-spice-simulations)]



![figure-2](dfm-layout/figure-2-18wid=609&fmt=png-alpha&op_usm=0.9,1.png)

The root cause of the delay mismatch is related to *how parasitic extraction tools distribute coupling capacitances over the nodes of the resistive networks*

> The most likely reason for such asymmetry is the anisotropy of computational geometry algorithms used by extraction tools.

![figure-4](dfm-layout/figure-4-13wid=609&fmt=png-alpha&op_usm=0.9,1.png)






## STRAP

A "strap" refers to a low-impedance connection

![image-20230518001007350](dfm-layout/image-20230518001007350.png)

NWDMY = NWDMY1, NWDMY2



STRAP = NWSTRAP or PWSTRAP

NWSTRAP = {NP & OD} & {NW not {NW INTERACT NWDMY}}

PWSTRAP = {PP & OD} not NW

| cell \ pin  | PLUS    | MINUS   |
| ----------- | ------- | ------- |
| **N diode** | PWSTRAP | \       |
| **P diode** | \       | NWSTRAP |



### Calibre Rule::NOT

![image-20230518005758993](dfm-layout/image-20230518005758993.png)



### Calibre Rule::INTERACT

![image-20230518010124496](dfm-layout/image-20230518010124496.png)

![image-20230518010758342](dfm-layout/image-20230518010758342.png)





## Antenna Effect

The **antenna effect** is a common name for the effects of *charge accumulation* in *isolated nodes* of an integrated circuit ***during its processing***

> This effect is also sometimes called "*Plasma Induced Damage"*, *"Process Induced Damage" (PID)* or *"charging effect"*

![ ](dfm-layout/pastedimage1708001710744v1.png)

![ ](dfm-layout/pastedimage1708001758231v2.png)

> This **accumulation of charge** is usually, and *misleadingly*, called the **antenna effect**.



### antenna ratio

During manufacture, if part of the metal wiring is *connected to the gate*, but *not a diffusion contact*, this **"floating" metal** collects charge from the plasma.

Manufacturing rules for the antenna effect are usually expressed as the ***ratio of the area of floating metal (i.e. charge collection area) to the area of the gate***.

![image-20250714203610809](dfm-layout/image-20250714203610809.png)

To prevent the antenna effect from destroying your circuit you need to reduce the floating metal/gate area ratio or give the charge a safe way to dissipate to the ground before it can build up and cause damage



### metal jumping (bridging, metal hopping)

Long metal can be taken to ***higher metal*** routing layer, which is known as **metal jumping**. 

This metal jumping is usually done **near the gate**, which will mean that there is a full connection to the diffusion contact before the area of floating metal becomes too large

![ ](dfm-layout/pastedimage1708001758232v3.png)

> The jumper is constructed so that the long track is only connected to the gate once it has also been connected to a diffusion contact, which then allows the charge to dissipate through diffusion to the substrate



### Diode Insertion

Diode helps dissipate charges accumulated on metal. Diode should be placed as near as possible to the gate of device on low level of metal.

![ ](dfm-layout/pastedimage1708001758232v4.png)

![image-20250714204033328](dfm-layout/image-20250714204033328.png)

![main-qimg-c3fe57dfac5fd5e5b5616ddf4f89f08a-pjlq](dfm-layout/main-qimg-c3fe57dfac5fd5e5b5616ddf4f89f08a-pjlq.jpg)

> In the reverse bias region, the reverse saturation current of Si and Ge diodes doubles for every $10 ^oC$ rise in temperature

![image-20250719083520735](dfm-layout/image-20250719083520735.png)



---

> pulsic.com, Analog layout – Stop the antenna effect from destroying your circuit [[link](https://pulsic.com/analog-layout-stop-the-antenna-effect-from-destroying-your-circuit/)]
>
> Prof. Adam Teman, Digital VLSI Design. Lecture-10-The-Manufacturing-Process [[pdf](https://www.eng.biu.ac.il/temanad/files/2017/02/Lecture-10-The-Manufacturing-Process.pdf)]
>
> Zongjian Chen, Processing and Reliability Issues That Impact Design Practice. [[https://web.stanford.edu/class/archive/ee/ee371/ee371.1066/lectures/Old/lect_15_2up.pdf](https://web.stanford.edu/class/archive/ee/ee371/ee371.1066/lectures/Old/lect_15_2up.pdf)]



## Shallow Trench Isolation (STI)

![image-20241121211242335](dfm-layout/image-20241121211242335.png)

![image-20241121211348053](dfm-layout/image-20241121211348053.png)



## Voltage-Dependent DRC

In T* DRC deck, it is based on the voltage recognition CAD layer and net connection to calculate the voltage difference between two neighboring nets by the following formula:

$$
\Delta V = \max(V_H(\text{net1})-V_L(\text{net2}), V_H(\text{net2})-V_L(\text{net1}))
$$

where
$$
V_H(\text{netx}) = \max(V(\text{netx}))
$$
and 
$$
V_L(\text{netx}) = \min(V(\text{netx}))
$$

> - The $\Delta V$ will be **0** if two nets are connected as same potential
> - If $V_L \gt V_H$ **on a net**, DRC will report warning on this net

### Voltage recognition CAD Layer

> [Automate those voltage-dependent DRC checks! - siemens](https://blogs.sw.siemens.com/calibre/2015/08/18/automate-those-voltage-dependent-drc-checks/)



Two method

1. voltage text layer

   You place specific voltage text on specific drawing layer

2. voltage marker layer

   Each voltage marker layer represent different voltage for specific drawing layer

> *voltage text layer* has higher priority than *voltage marker layer* and is recommended



#### voltage text layer

For example **M3**

| Process Layer | CAD Layer# | Voltage High | Voltage High Top<br />(highest priority) | Voltage Low | Voltage Low Top<br />(highest priority) |
| ------------- | ---------- | ------------ | ---------------------------------------- | ----------- | --------------------------------------- |
| M3            | 63         | 110          | 112                                      | 111         | 113                                     |

> where **63** is **layer number**, **110 ~ 113** is **datatype**

#### voltage marker layer

Different data type represent different voltage, like

| DataType | 100  | 101  | 102  | ...  | 109  |
| -------- | ---- | ---- | ---- | ---- | ---- |
| Voltage  | 0.0  | 0.1  | 0.2  | 0.3  | 0.9  |

### Example

![image-20220503171006936](dfm-layout/image-20220503171006936.png)



## drain & source sharing

### Planar process vs. FinFet process

![local_Interconnect.drawio](dfm-layout/local_Interconnect.drawio.svg)

### Standard Cell  Tapcell
![tapcell.drawio](dfm-layout/tapcell.drawio.svg)

### Guard Ring in Custom block

Place well tie and substrate tie where they are needed. Redundant guard ring consume area and increase the routing of critical signal net.

![guardring_stypes.drawio](dfm-layout/guardring_stypes.drawio.svg)

### Continuous OD

#### Performance & Matching

![image-20220219223723289](dfm-layout/image-20220219223723289.png)

#### current mirror

split diffusion with dummy transistors

![mirror_continuous_OD_split_with_dummy.drawio](dfm-layout/mirror_continuous_OD_split_with_dummy.drawio.svg)

#### cascode structure

off transistor split diffusion

![cascode_continuous_OD_split_with_dummy.drawio](dfm-layout/cascode_continuous_OD_split_with_dummy.drawio.svg)

#### sharing source & drain

![sharing_SD.drawio](dfm-layout/sharing_SD.drawio.svg)



### Stacked MOSFETs



## LDE (Layout Dependent Effects)

> Vladimír Stejskal, Jiří Slezák March, 2016. LOD Effect: Modeling and Implementation [[https://www.mos-ak.org/dresden_2016/presentations/T5_Stejskal_MOS-AK_Dresden_2016.pdf](https://www.mos-ak.org/dresden_2016/presentations/T5_Stejskal_MOS-AK_Dresden_2016.pdf)]
>
> John Faricelli – April 16, 2009. Layout-Dependent Proximity Effects in Deep Nanoscale CMOS [[https://ewh.ieee.org/r5/denver/sscs/Presentations/2009_04_Faricelli.pdf](https://ewh.ieee.org/r5/denver/sscs/Presentations/2009_04_Faricelli.pdf)]
>
> 吉富貞幸. 2021年7月29日. 高周波RFCMOS回路を実現する半導体素子のコンパクトモデリング技術 [[https://kobaweb.ei.st.gunma-u.ac.jp/lecture/20210729_analog_KIOXIA_Yoshitomi.pdf](https://kobaweb.ei.st.gunma-u.ac.jp/lecture/20210729_analog_KIOXIA_Yoshitomi.pdf)]
>
> Kanamoto, Toshiki, Yasuhiro Ogasahara, Keiko Natsume, Kenji Yamaguchi, Hiroyuki Amishiro, Tetsuya Watanabe and Masanori Hashimoto. “Impact of well edge proximity effect on timing.” *ESSDERC 2007 - 37th European Solid State Device Research Conference* (2007)
>
> J. V. Faricelli, "Layout-dependent proximity effects in deep nanoscale CMOS," *IEEE Custom Integrated Circuits Conference 2010*, San Jose, CA, USA, 2010 [[https://sci-hub.se/10.1109/CICC.2010.5617407](https://sci-hub.se/10.1109/CICC.2010.5617407)]
>
> Aleksandr Sidun, Layout-dependent effects (LOD, WPE, Latch-up, Electromigration, Antenna) [[https://analoghub.ie/category/Layout/article/layoutDependentEffects](https://analoghub.ie/category/Layout/article/layoutDependentEffects)]

![image-20251009231152210](dfm-layout/image-20251009231152210.png)

### Length of Diffusion (LOD)

> ***Shallow Trench Isolation Stress***

**LOD key points:**

- LOD is the result of the STI formation (Shallow trench isolation);
- STI becomes compressive as the wafer cools down;
- The width of STI (active to active spacing) has a strong impact on determining stress;
- LOD improves holes mobility and decreases electron mobility.

![image-20251010201258948](dfm-layout/image-20251010201258948.png)

Stress has been more effective for PMOS

- *This has caused beta (N/P) ratio to fall to about unity at 7nm*

![image-20251009233811877](dfm-layout/image-20251009233811877.png)

> ![image-20251009234239279](dfm-layout/image-20251009234239279.png)





LOD effect can be prevented by distancing devices away from the WELL edge (guard ring). This is usually done by placing dummy devices around the circuit devices, in which case your circuit devices will also benefit from the equal edge effects (each device will have the same neighbours).

![image-20251009235236169](dfm-layout/image-20251009235236169.png)

### Well Proximity Effect (WPE)

Since the well implant dopant (acceptor or donor) is the same type as the channel implant dopant, the ***additional doping increases the absolute value of the threshold voltage (VT) of both NMOS and PMOS devices***

![image-20251009234116191](dfm-layout/image-20251009234116191.png)

![img](dfm-layout/1-Figure1-1.png)



### Gate Cut Stress LDE

![image-20251010202621882](dfm-layout/image-20251010202621882.png)



### Metal Boundary Effect (MBE)

> M. Hamaguchi et al., "New layout dependency in high-k/Metal Gate MOSFETs," 2011 International Electron Devices Meeting, Washington, DC, USA, 2011 [[https://sci-hub.st/10.1109/IEDM.2011.6131614](https://sci-hub.st/10.1109/IEDM.2011.6131614)]
>
> Alvin Loke. 2016 VLSI Circuits Short Courses – 2.2 Migrating Analog/Mixed-Signal Designs to FinFET Alvin Loke / Qualcomm [[pdf](https://picture.iczhiku.com/resource/eetop/sYIFPzErssDRkbnN.pdf)]

Gate = (ALD MG stack to set $\Phi_M$)+(metal fill to reduce RG)

![image-20251010201413941](dfm-layout/image-20251010201413941.png)

> ![image-20251010201527553](dfm-layout/image-20251010201527553.png)
>
> ![image-20251010202132434](dfm-layout/image-20251010202132434.png)



## Matching

> Aleksandr Sidun. Matching patterns in layout [[https://analoghub.ie/category/Layout/article/layoutMatchingPatterns](https://analoghub.ie/category/Layout/article/layoutMatchingPatterns)]
>
> —. Matching in layout [[https://analoghub.ie/category/Layout/article/layoutMatching](https://analoghub.ie/category/Layout/article/layoutMatching)]

![image-20251011205334957](dfm-layout/image-20251011205334957.png)

### Interdigitation

***Interdigitation*** provides good matching properties against ***1D-gradients*** and is suitable for the simple circuits

> **The main concept** is that you should create an imaginary center line and place your devices symmetrically, relative to this line. The simplest example of that is so called **"ABBA"** pattern
>
> ![image-20251011205815529](dfm-layout/image-20251011205815529.png)

![image-20251011205608993](dfm-layout/image-20251011205608993.png)

---

*Interdigitation* reduces the device mismatch as it suffers equally from process variations in *X dimension*. This technique was used to layout current mirrors and resistors in PTAT and BGR circuits.

   ![HTML5 Icon](dfm-layout/figure14.jpeg)

### Common Centroid

***Common Centroid*** provides better matching for ***2D gradients***, which is critical for the large arrays and advanced (below 28nm) nodes

> The main idea behind common centroid is that we make our array symmetrical of the common centre. In other words, the array should be symmetrical in both **X-** and **Y-** axes

![image-20251011210113327](dfm-layout/image-20251011210113327.png)



---

The *common centroid* technique describes that if there are n blocks which are to be matched then the blocks are arranged symmetrically around the common centre at equal distances from the centre. This technique offers best matching for devices as it helps in avoiding cross-chip gradients

   ![HTML5 Icon](dfm-layout/figure13.jpeg)





## Design with FinFETs

![image-20221210165644336](dfm-layout/image-20221210165644336.png)



![image-20221210165916985](dfm-layout/image-20221210165916985.png)


> Mark Williams. Stacked MOSFETs in Analog Layout [[https://community.cadence.com/cadence_blogs_8/b/cic/posts/stacked-mosfets-in-analog-layout](https://community.cadence.com/cadence_blogs_8/b/cic/posts/stacked-mosfets-in-analog-layout)]

### Modeling Consideration

![image-20221217152830191](dfm-layout/image-20221217152830191.png)

![image-20221210170042233](dfm-layout/image-20221210170042233.png)



![mos_pro](dfm-layout/mos_pro.drawio.svg)
$$\begin{align}
R_{d1} &\propto \frac{1}{N_{fins}} \\
R_{s1} &\propto \frac{1}{N_{fins}} \\
R_{g1} &\propto N_{fins} \\
C_{gd} &\propto N_{fins} \cdot N_{fingers} \cdot N_{multipler} \\
C_{gs} &= Cgd \\
C_{g1d} &\propto N_{fins} \\
C_{g1s} &= C_{g1d} \\
C_{g1d1} &\propto N_{fins} \\
C_{g1s1} &= C_{g1d1}  \\
C_{g1d1} &\simeq 2\times C_{g1d}
\end{align}$$



![image-20230708221056420](dfm-layout/image-20230708221056420.png)



### PODE & CPODE

> The PODE devices is extracted as parasitic devices in post-layout netlist

![image-20220213172653116](dfm-layout/image-20220213172653116.png)



**DDB** is the **PODE** (Poly on OD/Diffusion Edge) in TSMC 16FFC process.

**SDB** is the **CPODE** (Common Poly on Diffusion Edge) in TSMC 16FFC process.

> PO on OD edge (PODE) is a must and to define GATE that abuts OD vertical edge
>
> CPODE is used to connect two PODE cells together. It will isolate OD to save 1 poly pitch, via STI; Additional mask (12N) is required for manufacture

|                 | PODE                                                         | CPODE                                                        |
| --------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Pro's**       | simple                                                       | density                                                      |
| **Con's**       | density                                                      | LDE (LOD/OSE)                                                |
| **edge device** | 3T PODE(with single side OD): NO ERC<br />4T M-PODE (with S/D): ERC (gate tied to power/ground) | won't form device; <br />NO ERC; <br />OD under CPODE is cut off |





![image-20221210145232826](dfm-layout/image-20221210145232826.png)

![image-20221210150847737](dfm-layout/image-20221210150847737.png)

![image-20240509205506112](dfm-layout/image-20240509205506112.png)





---

> Leading Edge Logic Comparison March 9, 2018 [[https://semiwiki.com/wp-content/uploads/2018/03/Leading-Edge-Logic.pdf](https://semiwiki.com/wp-content/uploads/2018/03/Leading-Edge-Logic.pdf)]
>
> What is CPODE, and why do we use it in VLSI layout? [[https://semiconwiki.com/what-is-cpode-and-why-do-we-use-it-in-vlsi-layout/](https://semiconwiki.com/what-is-cpode-and-why-do-we-use-it-in-vlsi-layout/)]



---

**3T PODE device**

![image-20250708001318109](dfm-layout/image-20250708001318109.png)

> US9053283B2: Methods for layout verification for polysilicon cell edge structures in finFET standard cells using filters [[https://patentimages.storage.googleapis.com/36/2c/ff/ad3d4c232ecc8d/US9053283.pdf](https://patentimages.storage.googleapis.com/36/2c/ff/ad3d4c232ecc8d/US9053283.pdf)]
>
> US8943455B2: Methods for layout verification for polysilicon cell edge structures in FinFET standard cells [[https://patentimages.storage.googleapis.com/19/12/64/f2badfdc09a4a4/US8943455.pdf](https://patentimages.storage.googleapis.com/19/12/64/f2badfdc09a4a4/US8943455.pdf)]



### CNOD

continuous oxide diffusion (**CNOD**) design

![img](dfm-layout/https%253A%252F%252Fbucketeer-e05bbc84-baa3-437e-9518-adb32be77984.s3.amazonaws.com%252Fpublic%252Fimages%252F924b683b-c079-4050-ae33-577e29202814_571x411.png)

In CNOD, the diffusion is not broken at all. The fabrication process continues normally, but when standard cells need to be separated, 
the gate between them is designated as a dummy gate. This dummy gate is then connected to a *Gate Tie-Down Via to the power rail*

This dummy gate tie-down method of CNOD achieves the same horizontal width savings as *SDB*, 
and has *the advantage of keeping the transistor diffusion unbroken and thus can achieve more uniform strain and performance characteristics*


> The TRUTH of TSMC 5nm [[https://www.angstronomics.com/p/the-truth-of-tsmc-5nm](https://www.angstronomics.com/p/the-truth-of-tsmc-5nm)]
>
> S. Badel et al., "Chip Variability Mitigation through Continuous Diffusion Enabled by EUV and Self-Aligned Gate Contact," 2018 14th IEEE International Conference on Solid-State and Integrated Circuit Technology (ICSICT), Qingdao, China, 2018 [[https://sci-hub.st/10.1109/ICSICT.2018.8565694](https://sci-hub.st/10.1109/ICSICT.2018.8565694)]

---

![image-20250707210444362](dfm-layout/image-20250707210444362.png)

---

**4T MPODE (with source/drain)** may be formed in **CNOD design layout**

potential leakage: **channel leakage (S to D)**; **junction leakage (S/D to bulk)**

![image-20250708001207301](dfm-layout/image-20250708001207301.png)

---

**CNOD** (**MPODE**) is same with primitive MOS model; **PODE** is the primitive MOS, just S/D shorted together

![image-20250725215821959](dfm-layout/image-20250725215821959.png)




### Contacted-Poly-Pitch (CPP)

> Wider Contacted-Poly-Pitch allows wider MD and VD size, which help reduce MEOL IRdrop

![Schematic representation of a logic standard cell layout (CPP = contacted poly pitch, FP = fin pitch, MP = metal pitch; cell height = number of metal lines per cell x MP).](dfm-layout/imageurl=%252Fsites%252Fdefault%252Ffiles%252F2022-02%252FFigure%201%20-%20Logic%20standard%20cell%20scaling.jpeg)

*Naoto Horiguchi. Entering the Nanosheet Transistor Era  [[link](https://www.imec-int.com/en/articles/entering-nanosheet-transistor-era-0)]*

### SAC & SAGC

#### self-aligned diffusion contacts (SACs)

As shown in Fig. 35 in older planar technology nodes, gate pitch is so relaxed such that S/D contacts and gate contacts can easily be placed next to each other without causing any shorting risk (see Fig. 35(a)).

**As the gate pitch scales, there’s no room to put gate contacts next to S/D contacts, and gatecontacts have been pushed away from the active region and are only placed on the STI region.**

![image-20230708221916716](dfm-layout/image-20230708221916716.png)

In addition, at tight gate pitch, even forming *S/D contact* without shorting to *gate metal* becomes very challenging.

The idea of **self-aligned contacts (SAC)** has been introduced to mitigate the issue of S/D contact to gate shorts.

As shown in Fig. 35(b), *the gate metal is fully encapsulated by a dielectric spacer and gate cap*, which protects the gate from shorting to the S/D contact.

![image-20230708230238362](dfm-layout/image-20230708230238362.png)



>  A dielectric cap is added on top of the gate so that if the contact overlaps the gate, no short occurs.
>
>  **MD** layer represent SACs in PDK

![image-20230709005334372](dfm-layout/image-20230709005334372.png)



#### self-aligned gate contacts (SAGCs)

**Self-aligned gate contacts (SAGCs)** have also been implemented and Denser standard cells can be achieved by eliminating the need to land contacts on the gate outside the active area.

SAGCs require the source/drain contacts to be capped with an insulator that is different from both contact and gate cap dielectrics to protect the source/drain contacts against a misaligned gate contact etch.



![image-20230708233009568](dfm-layout/image-20230708233009568.png)



![image-20230708232429240](dfm-layout/image-20230708232429240.png)

> According to the DRC of T foundary, poly extension > 0 um and space between MP and OD > 0 um., which demonstrate self-aligned gate contact is **not** introduced.


### Gate Resistance

![image-20230709000326683](dfm-layout/image-20230709000326683.png)

![image-20230709004432013](dfm-layout/image-20230709004432013.png)

![image-20230709000637817](dfm-layout/image-20230709000637817.png)

![image-20230709003917922](dfm-layout/image-20230709003917922.png)



## Native NMOS Blocked Implant (NT_N)

> Principles of VLSI Design CMOS Processing CMPE 413 [[https://redirect.cs.umbc.edu/~cpatel2/links/315/lectures/chap3_lect09_processing2.pdf](https://redirect.cs.umbc.edu/~cpatel2/links/315/lectures/chap3_lect09_processing2.pdf)]
>
> CMOS processing [[http://users.ece.utexas.edu/~athomsen/cmos_processing.pdf](http://users.ece.utexas.edu/~athomsen/cmos_processing.pdf)]
>
> The Fabrication Process of CMOS Transistor [[https://www.elprocus.com/the-fabrication-process-of-cmos-transistor/#:~:text=latch%2Dup%20susceptibility.-,N%2D%20well%2F%20P%2D%20well%20Technology,well%20it%20is%20vice%2D%20verse.](https://www.elprocus.com/the-fabrication-process-of-cmos-transistor/#:~:text=latch%2Dup%20susceptibility.-,N%2D%20well%2F%20P%2D%20well%20Technology,well%20it%20is%20vice%2D%20verse.)]
>
> CMOS Processing Technology [[link1](http://ece-research.unm.edu/jimp/vlsi/slides/chap3_1.html), [link2](http://ece-research.unm.edu/jimp/vlsi/slides/chap3_2.html)]



A **native layer (NT_N)** is usually added under inductors or transformers in the nanoscale CMOS to define the non-doped high-resistance region of substrate, which decreases eddy currents in the substrate thus maintaining high Q of the coils.

> For T* PDK offered inductor, a native substrate region is created under the inductor coil to minimize *eddy currents* 

![image-20230810000702597](dfm-layout/image-20230810000702597.png)



> OD inside NT_N only can be used for NT_N potential pickup purpose, such as the guarding-ring of MOM and inductor



### Derived Geometries

| Term   | Definition           |
| ------ | -------------------- |
| PW     | {NOT NW}             |
| N+OD   | {NP AND OD}          |
| P+OD   | {PP AND OD}          |
| GATE   | {PO AND OD}          |
| TrGATE | {GATE NOT PODE_GATE} |


NP: N+ Source/Drain Ion Implantation

PP: P+ Source/Drain Ion Implantation

OD: Gate Oxide and Diffustion

NW: N-WELL

PW: P-WELL



### CMOS Processing Technology

*Four main CMOS technologies:*

- *n-well process*
- *p-well process*
- *twin-tub process*
- *silicon on insulator*





Triple well, Deep N-Well (optional):

- NWell:  NMOS svt, lvt, ulvt ...
- PWell: PMOS svt, lvt, ulvt ...
- DNW:  For isolating P-Well from the substrate

> The NT_N drawn layer adds **no** process cost and **no** extra mask
>
> The N-well / P-well technology, where n-type diffusion is done over a p-type substrate or p-type diffusion is done over n-type substrate respectively.
>
> The **Twin well technology**, where **NMOS and PMOS transistor** are developed over the wafer by simultaneous diffusion over an epitaxial growth base, rather than a substrate.





## Deep N-well

> Chew, K.W., Zhang, J., Shao, K., Loh, W., & Chu, S.F. (2002). Impact of Deep N-well Implantation on Substrate Noise Coupling and RF Transistor Performance for Systems-on-a-Chip Integration. 32nd European Solid-State Device Research Conference, 251-254. URL:[[slides](http://www.essderc2002.deis.unibo.it/ESSDERC_web/Session_D11/D11_1.pdf), [paper](http://www.essderc2002.deis.unibo.it/data/pdf/Chew.pdf)]
>
> Mark Waller, [Analog layout: Why wells, taps, and guard rings are crucial](https://www.planetanalog.com/analog-layout-why-wells-taps-and-guard-rings-are-crucial/)
>
> KEITH SABINE [Using Deep N Wells in Analog Design](https://www.planetanalog.com/using-deep-n-wells-in-analog-design/)
>
> Faricelli, J. (2010). Layout-dependent proximity effects in deep nanoscale CMOS. IEEE Custom Integrated Circuits Conference 2010, 1-8.
>
> cmos_processing, URL:[http://users.ece.utexas.edu/~athomsen/cmos_processing.pdf](http://users.ece.utexas.edu/~athomsen/cmos_processing.pdf)
>
> Kuo-Tsai LiPaul ChangAndy Chang, TSMC, US20120053923A1, "Methods of designing integrated circuits and systems thereof"



### Substrate noise

A variety of techniques can be used to minimize this noise, for example by keeping analog devices surrounded by guard rings, or using a separate supply for the substrate/well taps. 

However *guard rings alone cannot prevent noise coupling deep in the substrate, only surface currents*.

> PMOS are less noisy than NMOS since PMOS has its nwell which isolates the substrate noise, but such is not valid for NMOS .



### DNW

The N-channel devices built directly into the P-type substrate are not as effectively isolated as P-channel devices in their N-wells. This is because despite creating a P+ guard ring around the devices, there remains an electrical path below the guard ring for charge to flow. 

To overcome this issue, a *deep N-well* can be used to more effectively isolate these N-channel devices.

![image-20230529001556060](dfm-layout/image-20230529001556060.png)

![image-20230529010836003](dfm-layout/image-20230529010836003.png)

![BM_SS_Together at Last_Fig1](dfm-layout/BM_SS_Fig1-520x288.jpg)

> pwdnw: PW/DNW diode
>
> dnwpsub: DNW/PSUB diode
>
> [Together At Last – Combining Netlist and Layout Data for Power-Aware Verification](https://blogs.sw.siemens.com/calibre/2015/11/03/together-at-last-combining-netlist-and-layout-data-for-power-aware-verification/)

![image-20240708221831791](dfm-layout/image-20240708221831791.png)

![image-20240708222327376](dfm-layout/image-20240708222327376.png)



![image-20230529002733114](dfm-layout/image-20230529002733114.png)

- the P-well is separated, allowing the voltage to be controlled
- because the circuit within the deep N-well is separated from the p-substrate in this structure,
  there is the benefit that this circuitry is less susceptible to noise that propagates through the p-substrate.

## Decap

![img](dfm-layout/real-caps.png)

---



![img](dfm-layout/decouple_vbias_comp-1.png)




> Kevin Zheng. The Unsung Heroes – Dummies, Decaps, and More [[https://circuit-artists.com/the-unsung-heroes-dummies-decaps-and-more/](https://circuit-artists.com/the-unsung-heroes-dummies-decaps-and-more/)]
>
> The Difference Between MOM, MIM, and MOS Capacitors [[https://www.ansys.com/blog/difference-between-mom-mim-mos-capacitor](https://www.ansys.com/blog/difference-between-mom-mim-mos-capacitor)]
>
> MIM/MOM capacitor extraction boosts analog and RF designs [[https://www.eeworldonline.com/mim-mom-capacitor-extraction-boosts-analog-and-rf-designs/](https://www.eeworldonline.com/mim-mom-capacitor-extraction-boosts-analog-and-rf-designs/)]



## Metal Resistors In Wire Management



![img](dfm-layout/metresclk.png)

![img](dfm-layout/clk-route-sch.png)



> Kevin Zheng. Metal Resistors – Your Unexpected Friend In Wire Management [[https://circuit-artists.com/metal-resistors-your-unexpected-friend-in-wire-management/](https://circuit-artists.com/metal-resistors-your-unexpected-friend-in-wire-management/)]



## reference

Mikael Sahrling, Layout Techniques for Integrated Circuit Designers 1st Edition , Artech House 2022

LAYOUT, [EE6350 VLSI Design Lab](http://www.ee.columbia.edu/~kinget/EE6350_S16/)  SMART TEMPERATURE SENSOR  URL: [https://www.ee.columbia.edu/~kinget/EE6350_S16/06_TEMPSENS_Sukanya_Vani/layout.html](https://www.ee.columbia.edu/~kinget/EE6350_S16/06_TEMPSENS_Sukanya_Vani/layout.html)

Stacked MOSFETs in analog layout [https://pulsic.com/stacked-mosfets-in-analog-layout/](https://pulsic.com/stacked-mosfets-in-analog-layout/)

JED Hurwitz, ISSCC2011 "T4: Layout: The other half of Nanometer CMOS Analog Design" [[slides](https://www.nishanchettri.com/isscc-slides/2011%20ISSCC/TUTORIALS/ISSCC2011Visuals-T4.pdf), [transcript](https://www.nishanchettri.com/isscc-slides/2011%20ISSCC/TUTORIALS/Transcription_T4.pdf)]

Tom Quan, TSMC, Bob Lefferts, Fred Sendig, Synopsys, Custom Design with FinFETs - Best practices designing mixed-signal IP

Jacob, Ajey & Xie, Ruilong & Sung, Min & Liebmann, Lars & Lee, Rinus & Taylor, Bill. (2017). Scaling Challenges for Advanced CMOS Devices. International Journal of High Speed Electronics and Systems. 26. 1740001. 10.1142/S0129156417400018.

Joddy Wang, Synopsys ["FinFET SPICE Modeling"](https://www.mos-ak.org/washington_dc_2015/presentations/T03_Joddy_Wang_MOS-AK_Washington_DC_2015.pdf)  Modeling of Systems and Parameter Extraction Working Group 8th International MOS-AK Workshop (co-located with the IEDM Conference and CMC Meeting) Washington DC, December 9 2015

A. L. S. Loke et al., "Analog/mixed-signal design challenges in 7-nm CMOS and beyond," 2018 IEEE Custom Integrated Circuits Conference (CICC), San Diego, CA, USA, 2018, pp. 1-8, doi: 10.1109/CICC.2018.8357060.[[slides](https://ewh.ieee.org/r6/san_diego/sscs/events/slides/2018_05_23_AMSDesignChallengesIn7nmCMOS_AlvinLoke.pdf)]

Prof. Adam Teman, Advanced Process Technologies, [[pdf](https://www.eng.biu.ac.il/temanad/files/2022/03/Lecture-2-Advanced-Process-Technologies.pdf)]

Luke Collins. FinFET variability issues challenge advantages of new process [[link](https://www.techdesignforums.com/blog/2014/04/16/finfet-variability-challenges-advantages/)]

Loke, Alvin. (2020). FinFET technology considerations for circuit design (invited short course). BCICTS 2020 Monterey, CA

Alvin Leng Sun Loke, TSMC. Device and Physical Design Considerations for Circuits in FinFET Technology", ISSCC 2020

A. L. S. Loke, C. K. Lee and B. M. Leary, "Nanoscale CMOS Implications on Analog/Mixed-Signal Design," 2019 IEEE Custom Integrated Circuits Conference (CICC), Austin, TX, USA, 2019, pp. 1-57, doi: 10.1109/CICC.2019.8780267.

A. L. S. Loke, Migrating Analog/Mixed-Signal Designs to FinFET Alvin Loke / Qualcomm. 2016 Symposia on VLSI Technology and Circuits

Lattice Semiconductor, 16FFC Process Technology Introduction December 9th, 2021[[pdf](https://cdn.latticesemi-insights.com/wp-content/uploads/2024/01/29174339/HR1000000009.pdf)]
