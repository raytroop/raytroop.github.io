---
title: Demystifying stb and pstb in Spectre
date: 2022-03-06 15:23:40
tags:
- stb
- pstb
- spectre
- stability
categories:
- cad
mathjax: true
---

All credits to my colleague, Zhang Wenpian.

### Spectre's stb analysis

Spectre **stb**'s "loopgain" is negative of "T" in paper<sup>[1]</sup>
$$
T = \frac{2(AD-BC) - A + D}{2(AD-BC)-A+D-1}
$$

AC simulation testbench, shown as below,

![stb_pstb.drawio](stb-pstb-spectre/stb_pstb.drawio.svg)

1. $I_{inj}$ = 0, $V_{inj}$ = 1

   B = if, D = ve

2. $I_{inj}$ = 1, $V_{inj}$ = 0

   A = if, C = ve

### Spectre's pstb analysis

Spectre **pstb** is similar to stb, just set **pac** as **1** instead of  **ac** in current source and voltage source.

This analysis just use **harmonic 0** transfer function in pac analysis, which has limitation.



### reference

M. Tian, V. Visvanathan, J. Hantgan and K. Kundert, "Striving for small-signal stability," in IEEE Circuits and Devices Magazine, vol. 17, no. 1, pp. 31-41, Jan. 2001, doi: 10.1109/101.900125.

Open loop gain analysis and "STB" method  [https://www.linkedin.com/pulse/open-loop-gain-analysis-stb-method-jean-francois-debroux](https://www.linkedin.com/pulse/open-loop-gain-analysis-stb-method-jean-francois-debroux )
