---
title: Spurs
date: 2024-07-14 09:17:11
tags:
categories:
- noise
mathjax: true
---

*TODO* &#128197;


**spurs** are carrier or clock frequency spectral imperfections measured in the frequency domain just like phase noise. However, unlike phase noise they are *discrete* frequency components.

- Spurs are deterministic.

- Spur power is independent of bandwidth.

- Spurs contribute bounded peak jitter in the time domain.



## reference spurs



> https://www.linkedin.com/posts/chembiyan-t-0b34b910_pll-rfdesign-circuits-activity-7111435571448713216-9jng?utm_source=share&utm_medium=member_desktop



## charge pump mismatch

Matching of the CP currents is also a critical part of PLL design. Leakage and mismatch in the CP will lead to *deterministic jitter* on the PLL output

Any difference between the charging and discharging currents can cause static phase offset as well as *dynamic jitter*, known as **reference spur**



peak2peak deterministic jitter
$$
\text{DJ}_\text{PP} = \frac{\phi_{PP}}{2\pi}T_{osc}
$$


```matlab
kvco = 1e9;
Icp = 600e-6;
deltaI_Icp = 3e-2;
deltaI = deltaI_Icp*Icp;
ton = 100e-12;
C2 =0.5e-12;
Tosc = 1/15e9;

DJpp = kvco*deltaI*ton^2/(2*C2)*(deltaI_Icp + 1)*Tosc
```



> W. Rhee, "Design of high-performance CMOS charge pumps in phase-locked loops," *1999 IEEE International Symposium on Circuits and Systems (ISCAS)*, Orlando, FL, USA, 1999, pp. 545-548 vol.2 [[https://citeseerx.ist.psu.edu/document?repid=rep1&type=pdf&doi=3006edc15fdef2e71674d4170c10c62fd69f96a3](https://citeseerx.ist.psu.edu/document?repid=rep1&type=pdf&doi=3006edc15fdef2e71674d4170c10c62fd69f96a3)]
>
> Rhee, W. and Yu, Z., 2024. *Phase-Locked Loops: System Perspectives and Circuit Design Aspects*. John Wiley & Sons.
>
> H. M. S. Fazeel, L. Raghavan, C. Srinivasaraman and M. Jain, "Reduction of Current Mismatch in PLL Charge Pump," *2009 IEEE Computer Society Annual Symposium on VLSI*, Tampa, FL, USA, 2009, pp. 7-12, doi: 10.1109/ISVLSI.2009.45.
>
> H. -G. Ko, W. Bae, G. -S. Jeong and D. -K. Jeong, "Reference Spur Reduction Techniques for a Phase-Locked Loop," in *IEEE Access*, vol. 7, pp. 38035-38043, 2019 [[https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=8671476](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=8671476)]








## reference

Timing 101 #6: The Case of the Spurious Phase Noise, Silicon Labs,  [[Part I](https://community.silabs.com/s/share/a5U1M000000knzQUAQ/timing-101-6-the-case-of-the-spurious-phase-noise-part-i)], [[Part II](https://community.silabs.com/s/share/a5U1M000000knzQUAQ/timing-101-6-the-case-of-the-spurious-phase-noise-part-i?language=en_US)], [[Part III](https://community.silabs.com/s/share/a5U1M000000ko4DUAQ/timing-201-2-the-case-of-the-phase-noise-that-wasnt-part-2?language=en_US)]



