---
title: Delta-Sigma Modulator
date: 2024-09-08 16:48:32
tags:
categories:
- analog
mathjax: true
---



The average output of DSM tracks the input signal

$\Delta\Sigma$ modulators are **nonlinear systems** since a **quantizer** is implemented in the $\Delta\Sigma$-loop

---

![image-20241123140116340](delta-sigma/image-20241123140116340.png)



## No delay-free loops

![image-20241128232040924](delta-sigma/image-20241128232040924.png)

> Both integrator and quantizer are delay free  

NTF realizability criterion: No delay-free loops in the modulator



> ![image-20241128233022231](delta-sigma/image-20241128233022231.png)



## linear settling & GBW of amplifier

*TODO* &#128197;

Switched capacitor has been the common realization technique of *discrete-time (DT) modulators*, and in order to achieve a **linear settling**, the *sampling frequency* used in these converters needs to be *significantly lower than the gain bandwidth product (GBW) o*f the amplifiers. 



## Delta Modulator

![image-20240908173930949](delta-sigma/image-20240908173930949.png)

$$\begin{align}
(V_{in} - V_F) &= D_{out} \\
D_{out} &= s V_F
\end{align}$$

Therefore $V_{in} - \frac{D_{out}}{s} = D_{out}$
$$
D_{out} = \frac{s}{s+1} V_{in}
$$


> attenuates the low-frequency content of the signal, and amplifies high-frequency noise.



## MOD1

![image-20241005120659945](delta-sigma/image-20241005120659945.png)
$$
V(z) = U(z) +(1-z^{-1})E(z)
$$


- A binary DAC (and hence a binary modulator) is inherently linear
- With a CT loop filter, MOD1 has inherent anti-alising



---

![image-20241005202024498](delta-sigma/image-20241005202024498.png)
$$\begin{align}
v[1] &= u  - (0) + e[1] \\
v[2] &= 2u - (v[1]) + e[2] \\
v[3] &= 3u - (v[1]+v[2]) + e[3] \\
v[4] &= 4u - (v[1]+v[2]+v[3]) + e[4]
\end{align}$$

That is
$$
v[n] = nu - \sum_{k=1}^{n-1}v[k] + e[n]
$$
Therefore, we have $v[n-1] = (n-1)u - \sum_{k=1}^{n-2}v[k] + e[n-1]$, then
$$\begin{align}
v[n] &= nu - \sum_{k=1}^{n-1}v[k] + e[n] \\
&= u + \left((n-1)u - \sum_{k=1}^{n-2}v[k]\right) - v[n-1] + e[n] \\
&= u + v[n-1] - e[n-1]  -v[n-1] + e[n] \\
&= u + e[n] - e[n-1]
\end{align}$$



---

![image-20250524215712688](delta-sigma/image-20250524215712688.png)

Dout, the low frequency component of ADC out is same with Vin



## MOD2

![image-20241005160203074](delta-sigma/image-20241005160203074.png)





## decimation filter

The combination of the the *digital post-filter* and *downsampler* is called the **decimation filter** or **decimator**

![image-20241015220921002](delta-sigma/image-20241015220921002.png)

###  $\text{sinc}$ filter



![image-20241015215159577](delta-sigma/image-20241015215159577.png)

![image-20241015215227042](delta-sigma/image-20241015215227042.png)

> ![image-20241015225859710](delta-sigma/image-20241015225859710.png)



![image-20241015215111430](delta-sigma/image-20241015215111430.png)



### $\text{sinc}^2$ filter

![image-20241015220030204](delta-sigma/image-20241015220030204.png)



> [https://classes.engr.oregonstate.edu/eecs/spring2021/ece627/Lecture%20Notes/First-Order_D-S_ADC_Scan2.pdf](https://classes.engr.oregonstate.edu/eecs/spring2021/ece627/Lecture%20Notes/First-Order_D-S_ADC_Scan2.pdf)
>
> [https://classes.engr.oregonstate.edu/eecs/spring2017/ece627/Lecture%20Notes/First-Order%20D-S%20ADC.pdf](https://classes.engr.oregonstate.edu/eecs/spring2017/ece627/Lecture%20Notes/First-Order%20D-S%20ADC.pdf)



## Truncation DAC

![image-20241022204239594](delta-sigma/image-20241022204239594.png)

---



![image-20241019220819728](delta-sigma/image-20241019220819728.png)

An implementation of a **high-resolution integral path** using a *digital delta-sigma modulator*, *low-resolution Nyquist DAC*, and *a lowpass filter*

- $\Delta \Sigma$ truncates $n$-bit accumulator output to $m$-bits with $m\le n$
- A $m$-bit Nyquist DAC outputs current, which is fed into a low pass filter that suppresses $\Delta \Sigma$'s quantization noise





---

![image-20241022233749243](delta-sigma/image-20241022233749243.png)



The remaining *11 bits are truncated to 3-levels* using a second-order delta-sigma modulator (DSM), thus, obviating the need for a high resolution DAC



> Hanumolu, Pavan Kumar. "Design techniques for clocking high performance signaling systems" [[https://ir.library.oregonstate.edu/concern/graduate_thesis_or_dissertations/1v53k219r](https://ir.library.oregonstate.edu/concern/graduate_thesis_or_dissertations/1v53k219r)]



## Mismatch Shaping

![image-20241112220458335](delta-sigma/image-20241112220458335.png)



### Data-Weighted Averaging (DWA)

![image-20241113000942025](delta-sigma/image-20241113000942025.png)
$$\begin{align}
\sum_{i=0}^{n}v[i] + e_\text{DAC}[n] &= y[n] \\
\sum_{i=0}^{n-1}v[i] + e_\text{DAC}[n-1] &= y[n-1]
\end{align}$$

and we have $w[n] = y[n] - y[n-1]$, then
$$
w[n] = v[n] + e_\text{DAC}[n] - e_\text{DAC}[n-1]
$$
i.e.
$$
W = V + (1-z^{-1})e_\text{DAC}
$$





**Element Rotation:**

![image-20241112233059745](delta-sigma/image-20241112233059745.png)



> [[http://individual.utoronto.ca/schreier/lectures/12-2.pdf](http://individual.utoronto.ca/schreier/lectures/12-2.pdf)], [[http://individual.utoronto.ca/trevorcaldwell/course/Mismatch.pdf](http://individual.utoronto.ca/trevorcaldwell/course/Mismatch.pdf)]


## idle tone & dithering

**ditherin** break *periodicity* and convert them to noise while input is *constant*


## Fractional-N PLL

page13

$$
\tau[n-1] + (N+y[n])T_{PLL} - (N+\alpha)T_{PLL} = \tau[n]
$$

i.e.
$$
\tau[n] = \tau[n-1] + (y[n] - \alpha)T_{PLL}
$$

where $\tau[n] = t_{vdiv} -  t_{vdiv, desired}$ 



## reference

R. Schreier, ISSCC2006 tutorial: Understanding Delta-Sigma Data Converters

Shanthi Pavan, ISSCC2013 T5: Simulation Techniques in Data Converter Design [[https://www.nishanchettri.com/isscc-slides/2013%20ISSCC/TUTORIALS/ISSCC2013Visuals-T5.pdf](https://www.nishanchettri.com/isscc-slides/2013%20ISSCC/TUTORIALS/ISSCC2013Visuals-T5.pdf)]

Bruce A. Wooley , 2012, "The Evolution of Oversampling Analog-to-Digital Converters" [[https://r6.ieee.org/scv-sscs/wp-content/uploads/sites/80/2012/06/Oversampling-Wooley_SCV-ver2.pdf](https://r6.ieee.org/scv-sscs/wp-content/uploads/sites/80/2012/06/Oversampling-Wooley_SCV-ver2.pdf)]

B. Razavi, "The Delta-Sigma Modulator [A Circuit for All Seasons]," IEEE Solid-State Circuits Magazine, Volume. 8, Issue. 20, pp. 10-15, Spring 2016. [[http://www.seas.ucla.edu/brweb/papers/Journals/BRSpring16DeltaSigma.pdf](http://www.seas.ucla.edu/brweb/papers/Journals/BRSpring16DeltaSigma.pdf)]

Pavan, Shanthi, Richard Schreier, and Gabor Temes. (2016) 2016. Understanding Delta-Sigma Data Converters. 2nd ed. Wiley.

---

Richard E. Schreier, ECE 1371 Advanced Analog Circuits - 2015 [[http://individual.utoronto.ca/schreier/ece1371-2015.html](http://individual.utoronto.ca/schreier/ece1371-2015.html)]

Gabor C. Temes. ECE 627-Oversampled Delta-Sigma Data Converters [[https://classes.engr.oregonstate.edu/eecs/spring2017/ece627/lecturenotes.html](https://classes.engr.oregonstate.edu/eecs/spring2017/ece627/lecturenotes.html)]

Boris Murmann, ISSCC2022 SC1: Introduction to ADCs/DACs: Metrics, Topologies, Trade Space, and Applications [[link](【SC1.Introduction.to.ADCs.DACs.Metrics.Topologies.Trade.Space.and.Applications】 https://www.bilibili.com/video/BV1ENxxedEio/?share_source=copy_web&vd_source=5a095c2d604a5d4392ea78fa2bbc7249)]

Ian Galton. Delta-Sigma Fractional-N Phase-Locked Loops [[https://ispg.ucsd.edu/wordpress/wp-content/uploads/2022/10/fnpll_ieee_tutorial_2003_corrected.pdf](https://ispg.ucsd.edu/wordpress/wp-content/uploads/2022/10/fnpll_ieee_tutorial_2003_corrected.pdf)]

Sudhakar Pamarti. CICC 2020: Basics of Closed- and Open-Loop Fractional Frequency Synthesis [[https://youtu.be/t1TY-D95CY8?si=tbav3J2yag38HyZx](https://youtu.be/t1TY-D95CY8?si=tbav3J2yag38HyZx)]

