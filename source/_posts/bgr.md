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



## OTA offset effect


![bg_ota_vos.drawio](bgr/bg_ota_vos.drawio.svg)

$$\begin{align}
V_{be1} &= \frac{kT}{q}\ln(\frac{I_{e1}}{I_{ss}}) \\
V_{be2} &= \frac{kT}{q}\ln(\frac{I_{e2}}{nI_{ss}})
\end{align}$$

Here, we assume $I_e = I_c$



Hence,

$$\begin{align}
\Delta V_{be} &= \frac{kT}{q}\ln(n\frac{I_{e1}}{I_{e2}}) \\
&= \frac{kT}{q}\ln(n) + \frac{kT}{q}\ln(\frac{I_{e1}}{I_{e2}}) \\
&= \Delta V_{be,0} + \frac{kT}{q}\ln(\frac{I_{e1}}{I_{e2}})
\end{align}$$

Therefore,

$$\begin{align}
V_{bg} &= \frac{\Delta V_{be}+V_{os}}{R_2}(R_1+R_2) + V_{be2} \\
&= \alpha \Delta V_{be,0} + \alpha \frac{kT}{q}\ln(\frac{I_{e1}}{I_{e2}}) + \alpha V_{os} + \frac{kT}{q}\ln(\frac{I_{e2}}{nI_{ss}}) \\
&= \alpha \Delta V_{be,0} + \alpha \frac{kT}{q}\ln(\frac{I_{e1}}{I_{e2}}) + \alpha V_{os} + \frac{kT}{q}\ln(\frac{I_{e2,0}}{nI_{ss}})+\frac{kT}{q}\ln(\frac{I_{e2}}{I_{e2,0}})
\end{align}$$



We omit the last part
$$\begin{align}
V_{bg} &\approx \alpha \Delta V_{be,0} + \alpha \frac{kT}{q}\ln(\frac{I_{e1}}{I_{e2}}) + \alpha V_{os} + \frac{kT}{q}\ln(\frac{I_{e2,0}}{nI_{ss}}) \\
&= \alpha \Delta V_{be,0} + V_{be2,0} + \alpha \left(V_{os} + \frac{kT}{q}\ln(\frac{I_{e1}}{I_{e2}})\right) \\
&= V_{bg,0} + \alpha \left(V_{os} + \frac{kT}{q}\ln(\frac{I_{e1}}{I_{e2}})\right)
\end{align}$$

i.e. the bg variation due to OTA offset
$$
\Delta V_{bg} \approx \alpha \left(V_{os} + \frac{kT}{q}\ln(\frac{I_{e1}}{I_{e2}})\right)
$$

- $V_{os} \gt 0$

​	$I_{e1} \gt I_{e2}$: $\Delta V_{bg} \gt \alpha V_{os}$

- $V_{os} \lt 0$

​	$I_{e1} \lt I_{e2}$: $\Delta V_{bg} \lt \alpha V_{os}$


## OTA with chopper

![bg_chop.drawio](bgr/bg_chop.drawio.svg)

![bg_chop_shift.drawio](bgr/bg_chop_shift.drawio.svg)

> $I_{e1}$, $I_{e2}$


$$\begin{align}
V_{ip} &= V_{im} + V_{os} \\
\frac{V_{bg}-V_{ip}}{R_2} &= I_{e2} \\
\frac{V_{bg}-V_{im}}{R_2} &= I_{e1} \\
V_{ip} &= I_{e2}R_1 + V_T\frac{I_{e2}}{nI_S} \\
V_{im} &= V_T\frac{I_{e1}}{I_S}
\end{align}$$
where $V_T = \frac{kT}{q}$

we obtain
$$
I_{e1} = \frac{V_T\ln n}{R_1} + V_{os}\left(\frac{1}{R_1} + \frac{1}{R_2} \right) - \frac{1}{R_1}\cdot V_T\ln\left(1- \frac{V_{os}}{R_2I_{e1}} \right)
$$

we omit the last part
$$\begin{align}
I_{e1} &= I_{e0} + V_{os}\left(\frac{1}{R_1} + \frac{1}{R_2} \right) \\
I_{e2} &= I_{e1} - \frac{V_{os}}{R_2} = I_{e0} + \frac{V_{os}}{R_1}
\end{align}$$
where $I_{e0} = \frac{\Delta V_{be}}{R_1}$, $\Delta V_{be}=V_T\ln n$

> That is, both $I_{e1}$ and $I_{e2}$ are proportional to $V_{os}$

$I_{e1}$ and $I_{e2}$ can be expressed as
$$\begin{align}
I_{e1} &= I_{e0} + V_{os}\left(\frac{1}{R_1} + \frac{1}{2R_2} \right) + \frac{V_{os}}{2R_2} \\
I_{e2} &= I_{e0} + V_{os}\left(\frac{1}{R_1} + \frac{1}{2R_2} \right) - \frac{V_{os}}{2R_2}
\end{align}$$
i.e., $\Delta I_{e,cm} = V_{os}\left(\frac{1}{R_1} + \frac{1}{2R_2} \right)$ and $\Delta I_{e,dif} =\frac{V_{os}}{2R_2}$

bandgap output voltage is

$$\begin{align}
V_{bg} &= V_T \ln \frac{I_{e1}}{I_s} + I_{e1}R_2 \\
&= V_T \ln \frac{I_{e0} + V_{os}\left(\frac{1}{R_1} + \frac{1}{R_2} \right)}{I_s} + I_{e1}R_2 \\
&= V_T \ln \frac{I_{e0} + V_{os}\left(\frac{1}{R_1} + \frac{1}{R_2} \right)}{I_s} + I_{e0}R_2 + V_{os}\frac{R_1+R_2}{R_1} \\
&= I_{e0}R_2 + V_T \ln \frac{I_{e0}}{I_s} + V_T\ln\left(1+\frac{V_{os}\left(\frac{1}{R_1} + \frac{1}{R_2} \right)}{I_{e0}}  \right) + V_{os}\frac{R_1+R_2}{R_1} \\
&= V_{bg0} +  V_T\ln\left(1+\frac{V_{os}\left(\frac{1}{R_1} + \frac{1}{R_2} \right)}{I_{e0}}  \right) + V_{os}\frac{R_1+R_2}{R_1}
\end{align}$$



## ripple cancellation

![rippleCancel.drawio](bgr/rippleCancel.drawio.svg)

***phase 0:***

$$\begin{align}
V_{os}[n] &= V_{os}[n-1] - \frac{\Delta I_1}{g_m} \\
V_{os}[n]  &=  I_\Delta[n] R_E \\
\beta I_\Delta &= I_1[n] + I_2[n-1]
\end{align}$$
where $I_\Delta$ is the variation of $I_{e1}+I_{e2}$ due to $V_{os}$ and $R_E = \frac{R_1R_2}{R_1+2R_2}$


obtain
$$\begin{align}
\Delta I_1 &= G\cdot V_{os}[n-1] - K\cdot I_1[n-1] - K\cdot I_2[n-1] \\
I_1[n] &= G\cdot V_{os}[n-1] + (1-K)\cdot I_1[n-1] - K\cdot I_2[n-1] \\
V_{os}[n] &= K\cdot V_{os}[n-1] + R\cdot I_1[n-1] + R\cdot I_2[n-1]\\
\end{align}$$

where $G=g_m\frac{\beta}{g_m R_E + \beta}$, $R=R_E\frac{1}{g_m R_E + \beta}$ and $K=\frac{g_mR_E}{g_m R_E + \beta}$

and
$$
V_{os}[n] = (2K-1)\cdot V_{os}[n-1] = (1-\frac{2\beta}{g_mR_E+\beta})\cdot V_{os}[n-1]
$$

***phase 1:***

$$\begin{align}
V_{os}[n] &= V_{os}[n-1] - \frac{-\Delta I_2}{g_m} \\
V_{os}[n]  &=  -I_\Delta[n] R_E \\
\beta I_\Delta &= I_1[n] + I_2[n-1]
\end{align}$$

obtain
$$\begin{align}
\Delta I_2 &= -G\cdot V_{os}[n-1] - K\cdot I_1[n-1] - K\cdot I_2[n-1] \\
I_1[n] &= -G\cdot V_{os}[n-1] -K\cdot I_1[n-1] + (1-K)\cdot I_2[n-1] \\
V_{os}[n] &= K\cdot V_{os}[n-1] - R\cdot I_1[n-1] - R\cdot I_2[n-1]\\
\end{align}$$

similaly
$$
V_{os}[n] = (1-\frac{2\beta}{g_mR_E+\beta})\cdot V_{os}[n-1]
$$


That is, for either phase
$$
V_{os}[n] = (1-\frac{2\beta}{g_mR_E+\beta})\cdot V_{os}[n-1]
$$


## reference

ECEN 607 (ESS) Bandgap Reference: Basics URL:[https://people.engr.tamu.edu/s-sanchez/607%20Lect%204%20Bandgap-2009.pdf](https://people.engr.tamu.edu/s-sanchez/607%20Lect%204%20Bandgap-2009.pdf)
