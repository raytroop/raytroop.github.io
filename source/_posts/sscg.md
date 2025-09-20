---
title: Spread Spectrum Clocking (SSC)
date: 2025-08-30 22:17:12
tags:
categories:
- dsp
mathjax: true
---

***spread spectrum clock generation (SSCG)*** — an advanced clock generation solution for ***electromagnetic interference (EMI)***

![image-20250913195157852](sscg/image-20250913195157852.png)

![image-20250913192850807](sscg/image-20250913192850807.png)

![image-20250913192820120](sscg/image-20250913192820120.png)

## SSC modulation profile

> [[https://www.synopsys.com/blogs/chip-design/understanding-pcie-spread-spectrum-clocking.html](https://www.synopsys.com/blogs/chip-design/understanding-pcie-spread-spectrum-clocking.html)]

The most common modulation techniques are down-spread and center-spread:

- ***Down-spread***: Carrier is modulated to lower than nominal frequency by specified percentage, and not higher

- ***Center-spread***: Carrier is modulated both higher and lower than nominal frequency by specified percentage

![image-20250913194151764](sscg/image-20250913194151764.png)



##  SSCG Architectures

> K. -H. Cheng, C. -L. Hung, C. -H. Chang, Y. -L. Lo, W. -B. Yang and J. -W. Miaw, "A Spread-Spectrum Clock Generator Using Fractional-N PLL Controlled Delta-Sigma Modulator for Serial-ATA III," *2008 11th IEEE Workshop on Design and Diagnostics of Electronic Circuits and Systems*, Bratislava, Slovakia, 2008 [[https://sci-hub.se/10.1109/DDECS.2008.4538758](https://sci-hub.se/10.1109/DDECS.2008.4538758)]

![image-20250903230209570](sscg/image-20250903230209570.png)





## Refclk Clocking Architectures

> PCI Express Base Specification Revision *3.0*
>
> Jeff Morriss, Intel Gerry Talbot, AMD. PCI-SIG Devcon 2006. Jitter Budgeting for Clock Architecture
>
> Verification of SRIS/SRNS Clocking [[https://www.esaindia.com/emailer/download/sria-srns-white-paper-final-v3.pdf](https://www.esaindia.com/emailer/download/sria-srns-white-paper-final-v3.pdf)]



### Common Reference Clock (CC)

Common Refclk Rx architectures are characterized by the Tx and Rx sharing the same Refclk source

Most of the SSC jitter sourced by the Refclk is propagated equally through Tx and Rx PLLs, and so intrinsically tracks ***LF jitter***

The amount of jitter appearing at the CDR is then defined by the difference function between the Tx and Rx PLLs multiplied by the ***CDR highpass characteristic***

![image-20250719172803394](sscg/image-20250719172803394.png)
$$
H(s)= H_1(s)e^{-sT} -  \left[H_1(s)e^{-sT}(1-H_3(s)) + H_2(s)H_3(s) \right] = [H_1(s)e^{-sT} -H_2(s)]H_3(s)
$$
where $H_3(s)$ is similar to $NTF_{VCO}$, $1-H_3(s)$ is similar to $NTF_{REF}$



> ![image-20250719181032685](sscg/image-20250719181032685.png)



---

![image-20250814011504270](sscg/image-20250814011504270.png)

### Data Clocked Refclk Rx Architecture

A data clocked Rx architecture is characterized by requiring the *receiver's CDR to track the entirety of the low frequency jitter, including SSC*

![image-20250719183101724](sscg/image-20250719183101724.png)



### Separate Reference Clocks with SSC (SRIS) 

> TITLE: Separate Refclk Independent SSC Architecture (SRIS)
> DATE: Updated 10 January 2013
> AFFECTED DOCUMENT: PCI Express Base Spec. Rev. 3.0
> SPONSOR: Intel, HP, AMD

![image-20250719183242222](sscg/image-20250719183242222.png)
$$\begin{align}
X_{LATCH}(s) &= X_1(s)H_1(s) -  \left[X_1(s)H_1(s)(1-H_3(s)) + X_2(s)H_2(s)H_3(s) \right] \\
& = \left[X_1(s)H_1(s) -X_2(s)H_2(s)\right]H_3(s)
\end{align}$$
where $H_3(s)$ is similar to $NTF_{VCO}$, $1-H_3(s)$ is similar to $NTF_{REF}$

![image-20250719182447193](sscg/image-20250719182447193.png)

![image-20250719182517511](sscg/image-20250719182517511.png)



> ![image-20250719182123550](sscg/image-20250719182123550.png)
>
> ![image-20250719181221513](sscg/image-20250719181221513.png)

---

![image-20250719152821655](sscg/image-20250719152821655.png)

---

![image-20250814011411755](sscg/image-20250814011411755.png)

### Separate Reference Clocks with No SSC (SRNS) 

![image-20250814011354803](sscg/image-20250814011354803.png)



## reference

Jason Sachs. Linear Feedback Shift Registers for the Uninitiated, Part XII: Spread-Spectrum Fundamentals [[link](https://www.embeddedrelated.com/showarticle/1124.php)]

Jan Meel, [*Spread Spectrum (SS) — introduction*](http://www.sss-mag.com/pdf/Ss_jme_denayer_intro_print.pdf), De Nayer Instituut, Sint-Katelijne-Waver, Belgium, 1999.

Raymond L. Pickholtz, Donald L. Schilling, Laurence B. Milstein, [*Theory of Spread-Spectrum Communications — A Tutorial*](http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.114.208&rank=1), IEEE Transactions on Communications, vol. 30, no. 5, pp. 855-884, May 1982.

Kadeem Samuel. Application Note Clocking for PCIe Applications [[https://www.ti.com/lit/an/snaa386/snaa386.pdf?ts=1756864837383](https://www.ti.com/lit/an/snaa386/snaa386.pdf?ts=1756864837383)]

K. -H. Cheng, C. -L. Hung, C. -H. Chang, Y. -L. Lo, W. -B. Yang and J. -W. Miaw, "A Spread-Spectrum Clock Generator Using Fractional-N PLL Controlled Delta-Sigma Modulator for Serial-ATA III," *2008 11th IEEE Workshop on Design and Diagnostics of Electronic Circuits and Systems*, Bratislava, Slovakia, 2008 [[https://sci-hub.se/10.1109/DDECS.2008.4538758](https://sci-hub.se/10.1109/DDECS.2008.4538758)]

---

Rhee, W. (2020). *Phase-locked frequency generation and clocking : architectures and circuits for modern wireless and wireline systems*. The Institution of Engineering and Technology
