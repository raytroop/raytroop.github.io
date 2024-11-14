---
title: Analog Front-End (AFE) Design & Equalization Techniques
date: 2024-09-21 21:08:12
tags:
categories:
- analog
mathjax: true
---



## MOS parasitic Rd&Rs, Cd&Cs

Decrease  the parasitic R&C

priority: $R_s \gt R_d$, $C_s \gt C_d$



## XCP as Negative Impedance Converter (NIC)

The **Cross-Coupled Pair (XCP)** can operate as an **impedance negator** [a.k.a. a **negative impedance converter** (**NIC**)] 

A common application is to create a *negative capacitance* that can cancel the *positive capacitance*
seen at a port, thereby improving the *speed*

![image-20240922174319496](afe/image-20240922174319496.png)
$$
I_{NIC} =\frac{V_{im} - V_{ip}}{\frac{2}{g_m}+\frac{1}{sC_c}} = \frac{-2V_{ip}}{\frac{2}{g_m}+\frac{1}{sC_c}}
$$
Therefore
$$
Z_{NIC} = \frac{V_{ip} - V_{im}}{I_{NIC}}=\frac{2V_{ip}}{I_{NIC}} =- \frac{2}{g_m}-\frac{1}{sC_c}
$$
***half-circuit***

If $C_{gd}$ is considered, and apply miller effect. half equivalent circuit is shown as below

![nic.drawio](afe/nic.drawio.svg)





> B. Razavi, "The Cross-Coupled Pair - Part III [A Circuit for All Seasons]," IEEE Solid-State Circuits Magazine, Issue. 1, pp. 10-13, Winter 2015. [[https://www.seas.ucla.edu/brweb/papers/Journals/BR_Magzine3.pdf](https://www.seas.ucla.edu/brweb/papers/Journals/BR_Magzine3.pdf)]
>
> S. Galal and B. Razavi, "10-Gb/s Limiting Amplifier and Laser/Modulator Driver in 0.18um CMOS Technology,” IEEE Journal of Solid-State Circuits, vol. 38, pp. 2138-2146, Dec. 2003.  [[https://www.seas.ucla.edu/brweb/papers/Journals/G&RDec03_2.pdf](https://www.seas.ucla.edu/brweb/papers/Journals/G&RDec03_2.pdf)]



## Flipped Voltage Follower (FVF)

![image-20240921110019881](afe/image-20240921110019881.png)

![image-20240921113630249](afe/image-20240921113630249.png)

**T&H buffer in ADC**

![image-20240923200147070](afe/image-20240923200147070.png)


> [[https://www.linkedin.com/posts/chembiyan-t-0b34b910_flipped-voltage-follower-fvf-basics-activity-7118482840803020800-qwyX?utm_source=share&utm_medium=member_desktop](https://www.linkedin.com/posts/chembiyan-t-0b34b910_flipped-voltage-follower-fvf-basics-activity-7118482840803020800-qwyX?utm_source=share&utm_medium=member_desktop)]
>
> Z. Guo et al., "A 112.5Gb/s ADC-DSP-Based PAM-4 Long-Reach Transceiver with >50dB Channel Loss in 5nm FinFET," 2022 IEEE International Solid-State Circuits Conference (ISSCC), San Francisco, CA, USA, 2022, pp. 116-118, doi: 10.1109/ISSCC42614.2022.9731650.



## Super-source follower (SSF)

![image-20240924213742877](afe/image-20240924213742877.png)

![image-20240924213845608](afe/image-20240924213845608.png)

![image-20240924213853954](afe/image-20240924213853954.png)

> A. Sheikholeslami, "Voltage Follower, Part III [Circuit Intuitions]," in *IEEE Solid-State Circuits Magazine*, vol. 15, no. 2, pp. 14-26, Spring 2023, doi: 10.1109/MSSC.2023.3269457
>
> Paul R. Gray. 2009. Analysis and Design of Analog Integrated Circuits (5th. ed.). Wiley Publishing.





## Double differential Pair

$V_\text{ip}$ and $V_\text{im}$ are input, $V_\text{rp}$ and $V_\text{rm}$ are reference voltage
$$
V_o = A_v(\overline{V_\text{ip} - V_\text{im}} - \overline{V_\text{rp} - V_\text{rm}})
$$


![2diffpair.drawio](afe/2diffpair.drawio.svg)

In differential comparison mode, the feedback loop ensure $V_\text{ip} = V_\text{rp}$, $V_\text{im} = V_\text{rm}$ in the end 

> assume input and reference common voltage are **same**

Pros of *(b)*

- larger input range i.e.,  $\gt \pm \sqrt{2}V_\text{ov}$ of *(a)*, it works even one differential is off due to lower voltage
- larger $g_m$ (smaller input difference of pair)

Cons of *(b)*

- sensitive to the difference of common voltage between $V_\text{ip}$,  $V_\text{im}$ and  $V_\text{rp}$,  $V_\text{rm}$



## peaking without inductor

*TODO* &#128197;

> How to generate **complex poles without inductor**? [[https://a2d2ic.wordpress.com/2020/02/19/basics-on-active-rc-low-pass-filters/](https://a2d2ic.wordpress.com/2020/02/19/basics-on-active-rc-low-pass-filters/)]


## mismatch of pair add & subtract

![diff_mismatch_connect.drawio](afe/diff_mismatch_connect.drawio.svg)


$$\begin{align}
I_{add} &= g_m(\sigma_{vth,0} + \sigma_{vth,1}) \\
I_{sub} &= g_m(\sigma_{vth,0} - \sigma_{vth,1})
\end{align}$$

The input equivalient offset voltage
$$\begin{align}
V_{os,add} &= \frac{I_{add}}{2g_m} = \frac{\sigma_{vth,0} + \sigma_{vth,1}}{2} \\
V_{os,sub} &= \frac{I_{sub}}{g_m} = \sigma_{vth,0} - \sigma_{vth,1}
\end{align}$$

Then
$$\begin{align}
\sigma_{vos,add} &= \sqrt{\frac{2\sigma_{vth}^2}{4}} = \frac{\sigma_{vth}}{\sqrt{2}} \\
\sigma_{vos,sub} &= \sqrt{2\sigma_{vth}^2} = \sqrt{2}\sigma_{vth}
\end{align}$$

We obtain
$$
\sigma_{vos,sub} = 2\sigma_{vos,add}
$$


## reference

Elad Alon, ISSCC 2014, "T6: Analog Front-End Design for Gb/s Wireline Receivers" [[https://picture.iczhiku.com/resource/eetop/wHKfZPYpAleAKXBV.pdf](https://picture.iczhiku.com/resource/eetop/wHKfZPYpAleAKXBV.pdf)]

Byungsub Kim,  ISSCC 2022, "T11: Basics of Equalization Techniques: Channels, Equalization, and Circuits"

Minsoo Choi et al., "An Approximate Closed-Form Channel Model for Diverse Interconnect Applications," IEEE Transactions on Circuits and Systems-I: Regular Papers, vol. 61, no. 10, pp. 3034-3043, Oct. 2014.

