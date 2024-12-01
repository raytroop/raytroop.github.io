---
title: Circuit insight
date: 2023-01-01 17:50:13
tags:
categories:
- analog
mathjax: true
---



## Gain-boosted cascode

*TODO* &#128197;




## Zero-Value Time Constant Analysis

*TODO* &#128197;



## common gate amplifiers

![No alt text provided for this image](insight/1699196508319.jpeg)



> [[https://www.linkedin.com/posts/chembiyan-t-0b34b910_analog-analogdesign-rfdesign-activity-7126946716938878976-GeW6?utm_source=share&utm_medium=member_desktop](https://www.linkedin.com/posts/chembiyan-t-0b34b910_analog-analogdesign-rfdesign-activity-7126946716938878976-GeW6?utm_source=share&utm_medium=member_desktop)]



## Shot Noise

Any dc **current flowing through a diode** generates the so-called "*shot noise*" due to the random nature of the hole and electron transitions across the **pn junction**



> Shot noise is **not relevant in CMOS devices** since it is only present in bipolar transistors and junction diodes




## Level Shifter

![image-20241003224949171](insight/image-20241003224949171.png)


## TIA

![image-20240824111517140](insight/image-20240824111517140.png)

$$\begin{align}
I_{in} &= \frac{V_i}{R_S} + \frac{V_i - V_o}{R_F} \\
\frac{V_i - V_o}{R_F} &= g_m V_i
\end{align}$$

Then

$$\begin{align}
V_o &= \frac{I_{in}R_F}{\frac{R_S+R_F}{R_S}\frac{1}{1-g_mR_F}- 1} \\
V_i &= \frac{I_{in}R_F}{\frac{R_F}{R_S}+g_mR_F}
\end{align}$$
If $R_S \gg R_F$
$$\begin{align}
V_o &= \frac{I_{in}}{g_m}(1-g_mR_F) \\
V_i &= \frac{I_{in}}{g_m} 
\end{align}$$

### linearity
> TIA stage allows for improved gain with **better linearity**, as mostly signal current passes through $R_F$
*TODO* &#128197;
??? Quantitative analysis





## R-2R & C-2C

*TODO* &#128197;

Conceptually, area goes up *linearly* with number of bit slices

 drawback of the R-2R DAC 



---

$N_b$ bit binary + $N_t$ bit thermometer DAC

![R-2R.drawio](insight/R-2R.drawio.svg)

$N_b$ bit binary can be simplified with Thevenin Equivalent
$$
V_B = \sum_{n=0}^{N_b-1} \frac{B_n}{2^{N_b-n}}
$$
with thermometer code

$$\begin{align}
V_o &= V_B\frac{\frac{2R}{2^{N_t}-1}}{\frac{2R}{2^{N_t}-1}+ 2R}+\sum_{n=0}^{2^{N_t}-2}T_n\frac{\frac{2R}{2^{N_t}-1}}{\frac{2R}{2^{N_t}-1}+ 2R} \\
&= \frac{V_B}{2^{N_t}} + \frac{\sum_{n=0}^{2^{N_t}-2}T_n}{2^{N_t}} \\
&= \sum_{n=0}^{N_b-1} \frac{B_n}{2^{N_t+N_b-n}} + \frac{\sum_{n=0}^{2^{N_t}-2}T_n}{2^{N_t}}
\end{align}$$






> B. Razavi, "The R-2R and C-2C Ladders [A Circuit for All Seasons]," in *IEEE Solid-State Circuits Magazine*, vol. 11, no. 3, pp. 10-15, Summer 2019 [[https://www.seas.ucla.edu/brweb/papers/Journals/BR_SSCM_3_2019.pdf](https://www.seas.ucla.edu/brweb/papers/Journals/BR_SSCM_3_2019.pdf)]


## Switched-Capacitor Resistor

$$
R_{eq} = \frac{1}{f_sC}
$$

![image-20240905202145206](insight/image-20240905202145206.png)



## Channel-Length Modulation & Pinched off

- $\lambda \propto \frac{1}{L_g}$
- $\lambda \propto \frac{1}{V_{DS}}$

![image-20241116080122184](insight/image-20241116080122184.png)

- If $V_{DS}$ is *slightly* greater than $V_{GS} - V_{TH}$, then the *inversion layer* stops at $x \leq L$, and we say the channel is "**pinched off**"
- Upon passing the pinchoff point, the electrons simply shoot through the depletion region near the drain junction and arrive at the drain terminal

> $L^{'}$ is the function of $V_{DS}$

with $\frac{1}{L^{'}} = \frac{1}{L-\Delta L}=\frac{L+\Delta L}{L^2-\Delta L^2}\approx \frac{1}{L}\left(1+\frac{\Delta L}{L}\right)$, we have
$$
I_D \approx \frac{1}{2}\mu_n C_{ox}\frac{W}{L}\left(1+\frac{\Delta L}{L}\right)(V_{GS}-V_{TH})^2 = \frac{1}{2}\mu_n C_{ox}\frac{W}{L}(V_{GS}-V_{TH})^2 (1+\lambda V_{DS})
$$
assuming  $\frac{\Delta L}{L} = \lambda V_{DS}$

> $\lambda$ represents the *relative* variation in length for a given increment in $V_{DS}$. Thus, for longer channels, $\lambda$ is smaller



---

In reality, however, $r_O$ varies with $V_{DS}$. As $V_{DS}$ *increases* and the pinch-off point moves toward the source, the *rate* at which the depletion region around the source becomes wider *decreases*, resulting in a *higher* incremental output impedance.

![image-20241116084353713](insight/image-20241116084353713.png)



## Early Voltage indicator

$$
g_m r_o = \frac{g_m}{I_D}I_D \cdot \frac{V_A}{I_D} =  \frac{g_m}{I_D} \cdot V_A
$$

$g_m r_o $ is the indicator of $V_A$, if $\frac{g_m}{I_D}$ is same



## Resonator

![image-20240826223955851](insight/image-20240826223955851.png)



![image-20240826224132736](insight/image-20240826224132736.png)

![image-20240826224317197](insight/image-20240826224317197.png)

---

![image-20240826224651954](insight/image-20240826224651954.png)

![image-20240826224823886](insight/image-20240826224823886.png)

*bandpass filter*



> Hossein Hashemi, RF Circuits, [[https://youtu.be/0f3yZMvD2Jg?si=2c1Q4y6WJq8Jj8oN](https://youtu.be/0f3yZMvD2Jg?si=2c1Q4y6WJq8Jj8oN)]






## Cgd of Common-Source Stage

Miller effect of Cgd during *layout*





## Nonlinearity of Differential Circuits

![image-20240804173949430](insight/image-20240804173949430.png)

> $$
> \cos^3\omega t = \frac{3\cos \omega t + \cos(3\omega t)}{4}
> $$

> ![image-20240804174042088](insight/image-20240804174042088.png)





## VCO varactor

> Two methods: 1. pss + pac; 2. pss+psp

### PSS + PAC

![image-20220510192206354](insight/image-20220510192206354.png)

pss time domain

![image-20220510192351590](insight/image-20220510192351590.png)

using the **0-harmonic**

![image-20220510192447040](insight/image-20220510192447040.png)

### PSS + PSP

![image-20220510192753324](insight/image-20220510192753324.png)

using **Y11** of `psp`

![image-20220510192639080](insight/image-20220510192639080.png)

### results

![image-20220510193036717](insight/image-20220510193036717.png)

> which are same



## Zero in differential pair with active current mirror

![image-20240629103021286](insight/image-20240629103021286.png)

Noting the circuit consists of a "slow path" (M1, M3, M4) in parallel with a "fast path" (M2)

- "slow path"
  $$
  H_\text{slow}(s) = \frac{A_0}{(1+s/\omega _{pE})(1+s/\omega _{pO})}
  $$

- "fast path"
  $$
  H_\text{fast}(s) = \frac{A_0}{1+s/\omega _{pO}}
  $$

Then
$$\begin{align}
\frac{V_\text{out}}{V_\text{in}} &= H_\text{slow}(s) + H_\text{fast}(s) \\
&= \frac{A_0}{1+s/\omega _{pO}}\left(\frac{1}{1+s/\omega _{pE}} + 1 \right) \\
&= \frac{A_0(1+s/2\omega _{pE})}{(1+s/\omega _{pO})(1+s/\omega _{pE})}
\end{align}$$

That is, the system exhibits a zero at $2\omega_{pE}$

---

signals traveling through *two paths* within an amplifier may cancel each other at one frequency, creating a *zero* in the transfer function

![image-20240629104408168](insight/image-20240629104408168.png)

$$
\omega_z = \frac{(A_1+A_2)\omega_{p1}\omega_{p2}}{A_1\omega_{p1}+A_2\omega_{p2}}
$$
noting $\omega_{p1}\lt \omega_z \lt \omega_{p2}$



## Recognize "Zero" by Inspection

> a method to predict the existence of "zero" by inspection, based on the concept of *"Analog Phase Interpolation"*



*TODO* &#128197;



> Debashis Dhar, How to Recognize "Zero" by Inspection (Utilizing Analog Phase Interpolation) [[https://www.linkedin.com/posts/debashis-dhar-12487024_how-to-recognize-zero-by-inspection-activity-7163364364329160704-9qOq?utm_source=share&utm_medium=member_desktop](https://www.linkedin.com/posts/debashis-dhar-12487024_how-to-recognize-zero-by-inspection-activity-7163364364329160704-9qOq?utm_source=share&utm_medium=member_desktop)]



## Random offset

The dependence of offset voltage and current mismatches upon the overdrive voltage is similar to our
observations for corresponding *noise quantities*

### differential pair

![image-20240624222306837](insight/image-20240624222306837.png)

In reality, since mismatches are independent statistical variables

![image-20240624222417564](insight/image-20240624222417564.png)

> Above shows that the input transistors must be designed for *high gain* ($g_mr_o = \frac{2}{V_{OV}\lambda}$), which means they must be designed for *small* $V_{GS}-V_{TH}$.
>
> It is desirable to minimize $V_{GS}-V_{TH}$ by *lowering the tail current* or *increasing the transistor widths*

---

For $\frac{\Delta K}{K}$

$$\begin{align}
v_{os} g_m &= \Delta K \frac{W}{L}(V_{GS}-V_{TH})^2 \\
v_{os} 2K\frac{W}{L}(V_{GS}-V_{TH}) &= \Delta K \frac{W}{L}(V_{GS}-V_{TH})^2 \\
v_{os} &= \frac{V_{GS}-V_{TH}}{2} \frac{\Delta K}{K}
\end{align}$$

> The derivation for $\frac{\Delta W/L}{W/L}$ is same with $\frac{\Delta K}{K}$


---

**alternative derivation**

$$\begin{align}
\Delta V_\beta \cdot g_m &= \frac{\partial I_D}{\partial \beta} \Delta \beta \\
&= I_D \frac{\Delta \beta}{\beta}
\end{align}$$

That is $\Delta V_\beta = \frac{I_D}{g_m}\frac{\Delta \beta}{\beta}$

$$
\Delta V_R \cdot g_m R = I_D \cdot \Delta R 
$$

That is $\Delta V_R = \frac{I_D}{ g_m} \cdot \frac{\Delta R}{R}$

> [[https://electronicengineering.phd.upc.edu/en/courses-and-seminars/courses-materials/2008-2009/slides-makinwa-1](https://electronicengineering.phd.upc.edu/en/courses-and-seminars/courses-materials/2008-2009/slides-makinwa-1)]

---


### current mirror

![image-20240624224944377](insight/image-20240624224944377.png)

![image-20240624225010443](insight/image-20240624225010443.png)

> To minimize current mismatch, the overdrive voltage must be maximized, a trend opposite to that in differential pair.
>
> This is because as $V_{GS}-V_{TH}$ increases, threshold mismatch has a lesser effect on the device currents
>
> $\Delta I_D= g_m \Delta V_{TH} = \frac{2I_D}{V_{OV}}\Delta V_{TH}$



## Effect of Feedback on Noise

> Feedback does **not improve** the noise performance of circuits.

![image-20240508205903213](insight/image-20240508205903213.png)

>The input-referred noise voltage and current remain the same if the feedback network introduces no noise.



## Burn-in & High-temperature operating life (HTOL) 

- **HTOL**: 
  - characterization test 
  - characterize the life expectancy
- **Burn-in**:
  - production test
  - weed out defective products

> HTOL and Burn-in Testing capture the two ends of the reliability characterization graph known as the "bathtub curve" 

![importance-of-htol-figure-1](insight/importance-of-htol-figure-1.png)

> [[https://arworld.us/the-importance-of-htol-and-burn-in-testing-methods/](https://arworld.us/the-importance-of-htol-and-burn-in-testing-methods/)]



## PERC

- CD: current density checks

- P2P: point to point resistance checks

- LDL: logic driven layout checks, latch up related

- TOPO: topology, circuit connection and device size checks

> database
>
> - CD, P2P, LDL : dfmdb
>
> - TOPO: svdb



> Frank Feng. New Approach For Full Chip Electrical Reliability Verification [[pdf](https://cse.nsysu.edu.tw/app/index.php?Action=downloadfile&file=WVhSMFlXTm9MelV3TDNCMFlWOHhOamN6TnpWZk5qYzFNVGd6TjE4NE5ESXlOQzV3WkdZPQ==&fname=1454FCFGGCPO45YTNOJCJGJGMKPKHC3534FG35YSA1GDXWFC34QOA0OOQOOKZWCDSSPOGDMP20NO4124YWB4B4LKYSMOQL0400YT34PKUWNK20FG00POUSXXYWXWOO15JCLKSWXWDCOKHG2050JCQKHCXTNPNOVSUSB4JCVW20HGJGTTWW40ZXIH5004A4GDMKJG5020OPMOJDLOML51NOFCSWROB454DGKKFCSTGCDCTXNPA4TWRKGDWW30CGKKDGB0YWLKIH05ML44WSFGQOTWOOECYWGHRKCCDD15A4XSFC14FCJGOO25WXROQLNK00JD31PKWSEC50A4SSOKHHTT)]



## STRAP

A "strap" refers to a low-impedance connection

![image-20230518001007350](insight/image-20230518001007350.png)

NWDMY = NWDMY1, NWDMY2



STRAP = NWSTRAP or PWSTRAP

NWSTRAP = {NP & OD} & {NW not {NW INTERACT NWDMY}}

PWSTRAP = {PP & OD} not NW

| cell \ pin  | PLUS    | MINUS   |
| ----------- | ------- | ------- |
| **N diode** | PWSTRAP | \       |
| **P diode** | \       | NWSTRAP |



### Calibre Rule::NOT

![image-20230518005758993](insight/image-20230518005758993.png)



### Calibre Rule::INTERACT

![image-20230518010124496](insight/image-20230518010124496.png)

![image-20230518010758342](insight/image-20230518010758342.png)





## RC charge & discharge

- charge:
  $$
  V_o(t) = V_{X}(1-e^{-\frac{t}{\tau}}) + V_{o,0}\cdot e^{-\frac{-t}{\tau}}
  $$

- discharge:
  $$
  V_o(t) = V_{o,0}\cdot e^{-\frac{t}{\tau}} + V_{o,\infty}\cdot(1-e^{-\frac{t}{\tau}})
  $$

> 1. $e^{-\frac{t}{\tau}}$ item determine the **initial state **
> 2. $(1-e^{-\frac{t}{\tau}})$ item determine the **final state**

![image-20231104231640290](insight/image-20231104231640290.png)

![image-20231104232000036](insight/image-20231104232000036.png)



## AC coupling

$V_m=\frac{1}{4},\space \frac{3}{4}$ and its common voltage $\frac{1}{2}$

$V_o=-\frac{1}{4},\space \frac{1}{4}$ and its common voltage $0$


![image-20231121224940814](insight/image-20231121224940814.png)

![image-20231121225358509](insight/image-20231121225358509.png)



---

$$
\tau = 200 \text{nF} \times (50+50)\text{ohm} = 20 \mu s
$$

high level envelope:

![image-20231121230155083](insight/image-20231121230155083.png)



![image-20231121230225895](insight/image-20231121230225895.png)





## Current mirror with source degeneration 

![image-20231103213308081](insight/image-20231103213308081.png)

![image-20231103213327501](insight/image-20231103213327501.png)

![degeneration](insight/current_mirror_with_res_degeneration.jpg)

> Razavi 2nd, problem 14.15



## Monitored Analog Critical Parameters



![monitor_parameters.drawio](insight/monitor_parameters.drawio.svg)

Parameter Definition:

$$\begin{align}
I_{\text{D,lin}} &= I_D \mid _{V_G=V_{DD},V_D=0.05V} \\
I_{\text{D,sat}} &= I_D \mid _{V_G=V_D=V_{DD}} \\
V_{\text{t,lin}} &= V_G \mid _{I_D=I_{\text{thx}}\cdot \frac{W}{L}@\{V_D=0.05V\}}
\end{align}$$

> $I_{\text{thx}}$ could be different for technologies. (For N16, $I_{\text{thx}}=10$nA)


---

**Constant Current Threshold Voltage**

![Extraction of constant current threshold voltage](insight/ins_ex_vti.png)

**gm-Maximum Method**

![Extraction of threshold voltage](insight/ins_ex_vtgm.png)

> [[Inspect 4. Extracting Standard Parameters](https://kolegite.com/EE_library/books_and_lectures/%D0%90%D0%B2%D1%82%D0%BE%D0%BC%D0%B0%D1%82%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8F%20%D0%BD%D0%B0%20%D0%9F%D1%80%D0%BE%D0%B5%D0%BA%D1%82%D0%B8%D1%80%D0%B0%D0%BD%D0%B5%D1%82%D0%BE%20%D0%B2%20%D0%95%D0%BB%D0%B5%D0%BA%D1%82%D1%80%D0%BE%D0%BD%D0%B8%D0%BA%D0%B0%D1%82%D0%B0/Sentaurus_Training/insp/insp_4.html)]



## STB and PSTB in Spectre/RF

All credits to my colleague, Zhang Wenpian.
> F. Wiedmann, "Loop gain simulation," Online:[[https://sites.google.com/site/frankwiedmann/loopgain](https://sites.google.com/site/frankwiedmann/loopgain)]

### STB analysis

Spectre **stb**'s "loopgain" is negative of "T" in paper<sup>[1]</sup>
$$
T = \frac{2(AD-BC) - A + D}{2(AD-BC)-A+D-1}
$$

AC simulation testbench, shown as below,

![stb_pstb.drawio](insight/stb_pstb.drawio.svg)

1. $I_{inj}$ = 0, $V_{inj}$ = 1

   B = if, D = ve

2. $I_{inj}$ = 1, $V_{inj}$ = 0

   A = if, C = ve

### PSTB analysis

Spectre **pstb** is similar to stb, just set **pac** as **1** instead of  **ac** in current source and voltage source.

This analysis just use **harmonic 0** transfer function in pac analysis, which has limitation.



## Thevenin and Norton Equivalent Circuits

### 戴维南定理

![image-20231021084850078](insight/image-20231021084850078.png)

### 等效电阻的计算方法

![image-20231021085151943](insight/image-20231021085151943.png)

> 使用**外加电源法**时， 全部独立电源需要置零

### 诺顿定理

![image-20231021090448282](insight/image-20231021090448282.png)

#### Lemma of Razavi

$$
A_V = -G_m R_{out}
$$

![image-20231021092407849](insight/image-20231021092407849.png)

> *Design of Analog CMOS Integrated Circuits, Second Edition - Behzad Razavi*





## Miller's Approximation: right-half-plane zero

![image-20231021101204165](insight/image-20231021101204165.png)

 A quick inspection of this circuit reveals that a **zero** lies at a frequency where the current through $C_{12}$ becomes equal to $g_2V_1$. 

When this occurs, the current through the parallel combination of $C_2$ and $R_2$ becomes zero, creating a zero in the transfer function. 

In other words, we can write

$$\begin{align}
g_2V_1 &= V_1sC_{12} \\
s &= \frac{g_2}{C_{12}}
\end{align}$$



## Nonoverlapping clock

**Classical**

![image-20241016212042812](insight/image-20241016212042812.png)



**DWC**

> **C2PHIa** is important to ensure nonoverlapping and DelayA2B is due to level shifter

![image-20241016212100040](insight/image-20241016212100040.png)



## Single ended Amplifier Offset Voltage

### unity gain buffer

![image-20220917115231508](insight/image-20220917115231508.png)

$$\begin{align}
V_o &= V_{o,dc}+A(V_p-V_m) \\
V_o' &= V_{o,dc}+A(V_p+V_{os}-V_m')
\end{align}$$

Then, we get
$$
V_{os}=\frac{V_o'-V_o}{A}+(V_m'-V_m)
$$
Due to $V_o=V_m$ and $V_o'=V_m'$
$$
V_{os}=(1/A+1)\Delta{V_m}
$$
or
$$
V_{os}=(1/A+1)\Delta{V_o}
$$
if $A \gg 1$
$$
V_{os}=\Delta{V_o}
$$


### non-inverting amplifier

![image-20220917115308699](insight/image-20220917115308699.png)
$$\begin{align}
V_o &= V_{o,dc}+A(V_p-V_m) \\
V_o' &= V_{o,dc}+A(V_p+V_{os}-V_m') \\
V_m &= \beta V_o \\
V_m' &= \beta V_o'
\end{align}$$

we get
$$
V_{os}=\frac{V_o'-V_o}{A}+(V_m'-V_m)
$$
or
$$
V_{os}=\frac{\Delta V_o}{A}+\beta \Delta V_o
$$
if $A \gg 1$
$$
V_{os}=\beta \Delta V_o
$$
or
$$
V_{os}=\Delta V_m
$$

---



**Lecture 22 Variability and Mismatch of Dr. Hesham A. Omran's Analog IC Design**

![image-20221022010448797](insight/image-20221022010448797.png)

> URL: [https://www.master-micro.com/professional-courses/analog-ic-design/course-resources](https://www.master-micro.com/professional-courses/analog-ic-design/course-resources)



## Gotcha MOS ron

There is discrepancy between model operating point and $V_{ds}/I_{ds}$

I believe that the equation $V_{ds}/I_{ds}$ is more appropriate where mos is used as switch, though $V_{ds}=0$ is an outlier.

![image-20230104230757729](insight/image-20230104230757729.png)

![image-20230104230837829](insight/image-20230104230837829.png)

![image-20230104230851475](insight/image-20230104230851475.png)



## Schmitt Inverter

![image-20231021232912529](insight/image-20231021232912529.png)





## gm/ID Intuition



![image-20230103220933081](insight/image-20230103220933081.png)

> small gm/ID for High ro,  or high Early voltage $V_A$



## Transit Frequency $f_T$

Defined as the frequency at which the **small-signal current gain** of a device is **unity**

![image-20231213234524075](insight/image-20231213234524075.png)

---

![image-20240116233951006](insight/image-20240116233951006.png)





## MOSFET ZTC Condition Analysis

>  zero temperature coefficient (ZTC)

![image-20231212195536754](insight/image-20231212195536754.png)





## MOM cap of wo_mx

Monte Carlo model:

- $C_{pa}=C_{pa1}$, $C_{pb}=C_{pb1}$ for each iteration during *Process Variation*
- different variation is applied to $C_{ab}$ and $C_{a1b1}$ each iteration during *Mismatch Variation*, though $C_{pa}$, $C_{pb}$, $C_{pa1}$ and $C_{pb1}$ remain constant

![image-20230220230434891](insight/image-20230220230434891.png)

![image-20230220230331505](insight/image-20230220230331505.png)



## Active Inductor

![activeInd](insight/activeInd.svg)

$$\begin{align}
A &= \frac{g_mR_L}{1+(g_\text{m\_dio}+ g_\text{ds\_tot})R_L}\cdot \frac{1+R_pC_Ps}{1+\frac{(1+g_\text{ds\_tot}R_L)R_PC_P+C_PR_L+R_LC_L}{1+(g_\text{m\_dio}+g_\text{ds\_tot})R_L}s + \frac{R_LC_LR_PC_P}{1+(g_\text{m\_dio}+g_\text{ds\_tot})R_L}s^2} \\
&= \frac{g_mR_L}{1+(g_\text{m\_dio}+ g_\text{ds\_tot})R_L}\cdot \frac{R_PC_P}{ \frac{R_LC_LR_PC_P}{1+(g_\text{m\_dio}+g_\text{ds\_tot})R_L}}\cdot \frac{1/(R_PC_P)+s}{s^2 + \frac{(1+g_\text{ds\_tot}R_L)R_PC_P+C_PR_L+R_LC_L}{R_PC_P}s + \frac{1+(g_\text{m\_dio}+g_\text{ds\_tot})R_L}{R_LC_LR_PC_P}} \\
&= A_0 \cdot A(s)
\end{align}$$

That is

$$\begin{align}
\omega_z &= \frac{1}{R_PC_P} \tag{1} \\ 
\omega_n &= \sqrt{\frac{1+(g_\text{m\_dio}+g_\text{ds\_tot})R_L}{R_LC_LR_PC_P}} = \sqrt{\omega_{p0}\omega_z} \\
\zeta & = \frac{(1+g_\text{ds\_tot}R_L)R_PC_P+C_PR_L+R_LC_L}{R_PC_P} \frac{1}{2 \omega_n}
\end{align}$$

Where
$$\begin{align}
\omega_{p0} &= \frac{1}{(R_L||\frac{1}{g_\text{m\_dio}}||\frac{1}{g_\text{ds\_tot}})C_L}  \tag{2}
\end{align}$$

Here, relate $\omega_{p0}$ and $\omega_z$ by coefficient $\alpha$
$$
\omega_{p0} = \alpha \cdot  \omega_z \tag{3}
$$
This way
$$
\omega_n= \sqrt{\alpha}\cdot \omega_z
$$

$$
\zeta = \frac{1}{2}(K\sqrt{\alpha}+\frac{1+C_P/C_L}{\sqrt{\alpha}}) \tag{4}
$$
where
$$
K = \frac{R_L||\frac{1}{g_\text{m\_dio}}||\frac{1}{g_\text{ds\_tot}}}{R_L||g_\text{ds\_tot}} 
$$




And $A(s)$ can be expressed as
$$
A(s) = \frac{\frac{s}{\omega_z}+1}{\frac{s^2}{\omega_n^2}+2\frac{\zeta}{\omega_n}s+1}
$$
It magnitude in dB
$$
A_\text{dB} = 10\log\frac{1+(\omega/\omega_z)^2}{1+(\omega/\omega_n)^4+2\omega^2(2\zeta^2-1)/\omega_n^2}
$$
Substitute $\omega_n$ with Eq (2), followed is obtained
$$
A_\text{dB} = 10\log{\frac{\alpha^2(\omega_z^4 + \omega_z^2\omega^2)}{\alpha^2\omega_z^4+\omega^4+2\alpha\omega_z^2(2\zeta^2-1)\omega^2}}
$$
peaking frequency
$$
\omega_\text{peak} = \omega_z\cdot \sqrt{\sqrt{(\alpha+1)^2 - 4\alpha \zeta^2}-1}
$$
If $\zeta=1$
$$\begin{align}
\omega_{A_\text{dB = 0dB} }&= \sqrt{1-2/\alpha}\cdot \omega_{p0} \\
\omega_\text{peak} &= \omega_z\sqrt{\alpha-2} \\
A_\text{dB,peak} &= 10\log\frac{\alpha^2}{4(\alpha-1)}
\end{align}$$





## Miller multiplication of Capacitor

### Positive Cap 

![image-20231220225508580](insight/image-20231220225508580.png)

![image-20231220225450481](insight/image-20231220225450481.png)



### Negative Cap

 ![image-20231220225910283](insight/image-20231220225910283.png)

![image-20231220230015868](insight/image-20231220230015868.png)

---

gain has **limited** bandwidth

![image-20231224212914366](insight/image-20231224212914366.png)

![image-20231224212541383](insight/image-20231224212541383.png)

![image-20231224212625409](insight/image-20231224212625409.png)

$V_o = V_i |A|e^{j\theta}$, and $A_r = |A|\cos\theta$, $A_i = |A|\sin\theta$

Then $I_i = (V_i - V_o)sC_f= V_i(1-|A|e^{j\theta})sC_f$, impedance is shown as below

$$\begin{align}
Z &= \frac{V_i}{I_i} \\
&= \frac{1}{(1-|A|e^{j\theta})j\omega C_f} \\
&= -\frac{j}{\omega C_f\frac{1+|A|^2-2|A|\cos\theta}{1-|A|\cos\theta}} + \frac{|A|\sin\theta}{\omega C_f (1+|A|^2-2|A|\cos\theta)} \\
\end{align}$$

$C_\text{eq}$ and $R_\text{eq}$ are obtained
$$\begin{align}
C_\text{eq} &= \frac{1+|A|^2-2A_r}{1-A_r}\cdot C_f \\
R_\text{eq} &= \frac{A_i}{1+|A|^2-2A_r}\cdot \frac{1}{\omega C_f}
\end{align}$$





## D/S small signal model

![image-20240106161059584](insight/image-20240106161059584.png)

> The `Drain` and `Source` of MOS are determined in *DC operating point*, i.e. large signal. 

That is, top of $M_2$ is `drain` and bottom is `source`,
$$\begin{align}
R_\text{eq2} &= \frac{r_\text{o2}+R_L}{1+g_\text{m2}r_\text{o2}} \\
& \simeq  \frac{1}{g_\text{m2}}
\end{align}$$



## PMOS small signal model polarity

> The small-signal models of NMOS and PMOS transistors are **identical**

A negative $\Delta V_\text{GS}$ leads to a negative $\Delta I_D$. 

> Recall that $I_D$, in the direction shown here, is negative because the actual current of holes flows from the source to the drain.
>
> 
>
> ![image-20240106170315177](insight/image-20240106170315177.png)

Conversely, a positive $\Delta V_\text{GS}$ produces a positive $\Delta I_D$, as is the case for an NMOS device.

![image-20240106164923917](insight/image-20240106164923917.png)





## Leakage in MOS

![image-20241109195527005](insight/image-20241109195527005.png)

- Subthreshold leakage
  - Drain-Induced Barrier Lowering (**DIBL**)
- Reverse-bias Source/Drain junction leakages
- Gate leakage
- two other leakage mechanisms
  - Gate Induced Drain Leakage (**GIDL**)
  - Punchthrough



![image-20241110001311117](insight/image-20241110001311117.png)

> W. M. Elgharbawy and M. A. Bayoumi, "Leakage sources and possible solutions in nanometer CMOS technologies," in IEEE Circuits and Systems Magazine, vol. 5, no. 4, pp. 6-17, Fourth Quarter 2005, doi: 10.1109/MCAS.2005.1550165.
>
> X. Qi et al., "Efficient subthreshold leakage current optimization - Leakage current optimization and layout migration for 90- and 65- nm ASIC libraries," in IEEE Circuits and Devices Magazine, vol. 22, no. 5, pp. 39-47, Sept.-Oct. 2006, doi: 10.1109/MCD.2006.272999.
>
> P. Monsurró, S. Pennisi, G. Scotti and A. Trifiletti, "Exploiting the Body of MOS Devices for High Performance Analog Design," in IEEE Circuits and Systems Magazine, vol. 11, no. 4, pp. 8-23, Fourthquarter 2011, doi: 10.1109/MCAS.2011.942751.
>
> Andrea Baschirotto, ISSCC2015 "ADC Design in Scaled Technologies"
>
> Joachim Assenmacher Infineon Technologies, "BSIM4 Modeling and Parameter Extraction" [[https://ewh.ieee.org/r5/denver/sscs/References/2003_03_Assenmacher.pdf](https://ewh.ieee.org/r5/denver/sscs/References/2003_03_Assenmacher.pdf)]
>
> Stefan Rusu, Intel ISSCC 2008 Tutorial: "Leakage Reduction Techniques" [[https://www.nishanchettri.com/isscc-slides/2008%20ISSCC/Tutorials/T06_Pres.pdf](https://www.nishanchettri.com/isscc-slides/2008%20ISSCC/Tutorials/T06_Pres.pdf)]



### Drain-Induced Barrier Lowering (DIBL)

As a result of DIBL, **threshold voltage is reduced** with shorter channel lengths and, consequently, the subthreshold leakage current is increased

![image-20240901231532412](insight/image-20240901231532412.png)

***impact on output impedance***

The principal impact of DIBL on circuit design is the degraded output impedance.

> In short-channel devices, as $V_{DS}$ increases further, drain-induced barrier lowering becomes significant, *reducing the threshold voltage* and increasing the drain current

![image-20240901232709711](insight/image-20240901232709711.png)

> Impact Ionization and GIDL are *different*, however both *increase* drain current, which flowing from the drain into the substrate



![image-20241120210915254](insight/image-20241120210915254.png)



### Gate induced drain leakage (GIDL)

![image-20241110001118250](insight/image-20241110001118250.png)

![Figure 4.3](insight/3-s2.0-B9780323856775000081-f04-03-9780323856775.jpg)

 The large current flows from the *drain to bulk* and  this drain leakage current is named **gate-induced drain leakage (GIDL)** since it is due to *a gate-induced high electric field present in the gate-to-drain overlap region*

> gate-induced drain leakage (GIDL) increases exponentially due to the reduced gate oxide thickness



![image-20240902000820459](insight/image-20240902000820459.png)



> Chauhan, Yogesh Singh, et al. *FinFET modeling for IC simulation and design: using the BSIM-CMG standard*. Academic Press, 2015.

---



![image-20240901225754731](insight/image-20240901225754731.png)


$$
\frac{g_m}{I_D} = \frac{2}{V_{GS}-V_{TH}}
$$
Decrease of gm/Id results from decrease in VT.  

GIDL (**Gate induced drain leakage**) as at weak inversion may results in a weak lateral electric field causing leakage current between drain and bulk, which degrade the efficiency of the transistor (gm/ID).



> [[https://www.linkedin.com/posts/master-micro_mastermicro-mastermicro-adt-activity-7214549962833989632-ZoV_?utm_source=share&utm_medium=member_desktop](https://www.linkedin.com/posts/master-micro_mastermicro-mastermicro-adt-activity-7214549962833989632-ZoV_?utm_source=share&utm_medium=member_desktop)]



### Voltage Dependence

![image-20241111224955193](insight/image-20241111224955193.png)

### Temperature Dependence

![image-20241111225025277](insight/image-20241111225025277.png)

---

In advanced node, gate leakage is also a strong function of temperature

![image-20241111230519009](insight/image-20241111230519009.png)


## signal detection circuit



![sc_sigdet.drawio](insight/sc_sigdet.drawio.svg)

**phase I**

$$\begin{align}
Q_a &= (V_{a0} - 0.5*(V_{ip} + V_{im}))*C + (V_{a0} - V_{th})*C \\
Q_b &= (V_{b0} - 0.5*(V_{ip} + V_{im}))*C + V_{b0}*C
\end{align}$$



**Phase II**

$$\begin{align}
Q_a &= (V_{a} - V_{ip})*C + (V_{a} - V_{b})*0.5C \\
Q_b &= (V_{b} - V_{im})*C + (V_{b} - V_{a})*0.5C
\end{align}$$



**With the law of charge conservation, we get**

$$\begin{equation}
V_a - V_b = (V_{a0} - V_{b0}) + 0.5*(V_{ip} - V_{im} - V_{th})
\end{equation}$$



> REF: D. A. Yokoyama-Martin et al., "A Multi-Standard Low Power 1.5-3.125 Gb/s Serial Transceiver in 90nm CMOS," IEEE Custom Integrated Circuits Conference 2006, 2006, pp. 401-404, doi: 10.1109/CICC.2006.320970.



## Power/Ground and I/O Pins

### Power / Ground Pin Information

In both digital and analog I/O, power and ground pins appear at the sub-circuit definiton, allowing user to use the I/O in voltage islands. They follow certain naming conventions.

1. digital I/O sub-circuit

- VDD: pre-driver core voltage (supplied by PVDD1CDGM)
- VSS: pre-driver ground and also global ground (supplied by PVDD1CDGM)
- VDDPST: I/O post-driver voltage, i.e. 1.8V (supplied by PVDD2CDGM or PVDD2POCM)
- VSSPOST: I/O post-driver ground (supplied by PVDD2CDGM or PVDD2POCM)
- POCCTRL: POCCTRL signal (supplied by PVDD2POCM)

2. analog I/O placed in a core voltage domain, the convention is

- TACVDD: analog core voltage (supplied by PVDD3ACM)
- TACVSS: analog core ground (supplied by PVDD3ACM)
- VSS: global core ground

3. analog I/O placed in an I/O voltage domain, the convention is:

- TAVDD: analog I/O voltage, i.e. 1.8V (supplied by PVDD3AM)
- TAVSS: analog I/O ground (supplied by PVDD3AM)
- VSS: global core ground

Power/Ground **Combo Cells**

| power/ground combo pad cell | pins to be connected to bump | to core side pin name |
| --------------------------- | ---------------------------- | --------------------- |
| PVDD1CDGM                   | VDD VSS                      | VDD VSS               |
| PVDD2CDGM PVDD2POCM         | VDDPST VSSPST                | N/A                   |
| PVDD3AM                     | TAVDD TAVSS                  | AVDD AVSS             |
| PVDD3ACM                    | TACVDD TACVSS                | AVDD AVSS             |

### Note for the retention mode

1. At initial state, IRTE must be **0** when VDD is off.
2. IRTE must be kept >= 10us after VDD turns on again (from the retention mode to the normal operation mode).
3. IRTE can be switched only when both VDD and VDDPST are on.

![rention_seq.drawio](insight/rention_seq.drawio.svg)

When the rention function is needed, IRTE signal must come from an "always-on" core power domain. If you don't need the rention function, it is required to tie IRTE to ground. In other words, **no matter the rention feature is needed or not, it is required to have PCBRTE in each domain**.

![PCBRTE_in_digital_domain.drawio](insight/PCBRTE_in_digital_domain.drawio.svg)

**Note**: PCBRTE **does not** need PAD connection.

### Internal Pins

There are 3 internal global pins, i.e. **ESD**, **POCCTRL**, **RTE**, in all digital domain cells. 

In real application, 

- **ESD pin** is an internal signal and **active** in ESD event happening
- **POCCTRL** is an internal signal and active in Power-on-control event.

However, these special events (i.e. ESD event and Power-on-control event) are not modeled in NLDM kit (.lib), only normal function is covered, so **ESD** and **POCCTRL** pins are simply defined as ground in NLDM kit (.lib).

> These 3 global pins will be connected automatically after **cell-to-cell abutting** in physical layout.

### Power-Up sequence in Digital Domain

Power up the I/O power (VDDPST) first, then the core power (VDD)

![pocctrl_seq.drawio](insight/pocctrl_seq.drawio.svg)

1. PVDDD2POCM cell would generate Power-On-Control signal (POCCTRL) to have the post-driver NMOS and PMOS off, so that the crowbar current would not occur in the post-driver fingers when the I/O voltage is on while the core voltage remains off. As such, I/O cell would be in the Hi-Z state. when POCCTRL is on, the pll-up/down resistor is disabled and C is 0.
2. The POCCTRL signal is transmitted to I/O cells through **cell abutment**. There is no need to have routing for POCCTTRL nor give a control signal to the POCCTRL pin any of I/O cells. Note that the POCCTRL signal would be cut if inserting a power-cut (PRCUT)  cell.

![power-on-control-ciruit.drawio](insight/power-on-control-ciruit.drawio.svg)

### Power-Down sequence in Digital Domain

It's the reverse of power-up sequence.

### Use model in Innovus

```tcl
set init_gnd_net "vss_core vss DUMMY_ESD DUMMY_POCCTRL"

addInst -moduleBased u_io -ori R270 -physical -status fixed -loc 135 994 -inst u_io/VDDIO_1 -cell PVDD2CDGM_H

addNet u_io_RTE
attachTerm FILLER_6 RTE u_io_RTE
attachTerm VDDIO_1 RTE u_right_RTE
setAttribute -skip_routing true -net u_io_RTE

clearGlobalNets
globalNetConnect DUMMY_POCCTRL -type pgpin -pin POCCTRL -singleInstance u_io/VDDDIO_1 -override
globalNetConnect DUMMY_ESD -type pgpin -pin ESD -singleInstance u_io/VDDDIO_1 -override
```

```tcl
set pins [get_object_name [get_ports *]]
foreach pin $pins {
	set netPtr [dbGetNetByName $pin]
	if { $netPtr == "0x0" } {
		puts "INFO: can't find the port: $pin"
	} else {
		setAttribute -net $pin -skip_routing true
	}
}

foreach net [get_object_name [get_nets -of_objects [get_pins */RTE -hierarchical]]] {
	setAttribute -net $net -skip_routing true
	dbSet [dbGetNetByName $net].dontTouch true
}
```



## Antenna Effect

The **antenna effect** is a common name for the effects of *charge accumulation* in *isolated nodes* of an integrated circuit *during its processing*.

> This effect is also sometimes called "Plasma Induced Damage", "Process Induced Damage" (PID) or "charging effect".



### antenna ratio

The antenna rule specifies the maximum tolerance for the ratio of a metal line area to the area of connected gates.


### metal jumping

Long metal can be taken to *higher metal* routing layer. This is known as **metal jumping**. 

> This metal jumping will break the long interconnect and hence the charge collected on the long interconnect will not discharge through gate oxide because the higher metal layer is not yet fabricated. 

> so, if the gate immediately connects to the highest level by jump-up metals, large amount of charges can not be collected, while the poly finally connected to the diffusion part by highest level, thus no antenna violation will normally occure.

### Diode Insertion

Diode helps dissipate charges accumulated on metal. Diode should be placed as near as possible to the gate of device on low level of metal.

> Diode should always be connected in *reverse bias*, with cathode connected to gate electrode and anode connected to ground potential.
>
> During processing, even if the diodes are reversely biased, because of the elevated wafer temperature (200 o C plus) it will provide a much conductive path
>
> In the reverse bias region, the reverse saturation current of Si and Ge diodes doubles for every 10° C rise in temperature

![main-qimg-c3fe57dfac5fd5e5b5616ddf4f89f08a-pjlq](insight/main-qimg-c3fe57dfac5fd5e5b5616ddf4f89f08a-pjlq.jpg)

> Tuvia Liran, Antenna effect (PID): Do the design rules really protect us? [[link](https://www.eetimes.com/antenna-effect-do-the-design-rules-really-protect-us/)]
>
> Upma Pawan Kumar, Sunandan Chaubey, Antenna Effect in 16nm Technology Node [[link](https://www.design-reuse.com/articles/48227/antenna-effect-in-16nm-technology-node.html)]
>
> pulsic.com, Analog layout – Stop the antenna effect from destroying your circuit [[link](https://pulsic.com/analog-layout-stop-the-antenna-effect-from-destroying-your-circuit/)]
>
> BuBuChen, 積體電路的天線效應 (Antenna Effect in IC) [[link](https://www.bubuchen.com/2020/04/Antenna-Effect.html)]
>
> EDN, Antenna violations resolved using new method [[link](https://www.edn.com/antenna-violations-resolved-using-new-method/)]
>
> edaboard.com, why jump up metal can solve the antenna effect? [[link](https://www.edaboard.com/threads/why-jump-up-metal-can-solve-the-antenna-effect.177890/post-745696)]
>
> siliconvlsi.com, Antenna effect [[link](https://siliconvlsi.com/antenna-effect/)]
>
> Prof. Adam Teman, Digital VLSI Design. Lecture-10-The-Manufacturing-Process [[pdf](https://www.eng.biu.ac.il/temanad/files/2017/02/Lecture-10-The-Manufacturing-Process.pdf)]
>
>
> Zongjian Chen, Processing and Reliability Issues That Impact Design Practice. [[https://web.stanford.edu/class/archive/ee/ee371/ee371.1066/lectures/Old/lect_15_2up.pdf](https://web.stanford.edu/class/archive/ee/ee371/ee371.1066/lectures/Old/lect_15_2up.pdf)]



## Metastability & Synchronizer

> *Clock Domain Crossing (CDC)*

When a flip-flop samples an input that is changing during its aperture, the output Q may momentarily take on a voltage between 0 and VDD that is in the forbidden zone. This is called a metastable state. Eventually, the flip-flop will resolve the output to a stable state of either 0 or 1. However, the resolution time required to reach the stable state is *unbounded*



![image-20240803075025846](insight/image-20240803075025846.png)





### Mean Time Between Failure (MTBF)

*TODO* &#128197;







> Steve Golson. Synchronization and Metastability [[https://trilobyte.com/pdf/golson_snug14.pdf](https://trilobyte.com/pdf/golson_snug14.pdf)]
>
> R. Ginosar, "Metastability and Synchronizers: A Tutorial," in IEEE Design & Test of Computers, vol. 28, no. 5, pp. 23-35, Sept.-Oct. 2011, doi: 10.1109/MDT.2011.113. [[https://webee.technion.ac.il/~ran/papers/Metastability-and-Synchronizers.IEEEDToct2011.pdf](https://webee.technion.ac.il/~ran/papers/Metastability-and-Synchronizers.IEEEDToct2011.pdf)]
>
> Kinniment, D. J. Synchronization and arbitration in digital systems. John Wiley & Sons Ltd (2007).
>
> Amr Adel Mohammady, Clock Domain Crossing. [[https://media.licdn.com/dms/document/media/D4E1FAQFGmDwVxj-A3Q/feedshare-document-pdf-analyzed/0/1727431256521?e=1728518400&v=beta&t=aY8BaqSPrHuQCesh_1hEPs-wYHQAF9XMI4eRfMij7zI](https://media.licdn.com/dms/document/media/D4E1FAQFGmDwVxj-A3Q/feedshare-document-pdf-analyzed/0/1727431256521?e=1728518400&v=beta&t=aY8BaqSPrHuQCesh_1hEPs-wYHQAF9XMI4eRfMij7zI)]



## Slewing of Folded-Cascode Op Amps



![image-20240817161915989](insight/image-20240817161915989.png)

> In practice, we choose $I_P \simeq I_{SS}$

---

![image-20240817162418938](insight/image-20240817162418938.png)

![image-20240817162127452](insight/image-20240817162127452.png)



---

![image-20240816175038971](insight/image-20240816175038971.png)

Avoid *zero current* in cascodes

- left circuit

  $I_b \gt I_a$

- right circuit

  $I_b \gt 2I_a$



## Step Response of higher order system

![image-20240112002314153](insight/image-20240112002314153.png)

Since $1/sC_1+R_1 \gg R_0$
$$
\frac{V_m}{V_i}(s) \simeq \frac{R_0}{R_0 + 1/sC_0} = \frac{sR_0C_0}{1+sR_0C_0}
$$
*step response* of $V_m$
$$
V_m(t) = e^{-t/R_0C_0}
$$
where $\tau = R_0C_0$



And $V_o(s)$ can be expressed as
$$\begin{align}
\frac{V_o}{V_i}(s)  & \simeq \frac{sR_0C_0}{1+sR_0C_0} \cdot \frac{sR_1C_1}{1+sR_1C_1} \\
&= \frac{sR_0C_0R_1C_1}{R_0C_0-R_1C_1}\left(\frac{1}{1+sR_1C_1} - \frac{1}{1+sR_0C_0}\right)
\end{align}$$

Then *step response* of $Vo$
$$\begin{align}
Vo(t) &= \frac{R_0C_0R_1C_1}{R_0C_0-R_1C_1} \left(\frac{1}{R_1C_1}e^{-t/R_1C_1} - \frac{1}{R_0C_0}e^{-t/R_0C_0}\right) \\
&= \frac{1}{R_0C_0-R_1C_1}\left(R_0C_0e^{-t/R_1C_1} - R_1C_1e^{-t/R_0C_0}\right) \\
&\simeq = \frac{1}{R_0C_0-R_1C_1}\left(R_0C_0e^{-t/R_1C_1} - R_1C_1\right)
\end{align}$$

where $\tau=R_1C_1$



### Partial-fraction Expansion

```matlab
syms C0
syms R0
syms C1
syms R1
syms s

Z0 = 1/s/C1 + R1;
Z1 = R0*Z0/(R0+Z0);
vm = Z1 / (Z1 + 1/s/C0);
vo = R1/Z0 * vm;
```

```matlab
>> partfrac(vm, s)
 
ans =
 
1 - (s*(C1*R0 + C1*R1) + 1)/(C0*C1*R0*R1*s^2 + (C0*R0 + C1*R0 + C1*R1)*s + 1)
 
>> partfrac(vo, s)
 
ans =
 
1 - (s*(C0*R0 + C1*R0 + C1*R1) + 1)/(C0*C1*R0*R1*s^2 + (C0*R0 + C1*R0 + C1*R1)*s + 1)
```

$$\begin{align}
V_m(s) &= 1 - \frac{s(C_1R_0+C_1R_1)+1}{C_0C_1R_0R_1s^2+(C_0R_0+C_1R_0+C_1R_1)s+1} \\
V_o(s) &= 1 - \frac{s(C_0R_0+C_1R_0+C_1R_1)+1}{C_0C_1R_0R_1s^2+(C_0R_0+C_1R_0+C_1R_1)s+1}
\end{align}$$



```matlab
C0 = 200e-9;
R0 = 50;
C1 = 400e-15;
R1 = 200e3;

s = tf("s");

Z0 = 1/s/C1 + R1;
Z1 = R0*Z0/(R0+Z0);
vm = Z1 / (Z1 + 1/s/C0);
vo = R1/Z0 * vm;

vm_exp = 1 - (s*(C1*R0 + C1*R1) + 1)/(C0*C1*R0*R1*s^2 + (C0*R0 + C1*R0 + C1*R1)*s + 1);
vo_exp = 1 - (s*(C0*R0 + C1*R0 + C1*R1) + 1)/(C0*C1*R0*R1*s^2 + (C0*R0 + C1*R0 + C1*R1)*s + 1);

figure(1)
subplot(1,2,1)
step(vm, 500e-9, 'k-o');
hold on;
step(vm_exp, 500e-9, 'r-^')
title('vm step response')
grid on;
legend()


subplot(1,2,2)
step(vo, 500e-9, 'k-o');
hold on;
step(vo_exp, 500e-9, 'r-^')
title('vo step response')
grid on;
legend()


% with approximation
figure(2)
vm_exp2 = s*R0*C0/(1+s*R0*C0);
vo_exp2 = s*R0*C0/(1+s*R0*C0) * s*R1*C1/(1+s*R1*C1);

subplot(1,2,1)
step(vm, 500e-9, 'k-o');
hold on;
step(vm_exp2, 500e-9, 'r-^')
title('vm step response')
grid on;
legend()

subplot(1,2,2)
step(vo, 500e-9, 'k-o');
hold on;
step(vo_exp2, 500e-9, 'r-^')
title('vo step response')
grid on;
legend()
```

![image-20240113181003272](insight/image-20240113181003272.png)

![image-20240113181032379](insight/image-20240113181032379.png)



---

spectre simulation vs matlab


```matlab
C0 = 200e-9;
R0 = 50;
C1 = 400e-15;
R1 = 200e3;

s = tf("s");

Z0 = 1/s/C1 + R1;
Z1 = R0*Z0/(R0+Z0);
vm = Z1 / (Z1 + 1/s/C0);
vo = R1/Z0 * vm;

step(vm, 500e-9);
hold on;
step(vo, 500e-9);

grid on
```

```matlab
>> vm

vm =
 
          1.024e-44 s^5 + 2.56e-37 s^4 + 1.6e-30 s^3
  -----------------------------------------------------------
  1.024e-44 s^5 + 2.571e-37 s^4 + 1.626e-30 s^3 + 1.6e-25 s^2
 
Continuous-time transfer function.

>> vo

vo =
 
                 8.194e-52 s^6 + 2.048e-44 s^5 + 1.28e-37 s^4
  ---------------------------------------------------------------------------
  8.194e-52 s^6 + 3.081e-44 s^5 + 3.871e-37 s^4 + 1.638e-30 s^3 + 1.6e-25 s^2
 
Continuous-time transfer function.
```



![image-20240112002155622](insight/image-20240112002155622.png)





## reference

M. Tian, V. Visvanathan, J. Hantgan and K. Kundert, "Striving for small-signal stability," in IEEE Circuits and Devices Magazine, vol. 17, no. 1, pp. 31-41, Jan. 2001, doi: 10.1109/101.900125.

Open loop gain analysis and "STB" method  [[https://www.linkedin.com/pulse/open-loop-gain-analysis-stb-method-jean-francois-debroux](https://www.linkedin.com/pulse/open-loop-gain-analysis-stb-method-jean-francois-debroux )]

The Analog Designer's Toolbox (ADT) | Invited Talk by IEEE Santa Clara Valley Section CAS Society, [https://youtu.be/FT6kKC5OdE0](https://youtu.be/FT6kKC5OdE0)

ESSCIRC2023 Circuit Insights Ali Sheikholeslami [[https://youtu.be/2xFIZM5_FPw?si=XWwSzDgKWZGB0rX1](https://youtu.be/2xFIZM5_FPw?si=XWwSzDgKWZGB0rX1)]

Ali Sheikholeslami, Circuit Intuitions: Thevenin and Norton Equivalent Circuits, Part 3 IEEE Solid-State Circuits Magazine, Vol. 10, Issue 4, pp. 7-8, Fall 2018. 

—, Circuit Intuitions: Thevenin and Norton Equivalent Circuits, Part 2 IEEE Solid-State Circuits Magazine, Vol. 10, Issue 3, pp. 7-8, Summer 2018. 

—, Circuit Intuitions: Thevenin and Norton Equivalent Circuits, Part 1 IEEE Solid-State Circuits Magazine, Vol. 10, Issue 2, pp. 7-8, Spring 2018.

—, Circuit Intuitions: Miller's Approximation IEEE Solid-State Circuits Magazine, Vol. 7, Issue 4, pp. 7-8, Fall 2015. 

—, Circuit Intuitions: Miller's Theorem IEEE Solid-State Circuits Magazine, Vol. 7, Issue 3, pp. 8-10, Summer 2015.

Shanthi Pavan, "Demystifying Linear Time Varying Circuits"

ecircuitcenter. Switched-Capacitor Resistor [[http://www.ecircuitcenter.com/Circuits/SWCap/SWCap.htm](http://www.ecircuitcenter.com/Circuits/SWCap/SWCap.htm)]

Jørgen Andreas Michaelsen. INF4420 Switched-Capacitor Circuits. [[https://www.uio.no/studier/emner/matnat/ifi/INF4420/v13/undervisningsmateriale/inf4420_v13_07_switchedcapacitor_print.pdf](https://www.uio.no/studier/emner/matnat/ifi/INF4420/v13/undervisningsmateriale/inf4420_v13_07_switchedcapacitor_print.pdf)]

chembiyan T. OC Lecture 10: A very basic introduction to switched capacitor circuits [[https://youtu.be/SaYtemYp4rQ?si=q2qovTKJrLy65pnu](https://youtu.be/SaYtemYp4rQ?si=q2qovTKJrLy65pnu)

Robert Bogdan Staszewski, Poras T. Balsara. "All‐Digital Frequency Synthesizer in Deep‐Submicron CMOS"

Mayank Parasrampuria, Sandeep Jain, Burn-in 101 [[link](https://www.edn.com/burn-in-101/)]
