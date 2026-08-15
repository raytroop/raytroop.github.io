---
title: Charge Pump PLL
date: 2025-06-01 08:57:16
tags:
categories:
- link
mathjax: true
---

![image-20260613070841886](cp-pll/image-20260613070841886.png)

> Mehmet Soyuer. *Monolithic Phase-Locked Loops for Clocking* [[https://ewh.ieee.org/r5/denver/sscs/Presentations/2009_06_Soyuer.pdf](https://ewh.ieee.org/r5/denver/sscs/Presentations/2009_06_Soyuer.pdf)]

![image-20260808093448775](cp-pll/image-20260808093448775.png)

## PD & PFD

> Sam Palermo, ECEN620: Network Theory Broadband Circuit Design Fall 2025 Lecture 4: Phase Detector Circuits [[https://people.engr.tamu.edu/spalermo/ecen620/lecture04_ee620_phase_detectors.pdf](https://people.engr.tamu.edu/spalermo/ecen620/lecture04_ee620_phase_detectors.pdf)]
>
> Michael Perrott, 6.976 High Speed Communication Circuits and Systems *Lecture 15 Integer-N Frequency Synthesizers* [[https://rfic.eecs.berkeley.edu/courses/ee242/pdf/perrott_lec15.pdf](https://rfic.eecs.berkeley.edu/courses/ee242/pdf/perrott_lec15.pdf)]
>
> Mehmet Soyuer. *Monolithic Phase-Locked Loops for Clocking* [[https://ewh.ieee.org/r5/denver/sscs/Presentations/2009_06_Soyuer.pdf](https://ewh.ieee.org/r5/denver/sscs/Presentations/2009_06_Soyuer.pdf)]
>
> Qasim Chaudhari. What are Cycle Slips and Hangup in Phase Locked Loops?  [[https://wirelesspi.com/what-are-cycle-slips-and-hangup-in-phase-locked-loops/](https://wirelesspi.com/what-are-cycle-slips-and-hangup-in-phase-locked-loops/)]



![image-20260613083929737](cp-pll/image-20260613083929737.png)

###  XOR Phase Detector

![image-20260613083621395](cp-pll/image-20260613083621395.png)



### Tristate PFD

![image-20260613083646800](cp-pll/image-20260613083646800.png)

![image-20260613083715144](cp-pll/image-20260613083715144.png)

![image-20260613085340899](cp-pll/image-20260613085340899.png)

PFD requires periodic edges on both inputs

In a CDR, one input is random NRZ data, and a long run of identical bits has no transitions at all

The PFD's state machine interprets those missing edges as a huge phase/frequency error and pumps the loop away from lock



### frequency acquisition

![image-20260613095817926](cp-pll/image-20260613095817926.png)

![image-20260613101004088](cp-pll/image-20260613101004088.png)

> [[Gist link](https://gist.github.com/raytroop/ede1eca4ccea67da05b29ec1fdd78f34)]

![image-20260613101030913](cp-pll/image-20260613101030913.png)

![image-20260613101049573](cp-pll/image-20260613101049573.png)

>  beat period: $2\pi\cdot T_{beat,per}\cdot \Delta f = 2\pi \to T_{beat,per}=\frac{1}{\Delta f}$





### PFD Deadzone

> Sam Palermo, "Lecture 4: Phase Detector Circuit" [[https://people.engr.tamu.edu/spalermo/ecen620/lecture04_ee620_phase_detectors.pdf](https://people.engr.tamu.edu/spalermo/ecen620/lecture04_ee620_phase_detectors.pdf)]

![image-20260808091337910](cp-pll/image-20260808091337910.png)

Dead zone induced by *incomplete settling* of charge-pump currents

This situation can be avoided by adding *additional delay to the AND gate* in the PFD

![image-20241222190011244](cp-pll/image-20241222190011244.png)



---

> D. Turker et al., "A 7.4-to-14GHz PLL with 54fsrms jitter in 16nm FinFET for integrated RF-data-converter SoCs," 2018 IEEE International Solid-State Circuits Conference - (ISSCC), San Francisco, CA, USA, 2018 [[https://sci-hub.ru/10.1109/ISSCC.2018.8310342](

![image-20260807235323330](cp-pll/image-20260807235323330.png)

**$\tau$ shall be minimized to reduce noise of CP**



## PFD/CP Modeling

![image-20250807225013850](cp-pll/image-20250807225013850.png)

![pfdcp-lmdl.drawio](cp-pll/pfdcp-lmdl.drawio.svg)





---

---

<span style="color:blue">***feedback path delay***</span>

> Dennis Fischette, First Time, Every Time – Practical Tips for PhaseLocked Loop Design [[https://www.delroy.com/PLL_dir/tutorial/PLL_tutorial_slides.pdf](https://www.delroy.com/PLL_dir/tutorial/PLL_tutorial_slides.pdf)]
>
> Amir Amirkhany. ISSCC 2019 "Basics of Clock and Data Recovery Circuits"

Open-Loop PLL Gain

![image-20260812215725321](cp-pll/image-20260812215725321.png)

$\color{red}T_\text{pfd}/2$ term is typically an **equivalent delay caused by the <span style="color:blue">sampled-data nature of the PFD/charge-pump</span> **

![image-20260812212850273](cp-pll/image-20260812212850273.png)

The feedback divider provides a sampled version of the scaled VCO phase, and the PFD obtains the sampled phase error between that feedback phase and the reference phase

There is no delay between oscillator output phase and feedback divider output phase if C2Q and logic propagation delays are neglected

If the real divider has C2Q delay $t_{CQ}$, then it becomes approximately
$$
\boxed{T_d \approx t_{\mathrm{CQ}} + \frac{T_{\mathrm{pfd}}}{2}}
$$



An ideal feedback divider does not introduce propagation delay in **phase domain**

![image-20260814202707911](cp-pll/image-20260814202707911.png)




> ![image-20260812215429178](cp-pll/image-20260812215429178.png)





---

---

> Deog-Kyoon Jeong. Topics in IC Design 2.1 Introduction to Phase-Locked Loop

![image-20250807230740496](cp-pll/image-20250807230740496.png)





## Cycle Slipping

> Dennis Fischette, Could you explain the cycle-skip phenomenon in PLL performance? [[https://www.delroy.com/PLL_dir/FAQ/faq_cycle_slip.txt](https://www.delroy.com/PLL_dir/FAQ/faq_cycle_slip.txt)]

![image-20260627101018275](cp-pll/image-20260627101018275.png)





![image-20260613085103536](cp-pll/image-20260613085103536.png)

![image-20260613085238609](cp-pll/image-20260613085238609.png)





## Charge Pump Noise

> Cyclostationary Noise (Modulated Noise) [[https://raytroop.github.io/2024/04/27/noise/#cyclostationary-noise-modulated-noise](https://raytroop.github.io/2024/04/27/noise/#cyclostationary-noise-modulated-noise)]
>
> Sam Palermo, Lecture 3: Phase-Locked Loop Systems [[https://people.engr.tamu.edu/spalermo/ecen620/lecture03_ee620_pll_system.pdf](https://people.engr.tamu.edu/spalermo/ecen620/lecture03_ee620_pll_system.pdf)]

![image-20260212205227455](cp-pll/image-20260212205227455.png)

---

---

> Saurabh Saxena,Phase Locked Loops: Noise Simulations for CP-PLL Blocks [[https://youtu.be/Q1libz-XqRw](https://youtu.be/Q1libz-XqRw)]

![image-20250726183455160](cp-pll/image-20250726183455160.png)

---

---

> Michael H. Perrott, PLL Design Using the PLL Design Assistant Program. [[https://designers-guide.org/forum/Attachments/pll_manual.pdf](https://designers-guide.org/forum/Attachments/pll_manual.pdf)]
>
> M.H. Perrott, M.D. Trott, C.G. Sodini, "A Modeling Approach for Sigma-Delta Fractional-N Frequency Synthesizers Allowing Straightforward Noise Analysis", JSSC, vol 38, no 8, pp 1028-1038, Aug 2002. [[https://www.cppsim.com/Publications/JNL/perrott_jssc02.pdf](https://www.cppsim.com/Publications/JNL/perrott_jssc02.pdf)]

![image-20240928013058435](cp-pll/image-20240928013058435.png)



## Non-ideal Effects in Charge Pump

> Sam Palermo, Lecture 11: Clocking Architectures & PLLs [[https://people.engr.tamu.edu/spalermo/ecen689/lecture11_ee720_clocking_arch_plls.pdf](https://people.engr.tamu.edu/spalermo/ecen689/lecture11_ee720_clocking_arch_plls.pdf)]

The ***periodic*** signal on VCTRL modulates the VCO, giving rise to ***deterministic*** jitter

---

- Timing Offsets Between Up and Dn Pulses
- Mismatch Between Charge-Pump Current Sources
- Incomplete Settling of Charge-Pump Currents
- Finite Output Resistance of the Charge Pump



### Up/Dn Timing Offset

![image-20241222171705612](cp-pll/image-20241222171705612.png)

If Dn pulse arrives $\Delta T$ after the Up pulse, the steady-state VCTRL will be slightly **lower** than it would be without the $\Delta T$ mismatch so as to return the VCO's phase to match the reference clocks.

Vice versa, if If Up pulse arrives $\Delta T$ after the Dn pulse, the steady-state VCTRL will be slightly **higher** than without $\Delta T$ mismatch



### Current Sources Mismatch

![image-20241222174620713](cp-pll/image-20241222174620713.png)

![image-20241222174718564](cp-pll/image-20241222174718564.png)

---

![image-20260426171720182](cp-pll/image-20260426171720182.png)

---

---

> Young, I.A., Greason, J.K., Wong, K.L.: A PLL Clock Generator with 5 to 110MHz of Lock Range for Microprocessors. IEEE Journal of Solid-State Circuits 27(11), 1599– 1607 (1992)  [[https://people.engr.tamu.edu/spalermo/ecen620/pll_intel_young_jssc_1992.pdf](https://people.engr.tamu.edu/spalermo/ecen620/pll_intel_young_jssc_1992.pdf)]
>
> Johnson, M., Hudson, E.: A variable delay line PLL for CPU-coprocessor synchronization. IEEE Journal of Solid-State Circuits 23(10), 1218–1223 (1988)  [[https://sci-hub.se/10.1109/4.5947](https://sci-hub.se/10.1109/4.5947)]
>
> Sam Palermo, Lecture 5: Charge Pump Circuits, ECEN620: Network Theory Broadband Circuit Design Fall 2024 [[https://people.engr.tamu.edu/spalermo/ecen620/lecture05_ee620_charge_pumps.pdf](https://people.engr.tamu.edu/spalermo/ecen620/lecture05_ee620_charge_pumps.pdf)]
>
> D. Turker et al., "A 7.4-to-14GHz PLL with 54fsrms jitter in 16nm FinFET for integrated RF-data-converter SoCs," 2018 IEEE International Solid-State Circuits Conference - (ISSCC), San Francisco, CA, USA, 2018 [[https://sci-hub.ru/10.1109/ISSCC.2018.8310342](https://sci-hub.ru/10.1109/ISSCC.2018.8310342)]

***charge pump with amplifier***

![](cp-pll/image-20260426171545204.png)

![image-20260808005243795](cp-pll/image-20260808005243795.png)



## off-state leakage

*TODO* &#128197;

### Incomplete Settling

*TODO* &#128197;



> W. Rhee, "Design of high-performance CMOS charge pumps in phase-locked loops," *1999 IEEE International Symposium on Circuits and Systems (ISCAS)*, Orlando, FL, USA, 1999, pp. 545-548 vol.2 [[pdf](https://citeseerx.ist.psu.edu/document?repid=rep1&type=pdf&doi=3006edc15fdef2e71674d4170c10c62fd69f96a3)]
>
> Cowan G. *Mixed-Signal CMOS for Wireline Communication: Transistor-Level and System-Level Design Considerations*. Cambridge University Press; 2024



## 2nd loop filter

> PI (proportional - integral) Loop Filter

![image-20240907123938255](cp-pll/image-20240907123938255.png)

![image-20240907124029346](cp-pll/image-20240907124029346.png)

![image-20240907124018476](cp-pll/image-20240907124018476.png)



## LPF leakage

![image-20241222192007824](cp-pll/image-20241222192007824.png)



For the sake of simplicity, $V_{ctr}$ looks like a rectangular pulse with an amplitude of $I_{CP}R_1$ and a duty ratio of ($I_{leak}/I_{CP}$), whose first coefficient of Fourier series is

![image-20241222200514941](cp-pll/image-20241222200514941.png)

where $I_\text{leak} \ll I_{CP}$ is assumed

Then, the *peak* frequency deviation $\Delta f$
$$
\Delta f = a_1 \cdot K_v = 2I_\text{leak}R_1 K_v
$$
using narrowband FM approximation, we have 
$$
P_\text{spur} = 20\log\left(\frac{\Delta f}{2f_\text{ref}}\right) = 20\log\left(\frac{I_\text{leak}R_1 K_v}{f_\text{ref}}\right)
$$




> W. Rhee, "Design of high-performance CMOS charge pumps in phase-locked loops," *1999 IEEE International Symposium on Circuits and Systems (ISCAS)*, Orlando, FL, USA, 1999, pp. 545-548 vol.2 [[pdf](https://citeseerx.ist.psu.edu/document?repid=rep1&type=pdf&doi=3006edc15fdef2e71674d4170c10c62fd69f96a3)]
>
> —. Yu, Z., 2024. *Phase-Locked Loops: System Perspectives and Circuit Design Aspects*. John Wiley & Sons



---

![image-20241222200158107](cp-pll/image-20241222200158107.png)

> [[https://lpsa.swarthmore.edu/Fourier/Series/ExFS.html](https://lpsa.swarthmore.edu/Fourier/Series/ExFS.html)]










## PFD/CP Simulation

*TODO* &#128197;







## reference

Lacaita, Andrea Leonardo, Salvatore Levantino, and Carlo Samori. *Integrated frequency synthesizers for wireless systems*. Cambridge University Press, 2007.

Saurabh Saxena. Noise Simulations for CP-PLL Blocks [[https://youtu.be/Q1libz-XqRw](https://youtu.be/Q1libz-XqRw)]

—, IIT Madras. CICC2022 Clocking for Serial Links - Frequency and Jitter Requirements, Phase-Locked Loops, Clock and Data Recovery

Helene Thibieroz, Customer Support CIC. Using Spectre RF Noise-Aware PLL Methodology to Predict PLL Behavior Accurately  [[https://citeseerx.ist.psu.edu/document?repid=rep1&type=pdf&doi=3056e59ea76165373f90152f915a829d25dabebc](https://citeseerx.ist.psu.edu/document?repid=rep1&type=pdf&doi=3056e59ea76165373f90152f915a829d25dabebc)]

---

Chembiyan T. Chargepump PLL Basics- From A Control Theoretic Viewpoint [[linkedin](https://www.linkedin.com/posts/chembiyan-t-0b34b910_cppll-basics-activity-7047198719787626496--7GG?utm_source=share&utm_medium=member_desktop&rcm=ACoAAD-cuiIBDJ62eh9q3qTSSdslYXr-XMd8TGw)]

—. Challenges in Chargepump PLL Design- A Qualitative Approach [[linkedin](https://www.linkedin.com/posts/chembiyan-t-0b34b910_cppll-design-challenges-activity-7036787568344006657-7vM1?utm_source=share&utm_medium=member_desktop&rcm=ACoAAD-cuiIBDJ62eh9q3qTSSdslYXr-XMd8TGw)]

—. A Unified Approach to Low Noise Loop Design in Chargepump PLLs [[linkedin](https://www.linkedin.com/posts/chembiyan-t-0b34b910_pll-loop-design-shorter-version-activity-7116456644846252032-Klx0?utm_source=share&utm_medium=member_desktop&rcm=ACoAAD-cuiIBDJ62eh9q3qTSSdslYXr-XMd8TGw)]


N. Kuznetsov, A. Matveev, M. Yuldashev and R. Yuldashev, "Nonlinear Analysis of Charge-Pump Phase-Locked Loop: The Hold-In and Pull-In Ranges," in IEEE Transactions on Circuits and Systems I: Regular Papers, vol. 68, no. 10, pp. 4049-4061, Oct. 2021 [[https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=9509840](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=9509840)]

---

Xiang Gao Credo Semiconductor. ISSCC2018 T1: Low-Jitter PLLs for Wireless Transceivers
