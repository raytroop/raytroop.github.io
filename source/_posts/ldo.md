---
title: Low-Dropout Regulator
date: 2023-10-21 10:31:41
tags:
categories:
- analog
mathjax: true
---


## PMOS LDO

A large output capacitor solves the sudden load change problem, but the stability decreases because the large output capacitor forces the output pole toward the origin with the role of dominant pole



## DC output impedance 

DC output impedance of NMOS and PMOS LDO is the ***same*** for the same error amplifier gain

$$
R_{\text{out}} = \frac{1}{\beta A_{o1} g_{m2}}
$$

The NMOS LDO has a faster response to line transients than the PMOS LDO since it has better (smaller) PSRR

A good PSRR is important when an LDO is used as a sub-regulator in cascade with a switching regulator. The LDO would need to have a sufficiently high rejection at the switching frequency of the switching converter to filter out the ripples at that frequency



## Power MOS gain affect on PMOS LDO

![pwm_miller.drawio](ldo/pwm_miller.drawio.svg)



DC gain
$$
A_{dc} = g_mR_\text{ota} A_2
$$
3dB bandwidth
$$
\omega_p = \frac{1}{R_\text{ota}(C_g+A_2C_c)}
$$
and GBW
$$
\omega_u = \frac{g_m}{\frac{C_g}{A_2}+C_c}
$$


![image-20240803102158612](ldo/image-20240803102158612.png)



### Feedforward Compensation with $C_\text{FF}$​

- Improved Noise
- Improved Stability and Transient Response
- Improved PSRR

![outCc.drawio](ldo/outCc.drawio.svg)

$$\begin{align}
R_1 \parallel \frac{1}{sC_{FF}} &= \frac{R_1}{1+sR_1C_{FF}} \\
Z_o &= \left( R_1\parallel \frac{1}{sC_{FF}}+R_2\right)\parallel \frac{1}{sC_L} \\
&=\frac{R_1+R_2+sR_1R_2C_{FF}}{s^2R_1R_2C_{FF}C_L + s[(R_1+R_2)C_L+R_1C_{FF}]+1} \\
A_{V2} &= g_m Z_o \\
&= g_m \frac{R_1+R_2+sR_1R_2C_{FF}}{s^2R_1R_2C_{FF}C_L + s[(R_1+R_2)C_L+R_1C_{FF}]+1} \\
\beta &= \frac{R_2}{\frac{R_1}{1+sR_1C_{FF}}+R_2} \\
&= \frac{R_2(1+sR_1C_{FF})}{R_1+R_2+sR_1R_2C_{FF}} \\
A_{V2}\beta &= \frac{g_mR_2(1+sR_1C_{FF})}{s^2R_1R_2C_{FF}C_L+s[(R_1+R_2)C_L+R_1C_{FF}]+1} 
\end{align}$$

That is, adding a $C_{FF}$ also introduces a zero ($\omega_z$) and pole ($\omega_p$) into the *LDO feedback loop*

$$\begin{align}
\omega_{po} &= \frac{1}{(R_1+R_2)C_L} \\
\omega_z &= \frac{1}{R_1C_{FF}} \\
\omega_{p} &= \frac{1}{(R_1 \parallel R_2)C_{FF}}
\end{align}$$



> Application Report SBVA042–July 2014, Pros and Cons of Using a Feedforward Capacitor with a Low-Dropout Regulator [[https://www.ti.com/lit/an/sbva042/sbva042.pdf](https://www.ti.com/lit/an/sbva042/sbva042.pdf)]
>
> LDO Basics: Noise – How a Feed-forward Capacitor Improves System Performance [[https://www.ti.com/document-viewer/lit/html/SSZTA13](https://www.ti.com/document-viewer/lit/html/SSZTA13)]
>
> LDO Basics: Noise – How a Noise-reduction Pin Improves System Performance [[https://www.ti.com/document-viewer/lit/html/SSZTA40](https://www.ti.com/document-viewer/lit/html/SSZTA40)]



## NMOS Slave LDO

![nmos_slave_psrr.drawio](ldo/nmos_slave_psrr.drawio.svg)

$$\begin{align}
\frac{V_g}{V_i} &=\frac{R||\frac{1}{s(C_g+C_{gs})}}{R||\frac{1}{s(C_g+C_{gs})}+\frac{1}{sC_{gd}}} \\
&= \frac{sRC_{gd}}{sR(C+C_{gd}+C_{gs})+1}
\end{align}$$
$$
\frac{V_g}{V_i} = -\frac{sC_{ds}+g_{ds}}{sC_{gs}+g_m}
$$

That is,
$$
\omega_{z,d} \simeq \frac{1}{R(\frac{g_m}{g_{ds}}C_{gd}+C)}
$$

The calculating PSRR pole approach similar with zero, just $V_o$ to $V_i$ zero
$$
\omega_{p,d} \simeq \frac{1}{R(\frac{C_s}{g_mR}+C)}
$$

DC PSRR
$$
\text{PSRR} = \frac{1}{g_mr_o}
$$

---

![image-20240726205718920](ldo/image-20240726205718920.png)

![image-20240726205738664](ldo/image-20240726205738664.png)

---



## High frequency PSRR

![high-psrr.drawio](ldo/high-psrr.drawio.svg)





## feedback resistor divider noise

*TODO* &#128197;







## reference

Hinojo, J.M., Martinez, C.I., & Torralba, A.J. (2018). Internally Compensated LDO Regulators for Modern System-on-Chip Design.

Mingoo Seok. ISSCC 2020 tutorial "Basics of Digital Low-Dropout (LDO) Integrated Voltage Regulator"

Pavan Kumar Hanumolu. CICC 2015. "Low Dropout Regulators"

Chen, K. (2016). Power Management Techniques for Integrated Circuit Design.

Morita, B.G. (2014). Understand Low-Dropout Regulator ( LDO ) Concepts to Achieve Optimal Designs.

H. -S. Kim, "Exploring Ways to Minimize Dropout Voltage for Energy-Efficient Low-Dropout Regulators: Viable approaches that preserve performance," in IEEE Solid-State Circuits Magazine, vol. 15, no. 2, pp. 59-68, Spring 2023, doi: 10.1109/MSSC.2023.3262767.

Ali Sheikholeslami, Circuit Intuitions: Voltage Regulators IEEE Solid-State Circuits Magazine, Vol. 12, Issue 4, to appear, Fall 2020.

Operational Transconductance Amplifier II Multi-Stage Designs [[https://people.eecs.berkeley.edu/~boser/courses/240B/lectures/M07%20OTA%20II.pdf](https://people.eecs.berkeley.edu/~boser/courses/240B/lectures/M07%20OTA%20II.pdf)]

Toshiba, Load Transient Response of LDO and Methods to Improve it Application Note [[https://toshiba.semicon-storage.com/info/application_note_en_20210326_AKX00312.pdf?did=66268](https://toshiba.semicon-storage.com/info/application_note_en_20210326_AKX00312.pdf?did=66268)]



