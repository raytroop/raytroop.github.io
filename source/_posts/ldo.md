---
title: Low-Dropout Regulator
date: 2023-10-21 10:31:41
tags:
categories:
- analog
mathjax: true
---

*TODO* &#128197;


## PMOS LDO

A large output capacitor solves the sudden load change problem, but the stability decreases because the large output capacitor forces the output pole toward the origin with the role of dominant pole


## damping factor ($\zeta$) and phase margin

phase margin is defined for *open loop* system

damping factor ($\zeta$) is defined for *close loop* system

the roughly 90 to 100 times of damping factor ($\zeta$) is phase margin

$$
\mathrm{PM} = 90\zeta ~ 100\zeta
$$

> in order to have a good stable system, we want $\zeta > 0.5$ or phase margin more than $45^o$

> We can analyze open loop system in a better perspective because it is simpler



DC output impedance of NMOS and PMOS LDO is the *same* for the same error amplifier gain

$$
R_{\text{out}} = \frac{1}{\beta A_{o1} g_{m2}}
$$

The NMOS LDO has a faster response to line transients than the PMOS LDO since it has btter (smaller) PSRR

A good PSRR is important when an LDO is used as a sub-regulator in cascade with a switching regulator. The LDO would need to have a sufficiently high rejection at the switching frequency of the switching converter to filter out the ripples at that frequency




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

