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



## OTA offset affect


![bg_ota_vos.drawio](bgr/bg_ota_vos.drawio.svg)

$$\begin{align}
V_{be1} &= \frac{kT}{q}\ln(\frac{I_{e1}}{I_{ss}}) \\
V_{be2} &= \frac{kT}{q}\ln(\frac{I_{e2}}{nI_{ss}})
\end{align}$$

Hence,

$$\begin{align}
\Delta V_{be} &= \frac{kT}{q}\ln(n\frac{I_{e1}}{I_{e2}}) \\
&= \frac{kT}{q}\ln(n) + \frac{kT}{q}\ln(\frac{I_{e1}}{I_{e2}}) \\
&= \Delta V_{be0} + \frac{kT}{q}\ln(\frac{I_{e1}}{I_{e2}})
\end{align}$$

Therefore,

$$\begin{align}
V_{bg} &= \frac{\Delta V_{be}+V_{os}}{R_2}(R_1+R_2) + V_{be2} \\
&= \alpha \Delta V_{be0} + \alpha \frac{kT}{q}\ln(\frac{I_{e1}}{I_{e2}}) + \alpha V_{os} + \frac{kT}{q}\ln(\frac{I_{e2}}{nI_{ss}}) \\
&= \alpha \Delta V_{be0} + \alpha \frac{kT}{q}\ln(\frac{I_{e1}}{I_{e2}}) + \alpha V_{os} + \frac{kT}{q}\ln(\frac{I_{e2,0}}{nI_{ss}})+\frac{kT}{q}\ln(\frac{I_{e2}}{I_{e2,0}})
\end{align}$$

We omit the last part
$$\begin{align}
V_{bg} &= \alpha \Delta V_{be0} + \alpha \frac{kT}{q}\ln(\frac{I_{e1}}{I_{e2}}) + \alpha V_{os} + \frac{kT}{q}\ln(\frac{I_{e2,0}}{nI_{ss}}) \\
&= \alpha \Delta V_{be0} + \frac{kT}{q}\ln(\frac{I_{e2,0}}{nI_{ss}}) + \alpha \left(V_{os} + \frac{kT}{q}\ln(\frac{I_{e1}}{I_{e2}})\right) \\
&= V_{bg,0} + \alpha \left(V_{os} + \frac{kT}{q}\ln(\frac{I_{e1}}{I_{e2}})\right)
\end{align}$$

i.e. the bg varitaion due to OTA offset is
$$
\Delta V_{bg} \approx \alpha \left(V_{os} + \frac{kT}{q}\ln(\frac{I_{e1}}{I_{e2}})\right)
$$

- $V_{os} \gt 0$

$I_{e1} \gt I_{e2}$: $\Delta V_{bg} \gt \alpha V_{os}$

- $V_{os} \lt 0$

$I_{e1} \lt I_{e2}$: $\Delta V_{bg} \lt \alpha V_{os}$

## reference

ECEN 607 (ESS) Bandgap Reference: Basics URL:[https://people.engr.tamu.edu/s-sanchez/607%20Lect%204%20Bandgap-2009.pdf](https://people.engr.tamu.edu/s-sanchez/607%20Lect%204%20Bandgap-2009.pdf)
