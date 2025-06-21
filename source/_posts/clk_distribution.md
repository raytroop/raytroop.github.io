---
title: Clock Distribution Techniques
date: 2022-05-16 00:39:22
tags:
categories:
- noise
mathjax: true
---

![image-20220516004008878](clk_distribution/image-20220516004008878.png)

## Deterministic Jitter

![image-20220516004058916](clk_distribution/image-20220516004058916.png)

![image-20220516004206118](clk_distribution/image-20220516004206118.png)

`j_Djpp` can be calculated by PSD,too

![image-20220516004615033](clk_distribution/image-20220516004615033.png)

```matlab
fck = 38.4e6;
Nfft = 15000;
fres = fck/Nfft;
psddBc = -99.3343;
psBc = psddBc + 10*log10(fres);	% psd -> ps; 
phrad2 = 10^(psBc/10);
phrms = sqrt(phrad2);
Jrms = phrms/2/pi*1/fck;
Jpp = 2*sqrt(2)*Jrms;
```

```
Jpp =

   6.4038e-12
```

For DJ, we usually use peak to peak value

> BTW, the psd value at half of fundamental frequency ($f_s/2$) is ~~duty cycle distortion due to the NMOS/PMOS imbalance~~, *because of rising only data*



## Random Jitter

RJ can be accurately and efficiently measured using **PSS/Pnoise** or **HB/HBnoise**.  

Note that the **transient noise** can also be used to compute RJ; 

> However, the computation cost is typically very high, and the accuracy is lesser as compared to PSS/Pnoise and HB/HBnoise.

Since RJ follows a Gaussian distribution, it can be fully characterized using its Root-Mean-Squared value (RMS) or the standard deviation value ($\sigma$)

The Peak-to-Peak value of RJ ($\text{RJ}_{\text{p-p}}$) can be calculated under certain observation conditions
$$
\text{RJ}_{\text{p-p}}\equiv K \ast \text{RJ}_{\text{RMS}}
$$
Here, $K$ is a constant determined by the BER specification of the system given in the following Table

| BER        | Crest factor (K) |
| ---------- | ---------------- |
| $10^{-3}$  | 6.18             |
| $10^{-4}$  | 7.438            |
| $10^{-5}$  | 8.53             |
| $10^{-6}$  | 9.507            |
| $10^{-7}$  | 10.399           |
| $10^{-8}$  | 11.224           |
| $10^{-9}$  | 11.996           |
| $10^{-10}$ | 12.723           |
| $10^{-11}$ | 13.412           |
| $10^{-12}$ | 14.069           |
| $10^{-13}$ | 14.698           |

```matlab
K = 14.698;
Ks = K/2;
p = normcdf([-Ks Ks]);
BER = 1 - (p(2)-p(1));
```

```
BER =

   1.9962e-13
```



![image-20220516160050961](clk_distribution/image-20220516160050961.png)



![image-20220516193125490](clk_distribution/image-20220516193125490.png)

## Total Jitter

$$
\text{TJ}_{\text{p-p}}\equiv \text{DJ}_{\text{p-p}} + \text{RJ}_{\text{p-p}}(\text{BER})
$$

![tj.drawio](clk_distribution/tj.drawio.svg)

![image-20220516160006909](clk_distribution/image-20220516160006909.png)

![image-20220516012200383](clk_distribution/image-20220516012200383.png)

> In the psd of TJ, the spur is DJ and floor is RJ



## Phase Noise to Jitter

The **phase noise** is traditionally defined as the ratio of the power of the signal in 1Hz bandwidth at offset $f$ from the carrier $P$,
divided by the power of the carrier
$$
\ell (f) = \frac {S_v'(f_0+f)}{P}
$$
where $S_v'$ is is **one-sided voltage PSD** and $f \geqslant 0$

Under **narrow angle assumption**
$$
S_{\varphi}(f)= \frac {S_v'(f_0+f)}{P}
$$
where $\forall f\in \left[-\infty +\infty\right]$

Using the Wiener-Khinchin theorem, it is possible to easily derive the variance of the absolute jitter($J_{ee}$)via integration of the corresponding PSD
$$
J_{ee,rms}^2 = \int S_{J_{ee}}(f)df
$$

And we know the relationship between absolute jitter and excess phase is
$$
J_{ee}=\frac {\varphi}{\omega_0}
$$
Considering that phase noise is normally symmetrical about the zero frequency, multiplied by **two** is shown as below
$$
J_{ee,rms} = \frac{\sqrt{2\int_{0}^{+\infty}\ell(f)df}}{\omega_0}
$$
where phase noise is in linear units not in logarithmic ones.

Because the unit of phase noise in *Spectre-RF* is logarithmic unit (*dBc*), we have to convert the unit before applying the above equation
$$
\ell[linear] = 10^{\frac {\ell [dBc/Hz]}{10}}
$$
The complete equation using the simulation result of *Spectre-RF Pnoise* is
$$
J_{ee,rms} = \frac{\sqrt{2\int_{0}^{+\infty}10^{\frac {\ell [dBc/Hz]}{10}}df}}{\omega_0}
$$

The above equation has been verified for *sampled pnoise*, i.e.  *J<sub>ee</sub>* and *Edge Phase Noise*.

> - For **pnoise-sampled(jitter)**, *Direct Plot Form - Function: Jee:Integration Limits* can calculate it conveniently
> - But for **pnoise-timeaveage**, you have to use the below equation to get RMS jitter.

One example, integrate to $\frac{f_{osc}}{2}$ and $f_{osc} = 16GHz$

![image-20220415100034220](clk_distribution/image-20220415100034220.png)



Of course, it apply to conventional pnoise simulation.

On the other hand, output rms voltage noise, $V_{out,rms}$ divied by slope should be close to $J_{ee,rms}$
$$
J_{ee,rms} = \frac {V_{out,rms}}{slope}
$$


## Pulse Width Jitter (PWJ)

*TODO* &#128197;


> [[Spectre Tech Tips: Measuring Noise in Digital Circuits](https://community.cadence.com/cadence_blogs_8/b/cic/posts/spectre-tech-tips-measuring-noise-in-digital-circuits)]

**Pnoise sampled: Edge Delay mode** measures the noise defined by two edges. Both edges are defined by a threshold voltage and rising or falling edges, which measures the noise of the pulse itself and direct plot calculate the variation of the **pulse width**



## Power supply induced jitter (PSIJ)

A **sampled pxf** analysis can be used to simulate the *deterministic jitter* of a circuit due to *power supply ripple*

*TODO* &#128197;



## DCC Correction

The amount of correction can be set by intentional injection of an *offset current* into the summing input node of INV, ***threshold-adjustable inverter***

> Note that the change to the threshold is ***opposite in direction*** to the change to INV
>
> increasing DC of input signal is equivalent to lower down the threshold of INV

![image-20241215233057176](clk_distribution/image-20241215233057176.png)



---

![image-20241216205525818](clk_distribution/image-20241216205525818.png)

voltage at *INV1* will increased by:
$$
\frac{\Delta V_{DAC} - \Delta {INV1}}{R_{DAC}} = \frac{\Delta {INV1} +A_0 \Delta {INV1}}{R_{F}}
$$
therefore
$$
\Delta {INV1} = \Delta V_{DAC} \cdot \frac{R_F}{R_F+(A_0+1)R_{DAC}} \approx  \Delta V_{DAC} \cdot \frac{R_F}{A_0R_{DAC}}
$$

If $R_{DAC} = R_F$
$$
\Delta {INV1}\approx \frac{\Delta V_{DAC}}{A_0}
$$

> C. Menolfi *et al*., "A 112Gb/S 2.6pJ/b 8-Tap FFE PAM-4 SST TX in 14nm CMOS," *2018 IEEE International Solid-State Circuits Conference - (ISSCC)* [[https://sci-hub.se/https://doi.org/10.1109/ISSCC.2018.8310205](https://sci-hub.se/https://doi.org/10.1109/ISSCC.2018.8310205)]
>
> Bob Lefferts, Navraj Nandra. SNUG Israel 2007 [[https://picture.iczhiku.com/resource/eetop/whKYwQorwYoPUVbm.pdf](https://picture.iczhiku.com/resource/eetop/whKYwQorwYoPUVbm.pdf)]
>
> C. Menolfi *et al*., "A 112Gb/S 2.6pJ/b 8-Tap FFE PAM-4 SST TX in 14nm CMOS," *2018 IEEE International Solid-State Circuits Conference - (ISSCC)*, San Francisco, CA, USA, 2018 [[https://picture.iczhiku.com/resource/eetop/shiGDYTDYikLlnXv.pdf](https://picture.iczhiku.com/resource/eetop/shiGDYTDYikLlnXv.pdf)]





## reference

Article (20500632) Title: How to simulate Random and Deterministic Jitters URL: https://support.cadence.com/apex/ArticleAttachmentPortal?id=a1O3w000009fiXeEAI

Spectre Tech Tips: Measuring Noise in Digital Circuits - Analog/Custom Design - Cadence Blogs - Cadence Community [https://community.cadence.com/cadence_blogs_8/b/cic/posts/s . . .](https://community.cadence.com/cadence_blogs_8/b/cic/posts/spectre-tech-tips-measuring-noise-in-digital-circuits)

Cadence RAK: Deterministic Jitter Measurement using SpectreRF

Frank Wiedmann. Using sampled pxf analysis to simulate deterministic jitter [[https://community.cadence.com/cadence_technology_forums/f/custom-ic-design/51605/using-sampled-pxf-analysis-to-simulate-deterministic-jitter](https://community.cadence.com/cadence_technology_forums/f/custom-ic-design/51605/using-sampled-pxf-analysis-to-simulate-deterministic-jitter)]

supply noise sensitivity: PSS+PAC or PSS+PX [[https://designers-guide.org/forum/YaBB.pl?num=1376500816](https://designers-guide.org/forum/YaBB.pl?num=1376500816)]

---

J. Kim et al., "A 112 Gb/s PAM-4 56 Gb/s NRZ Reconfigurable Transmitter With Three-Tap FFE in 10-nm FinFET," in IEEE Journal of Solid-State Circuits, vol. 54, no. 1, pp. 29-42, Jan. 2019, doi: 10.1109/JSSC.2018.2874040

— et al., "A 224-Gb/s DAC-Based PAM-4 Quarter-Rate Transmitter With 8-Tap FFE in 10-nm FinFET," in IEEE Journal of Solid-State Circuits, vol. 57, no. 1, pp. 6-20, Jan. 2022, doi: 10.1109/JSSC.2021.3108969

---

J. N. Tripathi, V. K. Sharma and H. Shrimali, "A Review on Power Supply Induced Jitter," in IEEE Transactions on Components, Packaging and Manufacturing Technology, vol. 9, no. 3, pp. 511-524, March 2019 [[https://sci-hub.st/10.1109/TCPMT.2018.2872608](https://sci-hub.st/10.1109/TCPMT.2018.2872608)]

H. Kim, J. Fan and C. Hwang, "Modeling of power supply induced jitter (PSIJ) transfer function at inverter chains," 2017 IEEE International Symposium on Electromagnetic Compatibility & Signal/Power Integrity (EMCSI), Washington, DC, USA, 2017 [[https://sci-hub.st/10.1109/ISEMC.2017.8077937](https://sci-hub.st/10.1109/ISEMC.2017.8077937)]

Yin Sun, Chulsoon Hwang EMC Laboratory. Improving Power Supply Induced Jitter Simulation Accuracy for IBIS Model [[https://ibis.org/summits/aug20/sun.pdf](https://ibis.org/summits/aug20/sun.pdf)]

High Speed Communications Part 8 – On Die CMOS Clock Distribution. [[https://youtu.be/nx5CiHcwrF0?si=-eSO-LaaaFrVuIA1](https://youtu.be/nx5CiHcwrF0?si=-eSO-LaaaFrVuIA1)]

Low-Jitter CMOS Clock Distribution [[https://youtu.be/LMT-T41Y64U?si=y8IpWCtU90zpe4Ob](https://youtu.be/LMT-T41Y64U?si=y8IpWCtU90zpe4Ob)]

Mo, Xunjun & Wu, Jiaqi & Wary, Nijwm & Carusone, Tony. (2021). Design Methodologies for Low-Jitter CMOS Clock Distribution. IEEE Open Journal of the Solid-State Circuits Society. 1. 94-103. 10.1109/OJSSCS.2021.3117930. [[https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=9559395](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=9559395)]

---

Mozhgan Mansuri. ISSCC2021 SC3: Clocking, Clock Distribution, and Clock Management in Wireline/Wireless Subsystems [[[Clocking, Clock Distribution, and Clock Management in Wireline/Wireless Subsystems](https://www.nishanchettri.com/isscc-slides/2021 ISSCC/SHORT COURSE/ISSCC2021-SC3.pdf)]([Clocking, Clock Distribution, and Clock Management in Wireline/Wireless Subsystems](https://www.nishanchettri.com/isscc-slides/2021 ISSCC/SHORT COURSE/ISSCC2021-SC3.pdf))]

Phillip Restle. ISSCC2021 SC4: Processor Clock Generation, Distribution, and Clock Sensor/Management Loops [[https://www.nishanchettri.com/isscc-slides/2021%20ISSCC/SHORT%20COURSE/ISSCC2021-SC4.pdf](https://www.nishanchettri.com/isscc-slides/2021%20ISSCC/SHORT%20COURSE/ISSCC2021-SC4.pdf)]

Sam Palermo. Spring 2025 ECEN720 : High-Speed Links Circuits and Systems [[Lecture 14: Clock Distribution Techniques](https://people.engr.tamu.edu/spalermo/ecen689/lecture14_ee720_clk_distribution.pdf)]

