---
title: Jitter
date: 2023-09-16 23:48:05
tags:
categories:
- noise
mathjax: true
---

![image-20250816004521416](jitter/image-20250816004521416.png)



![image-20250816003816639](jitter/image-20250816003816639.png)

## Phase Noise to Jitter

> Note that $L(f )$ is defined over positive frequencies only $(f \ge 0)$

![image-20250902231037546](jitter/image-20250902231037546.png)

> for simple PLL
>
> For small $N$: $\sigma_{p(N)}^2 \approx \frac{\mathcal{L}_0 f_{3dB}}{2\pi f_0^2} \cdot \frac{2\pi f_{3dB}N}{f_0}=\frac{\mathcal{L}_0f_{3dB}^2}{f_0^3}=\sigma_{PER}^2$
>
> For large $N$:  $\sigma_{p(N)}^2 \approx \frac{\mathcal{L}_0f_{3dB}^2}{f_0^3} \cdot \frac{f_0}{2\pi f_{3dB}}=\sigma_{PER}^2\cdot \frac{f_0}{2\pi f_{3dB}}$
>
> | Free Running  OSC                                      | OSC in  simple PLL                                           |
> | ------------------------------------------------------ | ------------------------------------------------------------ |
> | $\mathcal{L}(f) = \frac{\mathcal{L}_0 f_{3dB}^2}{f^2}$ | $\mathcal{L}(f) = \frac{\mathcal{L}_0 f_{3dB}^2}{f^2 + f_{3dB}^2}$ |



---

![image-20250901224816795](jitter/image-20250901224816795.png)
$$\begin{align}
S_{jACC(N)}(f) &= |1-z^{-N}|^2\cdot S_{jABS}(f) \\
&= |1-\cos\theta +j\sin\theta|^2\cdot S_{jABS}(f) = ((1-\cos\theta)^2 + \sin^2\theta)\cdot S_{jABS}(f) \\
&= 2(1-\cos\theta)\cdot S_{jABS}(f) = 4\sin^2(\theta/2)\cdot S_{jABS}(f)
\end{align}$$

where $\theta = 2\pi f N/f_0$

![image-20250901233055582](jitter/image-20250901233055582.png)


As EQ(3.44), EQ(3.45)

the autocorrelation is the inverse Fouer transform of the PSD

$$
R_{\varphi}(t) = \int_{-\infty}^{+\infty} S_{\varphi} (f) e^{j2\pi f t} df
$$

Then,
$$\begin{align}
R_{\varphi}(0) &= \int_{-\infty}^{+\infty} S_{\varphi} (f)  df \\
R_{\varphi}(NT_0) &= \int_{-\infty}^{+\infty} S_{\varphi} (f)   e^{j2\pi f NT_0} df
\end{align}$$

Thus, yield EQ(3.48)

![image-20250903184827248](jitter/image-20250903184827248.png)



---

***Simplified PLL Phase Noise Profile***



***Absolute Jitter***

*TODO* &#128197;



 ***Period Jitter***

![image-20251218232426501](jitter/image-20251218232426501.png)

---

![image-20250901233626772](jitter/image-20250901233626772.png)

![image-20250901233756765](jitter/image-20250901233756765.png)

---

**a random-walk DCO - $1/f^2$ Phase Noise Profile**

> L. Avallone, M. Mercandelli, A. Santiccioli, M. P. Kennedy, S. Levantino and C. Samori, "A Comprehensive Phase Noise Analysis of Bang-Bang Digital PLLs," in IEEE Transactions on Circuits and Systems I: Regular Papers, vol. 68, no. 7, pp. 2775-2786, July 2021 [[https://sci-hub.st/10.1109/TCSI.2021.3072344](https://sci-hub.st/10.1109/TCSI.2021.3072344)]

![image-20250902232230515](jitter/image-20250902232230515.png)

> ![image-20250902231843251](jitter/image-20250902231843251.png)

---

> Mozhgan Mansuri “Low-Power Low-Jitter On-Chip Clock Generation” thesis UCLA [[https://people.engr.tamu.edu/spalermo/ecen689/pll_thesis_mansuri_ucla_2003.pdf](https://people.engr.tamu.edu/spalermo/ecen689/pll_thesis_mansuri_ucla_2003.pdf)]
>
> [[https://people.engr.tamu.edu/spalermo/ecen689/PRBS_&_PLL_model.pdf](https://people.engr.tamu.edu/spalermo/ecen689/PRBS_&_PLL_model.pdf)]

![image-20251218222327126](jitter/image-20251218222327126.png)




## Even-odd Jitter (EOJ)

| Jitter measurement | Description                                                  |
| :----------------- | :----------------------------------------------------------- |
| F/2                | F/2 is the peak-to-peak amplitude of the periodic jitter occurring at 1/2 of the data rate. |

**Even-odd jitter**, also known as **F/2 jitter**, arises from a clock signal's duty cycle not being perfectly 50%

![image-20250816130508935](jitter/image-20250816130508935.png)

> ***Even-odd jitter*** has been referred to as ***duty cycle distortion*** by other Physical Layer specifications for operation over electrical backplane or twinaxial copper cable assemblies



![image-20250816130650378](jitter/image-20250816130650378.png)

---

![image-20250816181004878](jitter/image-20250816181004878.png)

> Comparing DCD and F/2 Jitter Using a BERTScope® Bit Error Rate Testing Application Note [[https://download.tek.com/document/65W_26040_0_Letter.pdf](https://download.tek.com/document/65W_26040_0_Letter.pdf)]

## Pulse Width Jitter (PWJ)

![image-20250816125512147](jitter/image-20250816125512147.png)

![image-20250816125533070](jitter/image-20250816125533070.png)

> Jeff Morriss Updated 10/25/07. Analysis of 8G PCIe Pulse Width Jitter (*UI to UI Jitter_10_25.ppt*)



---

![image-20250816132730999](jitter/image-20250816132730999.png)



## Duty Cycle Distortion – DCD

![dcd.drawio](jitter/dcd.drawio.svg)

| Jitter measurement | Description                                                  |
| :----------------- | :----------------------------------------------------------- |
| DCD                | Duty Cycle Distortion is the peak-to-peak amplitude of the component of the deterministic jitter correlated with the signal polarity. |

![image-20250816081711834](jitter/image-20250816081711834.png)

![image-20250816081808897](jitter/image-20250816081808897.png)

---

> Jitter fundamental & How Isolating Root Causes of Jitter [[https://picture.iczhiku.com/resource/eetop/ShKgzTEiUfdFOcvn.pdf](https://picture.iczhiku.com/resource/eetop/ShKgzTEiUfdFOcvn.pdf)]

There are two primary causes of DCD jitter which are usually generated within a transmitter

-  If the data input to a transmitter is theoretically perfect, but if the ***transmitter sampling threshold*** is offset from its ideal level, then the output of transmitter will have duty cycle distortion as ***a function of the slew rate of the data signal*** 
- Another cause of duty cycle distortion can be a ***mismatch/asymmetry in rising and falling edge speeds***

![image-20250816085315710](jitter/image-20250816085315710.png)

---

Unfortunately, other sources such as ISI almost always exist making it sometimes difficult to isolate the DCD component. One technique to test for DCD is to stimulate your system/components with ***a repeating `1-0-1-0…` data pattern.*** This technique will eliminate inter-symbol interference (ISI) jitter and make viewing the DCD within the spectrum display much easier

> Why clock pattern? That's because all symbols experience ***same*** inter-symbol interference, which are canceled out

---

![image-20250816103444976](jitter/image-20250816103444976.png)

---

![image-20250816180338475](jitter/image-20250816180338475.png)

> [[https://scdn.rohde-schwarz.com/ur/pws/dl_downloads/dl_application/application_notes/1td03/1TD03_2e_RTO_Jitter_Analysis.pdf](https://scdn.rohde-schwarz.com/ur/pws/dl_downloads/dl_application/application_notes/1td03/1TD03_2e_RTO_Jitter_Analysis.pdf)]

## Correlated  vs. Uncorrelated

If the PDF of one jitter source changes when the PDF of another source is changed, then those two sources are ***dependent*** or ***correlated***

![image-20250816080432083](jitter/image-20250816080432083.png)





## Inter-Symbol Interference  (ISI)

The primary cause of Data Dependent Jitter

![image-20250816090326309](jitter/image-20250816090326309.png)

![image-20250816090430513](jitter/image-20250816090430513.png)

---



Jitter measurements can be classified into three categories: *cycle-to-cycle jitter*, *period jitter*, and *long-term jitter*

Jitter is a key performance parameter. Need to know what matters in each case: 

- *PJ* for digital timing
- *LTJ* for data converters and serial data
- *Phase noise* for communications (not all bandwidths matter)



![image-20240714095712249](jitter/image-20240714095712249.png)

> The above Cycle-Cycle Jitter equation is **wrong**,  $\tau_1$ and $\tau_2$ are not independent




##  Short Term Jitter

![image-20230916235240675](jitter/image-20230916235240675.png)

![image-20230916235314423](jitter/image-20230916235314423.png)

> **Period jitter**, *Jper* is the short term variation in clock period compared to the average (mean) clock period.
>
>  **Cycle-to-Cycle**, *Jcc* is the time difference of two adjacent clock periods





## Long Term Jitter (LTJ)

> [[https://people.engr.tamu.edu/spalermo/ecen689/PRBS_&_PLL_model.pdf](https://people.engr.tamu.edu/spalermo/ecen689/PRBS_&_PLL_model.pdf)]
>
> ***absolute jitter*** is also known as ***long-term jitter***
>
> ![image-20251218214812202](jitter/image-20251218214812202.png)

![image-20230916235647723](jitter/image-20230916235647723.png)

![image-20230916235709504](jitter/image-20230916235709504.png)

---

***measuring LTJ***

![image-20230916235033464](jitter/image-20230916235033464.png)

## Jitter Calculation Examples

![image-20230917003028143](jitter/image-20230917003028143.png)

## Jcc vs Jper

> Estimating the RMS cycle-to-cycle jitter if all you have available is the RMS period jitter.

- **Cycle-to-cycle jitter** - The *short-term* variation in clock period between *adjacent* clock cycles. This jitter measure, abbreviated here as $J_{CC}$, may be specified as either an RMS or peak-to-peak quantity.
- **Period jitter** - The *short-term* variation in clock period over *all* measured clock cycles, compared to the average clock period. This jitter measure, abbreviated here as $J_{PER}$, may be specified as either an RMS or peak-to-peak quantity.

Let the variable below represent the variance of a single edge's timing jitter, i.e. the difference in time of a jittery edge versus an ideal edge, $\sigma^2_j$

If each edge's jitter is *independent* then the variance of the period jitter can be written as
$$\begin{align}
\sigma^2_\text{jper} &= (\sigma_\text{j(n+1)}-\sigma_\text{j(n)})^2 \\
&= \sigma_\text{j(n+1)}^2-2\sigma_\text{j(n+1)}\sigma_\text{j(n)})+\sigma_\text{j(n)})^2\\
&= \sigma_\text{j(n+1)}^2+\sigma_\text{j(n)})^2 \\
&=2\sigma^2_j
\end{align}$$

In every cycle-to-cycle measurement we use one "**interior**" clock edge *twice* and therefore we must account for this

$$\begin{align}
\sigma^2_\text{jcc} &= (\sigma_\text{jper(n+1)}-\sigma_\text{jper(n)})^2 \\
&=(\sigma_\text{j(n+2)}-2\sigma_\text{j(n+1)}+\sigma_\text{j(n)})^2
\end{align}$$

Since each edge's jitter is assumed to be *independent* and have the same statistical properties we can drop the cross correlation terms and write:

$$\begin{align}
\sigma^2_\text{jcc} &=(\sigma_\text{j(n+2)}-2\sigma_\text{j(n+1)}+\sigma_\text{j(n)})^2 \\
&=\sigma_\text{j(n+2)}^2+4\sigma_\text{j(n+1)}^2+\sigma_\text{j(n)}^2 \\
&=6\sigma_\text{j}^2
\end{align}$$

The ratio of the variances is therefore
$$
\frac{\sigma^2_\text{jcc}}{\sigma^2_\text{jper}} = \frac{6\sigma_\text{j}^2} {2\sigma_\text{j}^2}=3
$$
Then
$$
\sigma_\text{jcc} = \sqrt{3}\sigma_\text{per}
$$

> [[Timing 101 #8: The Case of the Cycle-to-Cycle Jitter Rule of Thumb, Silicon Labs](https://community.silabs.com/s/share/a5U1M000000knzoUAA/timing-101-8-the-case-of-the-cycletocycle-jitter-rule-of-thumb?language=en_US)]



## references

AN10007 Clock Jitter Definitions and Measurement Methods, SiTime [[pdf](https://www.sitime.com/sites/default/files/hiddenresources/AN10007-Jitter-and-measurement-methods_SIT.pdf)]

SERDES Design and Simulation Using the Analog FastSPICE Platform, Silicon Creations [[pdf](https://www.siliconcr.com/sc-cms/uploads/u2u_presentation_sc_april25.pdf)]

Flexible clocking solutions in advanced processes from 180nm to 5nm, Silicon Creations [[pdf](https://www.siliconcr.com/sc-cms/uploads/siliconcreations_iccad_2019_v2_191020.pdf)]

One-size-fits-all PLLs for Advanced Samsung Foundry Processes, Silicon Creations [[pdf](https://www.siliconcr.com/sc-cms/uploads/siliconcreations_dac_2022_v2_22-07-12.pdf)]

Circuit Design and Verification of 7nm LowPower, Low-Jitter PLLs, Silicon Creations, [[pdf](https://www.siliconcr.com/sc-cms/uploads/u2u-2018-sicr-plls-v3-180509.pdf)]

Lecture 10: Jitter, ECEN720: High-Speed Links Circuits and Systems Spring 2023 [[pdf](https://people.engr.tamu.edu/spalermo/ecen689/lecture10_ee720_jitter.pdf)]

Jitter 360° Knowledge Series  [[pdf](https://ransomsnotes.com/index_htm_files/RansomStephensAndTektronixJitter360.pdf), [slides](https://picture.iczhiku.com/resource/eetop/WyiGPhKZaiWfoXxM.pdf)]

N. Da Dalt, "Tutorial: Jitter: Basic and Advanced Concepts, Statistics, and Applications," *2012 IEEE International Solid-State Circuits Conference*, San Francisco, CA, USA, 2012 [[slides](https://picture.iczhiku.com/resource/eetop/WhiryqaaRpqYeCxx.pdf), [transcript](https://picture.iczhiku.com/resource/eetop/WYifhqAAZphyFNcn.pdf) ]

