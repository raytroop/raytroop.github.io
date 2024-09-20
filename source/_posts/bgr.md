---
title: Bandgap Reference
date: 2022-11-17 00:15:17
tags:
categories:
- analog
mathjax: true
---



## temperature coefficient

The parameter that shows the dependence of the reference voltage on temperature variation is called the temperature coefficient and is defined as:
$$
TC_F=\frac{1}{V_{\text{REF}}}\left[ \frac{V_{\text{max}}-V_{\text{min}}}{T_{\text{max}}-T_{\text{min}}} \right]\times10^6\;ppm/^oC
$$

## Choice of n



![image-20221117002714125](bgr/image-20221117002714125.png)




## classic bandgap reference

![bg.drawio](bgr/bg.drawio.svg)

(a)
$$
V_{bg} = \frac{\Delta V_{be}}{R_1} (R_1+R_2) + V_{be2} = \frac{\Delta V_{be}}{R_1} R_2 + V_{be1}
$$
(b)
$$
V_{bg} = \left(\frac{\Delta V_{be}}{R_1} + \frac{V_{be1}}{R_2}\right)R_3 = \left(\frac{\Delta V_{be}}{R_1} R_2 + V_{be1}\right)\frac{R_3}{R_2}
$$










## reference

ECEN 607 (ESS) Bandgap Reference: Basics URL:[https://people.engr.tamu.edu/s-sanchez/607%20Lect%204%20Bandgap-2009.pdf](https://people.engr.tamu.edu/s-sanchez/607%20Lect%204%20Bandgap-2009.pdf)
