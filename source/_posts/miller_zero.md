---
title: Miller Zero and How to Mitigate Impact of Zero
date: 2022-02-24 13:14:38
tags:
- small signal
- amplifier
categories:
- analog
mathjax: true
---

#### Lectures
EE 240B: Advanced Analog Circuit Design, Prof. Bernhard E. Boser\
[OTA II, Multi-Stage](https://people.eecs.berkeley.edu/~boser/courses/240B/lectures/M07%20OTA%20II.pdf)

#### Papers

B. K. Ahuja, "An improved frequency compensation technique for CMOS operational amplifiers," in IEEE Journal of Solid-State Circuits, vol. 18, no. 6, pp. 629-633, Dec. 1983, doi: 10.1109/JSSC.1983.1052012.

D. B. Ribner and M. A. Copeland, "Design techniques for cascoded CMOS op amps with improved PSRR and common-mode input range," in IEEE Journal of Solid-State Circuits, vol. 19, no. 6, pp. 919-925, Dec. 1984, doi: 10.1109/JSSC.1984.1052246.

Abo, Andrew & Gray, Paul. (1999). A 1.5V, 10-bit, 14MS/s CMOS Pipeline Analog-to-Digital Converter.

#### Book's chapters
Design of analog CMOS integrated circuits, Behzad Razavi\
10.5 Compensation of Two-Stage Op Amps\
10.7 Other Compensation Techniques

Analog Design Essentials, Willy M.C. Sansen\
chapter #5 Stability of operational amplifiers - Compensation of positive zero

Analysis and Design of Analog Integrated Circuits 5th Edition,  Paul R. Gray, Paul J. Hurst, Stephen H. Lewis, Robert G. Meyer\
9.4.3 Two-Stage MOS Amplifier Compensation

CMOS Analog Circuit Design 3rd Edition,  Phillip E. Allen, Douglas R. Holberg\
6.2.2 Miller Compensation of the Two-Stage Op Amp

#### Example - cascode compensation
![cascode_compensation](miller_zero/cascode_compensation.PNG)
$$\begin{align}
\omega_{p1} &= \frac {1} {R_{eq}g_{m9}R_{L}C_{c}} \\
\omega_{p2} &= \frac {g_{m4}R_{eq}g_{m9}} {C_L} \\
\omega_z &= (g_{m4}R_{eq})(\frac {g_{m9}} {C_c})
\end{align}$$

> Figure 10.46 in Razavi's book