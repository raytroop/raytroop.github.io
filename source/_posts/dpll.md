---
title: Digital Phase-Locked Loops
date: 2025-05-13 17:30:16
tags:
categories:
- link
mathjax: true
---

## DPLL time-domain model

*TODO* &#128197;

## Hunting Jitter

***Hunting jitter*** is often referred to as ***dithering jitter***, the *periodic* time error between *data clock* and input data, which exhibits a ***limit-cycle*** behavior

![image-20250819202727871](dpll/image-20250819202727871.png)

![image-20250819203806711](dpll/image-20250819203806711.png)

![image-20250819210031102](dpll/image-20250819210031102.png)



## BB PD

> It's **ternary**, because *early*, *late* and *no transition*


### Linearing BB-PD

> Youngdon Choi, Deog-Kyoon Jeong and W. Kim, "Jitter transfer analysis of tracked oversampling techniques for multigigabit clock and data recovery," in IEEE Transactions on Circuits and Systems II: Analog and Digital Signal Processing, vol. 50, no. 11, pp. 775-783, Nov. 2003 [[https://sci-hub.st/10.1109/TCSII.2003.819070](https://sci-hub.st/10.1109/TCSII.2003.819070)]


The effective PD gain is a function of the **input jitter pdf**, it enables one to anticipate the effects of input jitter on loop characteristics


BB Gain is the slope of average BB output $\mu$, versus phase offset $\phi$, i.e. $\frac {\partial \mu}{\partial \phi}$,

BB only produces output for a transition and this de-rates the gain. Transition density = *0.5* for random data

$$
K_{BB} = \frac{1}{2}\frac {\partial \mu}{\partial \phi}
$$

where $\mu = (1)\times \mathrm{P}(\text{late}|\phi) + (-1)\times \mathrm{P}(\text{early}|\phi)$

![bb-PDF.drawio](dpll/bb-PDF.drawio.svg)


> Both jitter and amplitude noise distribution are same, just scaled by slope 


### Self-Noise Term

One price we pay for ***BB PD*** versus ***linear PD*** is the self-noise term. **For** **small phase errors** BB output noise is the **full magnitude** of the sliced data

> The PD output should be almost **0** for small phase errors. i.e. ideal PD output noise should be **0**

$$
\sigma_{BB}^2 = 1^2 \cdot \mathrm{P}(\text{trans}) + 0^2\cdot (1-\mathrm{P}(\text{trans})) = 0.5
$$

![image-20241127215947017](dpll/image-20241127215947017.png)

**Input referred jitter** from BB PD is **proportional to incoming jitter**

![image-20241127220933103](dpll/image-20241127220933103.png)



> John T. Stonick, ISSCC 2011 TUTORIALS *T5: DPLL-Based Clock and Data Recovery*
>
> Walker, Richard. (2003). Designing Bang-Bang PLLs for Clock and Data Recovery in Serial Data Transmission Systems.  [[pdf](https://www.omnisterra.com/walker/pdfs.papers/BBPLL.pdf)]
>
> \- Clock and Data Recovery for Serial Data Communications, focusing on bang-bang CDR design methodology, ISSCC Short Course, February 2002. [[slides](https://www.omnisterra.com/walker/pdfs.talks/ISSCC2002.pdf)]


## DCO Quantization Noise

*TODO* &#128197;

## TDC Quantization Noise

*TODO* &#128197;

![image-20250601122145164](dpll/image-20250601122145164.png)


## CDR Loop Latency

> Amir Amirkhany. ISSCC 2019 "Basics of Clock and Data Recovery Circuits"
>
> CC Chen. Why A Low Loop Latency in A CDR Design? [[https://youtu.be/io9WZbhlahU](https://youtu.be/io9WZbhlahU)]
>
> —. Why Understanding and Optimizing Loop Latency for A CDR Design? [[https://youtu.be/Jyy18865jv8](https://youtu.be/Jyy18865jv8)]

![image-20250706173343946](dpll/image-20250706173343946.png)

---

![image-20250706121529451](dpll/image-20250706121529451.png)

---

![image-20241102235118149](dpll/image-20241102235118149.png)

![image-20241102235145417](dpll/image-20241102235145417.png)

loop latency is represented as $e^{-sD}$ in linear model

---

![image-20241102235736432](dpll/image-20241102235736432.png)

![image-20241103000223470](dpll/image-20241103000223470.png)

![image-20241103000653906](dpll/image-20241103000653906.png)



### Sensitivity to Loop Latency

![image-20241103142137640](dpll/image-20241103142137640.png)

---

![image-20241103142656134](dpll/image-20241103142656134.png)

![image-20241103142531277](dpll/image-20241103142531277.png)

![image-20241103142938907](dpll/image-20241103142938907.png)



### Optimizing Loop Latency

*TODO* &#128197;



> CC Chen. Circuit Image: Why Understanding and Optimizing Loop Latency for A CDR Design? [[https://youtu.be/Jyy18865jv8?si=uY2HUV8mERLterwH](https://youtu.be/Jyy18865jv8?si=uY2HUV8mERLterwH)]



## DT & CT Spectral Density

![image-20250512230604969](dpll/image-20250512230604969.png)

---

[[Sampling of WSS process of Systems, Modulation and Noise](https://raytroop.github.io/2024/05/25/comm/#sampling-of-wss-process)]

![image-20250512233058520](dpll/image-20250512233058520.png)

That is
$$
P_{x_s x_s} (f)= \frac{1}{T_s}P_{xx}(f)
$$
In going from *discrete* time to *continuous* time,  we must add a scale factor $1/T$, the sample period



---

![image-20250513211531981](dpll/image-20250513211531981.png)







## reference

Sam Palermo, ECEN620 2024 Lecture 9: Digital PLLs [[https://people.engr.tamu.edu/spalermo/ecen620/lecture09_ee620_digital_PLLs.pdf](https://people.engr.tamu.edu/spalermo/ecen620/lecture09_ee620_digital_PLLs.pdf)]

Topics in IC(Wireline Transceiver Design) [[https://ocw.snu.ac.kr/sites/default/files/NOTE/Lec%203%20-%20ADPLL.pdf](https://ocw.snu.ac.kr/sites/default/files/NOTE/Lec%203%20-%20ADPLL.pdf)]

Michael H. Perrott, ISSCC 2008 Tutorial on Digital Phase-Locked Loops [[https://www.nishanchettri.com/isscc-slides/2008%20ISSCC/Tutorials/T05_Pres.pdf](https://www.nishanchettri.com/isscc-slides/2008%20ISSCC/Tutorials/T05_Pres.pdf)]

—, CICC 2009 Tutorial on Digital Phase-Locked Loops [[https://www.cppsim.com/PLL_Lectures/digital_pll_cicc_tutorial_perrott.pdf](https://www.cppsim.com/PLL_Lectures/digital_pll_cicc_tutorial_perrott.pdf)]

Robert Bogdan Staszewski,  CICC 2020:  Beyond All-Digital PLL for RF and Millimeter-Wave Frequency Synthesis [[link](https://www.researchgate.net/profile/Yizhe-Hu/publication/342702810_Beyond_All-Digital_PLL_for_RF_and_Millimeter-Wave_Frequency_Synthesis/links/5f02305692851c52d619ce21/Beyond-All-Digital-PLL-for-RF-and-Millimeter-Wave-Frequency-Synthesis.pdf)]

Akihide Sai, ISSCC 2023 T5: All-digital PLLs From Fundamental Concepts to Future Trends [[https://www.nishanchettri.com/isscc-slides/2023%20ISSCC/TUTORIALS/T5.pdf](https://www.nishanchettri.com/isscc-slides/2023%20ISSCC/TUTORIALS/T5.pdf)]

Mike Shuo-Wei Chen, CICC 2020 ES2-3: Low-Spur PLL Architectures and Techniques [[https://youtu.be/sgPDchYhN-4?si=FAy8N3SuX6vVpYhl](https://youtu.be/sgPDchYhN-4?si=FAy8N3SuX6vVpYhl)]

S. Levantino, "Digital phase-locked loops," 2018 IEEE Custom Integrated Circuits Conference (CICC), San Diego, CA, USA, 2018 [[slides](https://picture.iczhiku.com/resource/eetop/sHkGfpEDIeeEIXVc.pdf)]

Saurabh Saxena, IIT Madras. Phase-Locked Loops: Noise Analysis in Digital PLL [[https://youtu.be/mddtxcqfiKU?si=yD15KM9WBkT6c68P](https://youtu.be/mddtxcqfiKU?si=yD15KM9WBkT6c68P)]

---

Y. Hu, T. Siriburanon and R. B. Staszewski, "Multirate Timestamp Modeling for Ultralow-Jitter Frequency Synthesis: A Tutorial," in *IEEE Transactions on Circuits and Systems II: Express Briefs*, vol. 69, no. 7, pp. 3030-3036, July 2022

---

Neil Robertson. Digital PLL's -- Part 1 [[https://www.dsprelated.com/showarticle/967.php](https://www.dsprelated.com/showarticle/967.php)]

Neil Robertson. Digital PLL's -- Part 2 [[https://www.dsprelated.com/showarticle/973.php](https://www.dsprelated.com/showarticle/973.php)]

Neil Robertson. Digital PLL's -- Part 3 [[https://www.dsprelated.com/showarticle/1177.php](https://www.dsprelated.com/showarticle/1177.php)]

Daniel Boschen. GRCon24 - Quick Start on Control Loops with Python Workshop [[video](https://youtu.be/RxQWk1PjJLQ), [slides](https://events.gnuradio.org/event/24/contributions/599/)]

---


L. Avallone, M. Mercandelli, A. Santiccioli, M. P. Kennedy, S. Levantino and C. Samori, "A Comprehensive Phase Noise Analysis of Bang-Bang Digital PLLs," in IEEE Transactions on Circuits and Systems I: Regular Papers, vol. 68, no. 7, pp. 2775-2786, July 2021 [[https://sci-hub.st/10.1109/TCSI.2021.3072344](https://sci-hub.st/10.1109/TCSI.2021.3072344)]

M. Zanuso, D. Tasca, S. Levantino, A. Donadel, C. Samori and A. L. Lacaita, "Noise Analysis and Minimization in Bang-Bang Digital PLLs," in IEEE Transactions on Circuits and Systems II: Express Briefs, vol. 56, no. 11, pp. 835-839, Nov. 2009 [[https://sci-hub.st/10.1109/TCSII.2009.2032470](https://sci-hub.st/10.1109/TCSII.2009.2032470)]

N. Da Dalt, "Linearized Analysis of a Digital Bang-Bang PLL and Its Validity Limits Applied to Jitter Transfer and Jitter Generation," in IEEE Transactions on Circuits and Systems I: Regular Papers, vol. 55, no. 11, pp. 3663-3675, Dec. 2008 [[https://sci-hub.st/10.1109/TCSI.2008.925948](https://sci-hub.st/10.1109/TCSI.2008.925948)]

—, "Markov Chains-Based Derivation of the Phase Detector Gain in Bang-Bang PLLs," in IEEE Transactions on Circuits and Systems II: Express Briefs, vol. 53, no. 11, pp. 1195-1199, Nov. 2006 [[https://sci-hub.st/10.1109/TCSII.2006.883197](https://sci-hub.st/10.1109/TCSII.2006.883197)]

—, "A design-oriented study of the nonlinear dynamics of digital bang-bang PLLs," in *IEEE Transactions on Circuits and Systems I: Regular Papers*, vol. 52, no. 1, pp. 21-31, Jan. 2005 [[https://sci-hub.se/10.1109/TCSI.2004.840089](https://sci-hub.se/10.1109/TCSI.2004.840089)]

—, "Theory and Implementation of Digital Bang-Bang Frequency Synthesizers for High Speed Serial Data Communications", PhD Dissertation, RWTH Aachen University, Aachen, North Rhine-Westphalia, Germany, 2007 [[pdf](https://publications.rwth-aachen.de/record/62439/files/DaDalt_Nicola.pdf)]

Walker, Richard. (2003). Designing Bang-Bang PLLs for Clock and Data Recovery in Serial Data Transmission Systems. [[paper](https://www.omnisterra.com/walker/pdfs.papers/BBPLL.pdf),[slides](https://www.omnisterra.com/walker/pdfs.talks/bctm2.maker.pdf)]

---

***hunting jitter***

S. Jang, S. Kim, S. -H. Chu, G. -S. Jeong, Y. Kim and D. -K. Jeong, "An Optimum Loop Gain Tracking All-Digital PLL Using Autocorrelation of Bang–Bang Phase-Frequency Detection," in IEEE Transactions on Circuits and Systems II: Express Briefs, vol. 62, no. 9, pp. 836-840, Sept. 2015 [[https://sci-hub.st/10.1109/TCSII.2015.2435691](https://sci-hub.st/10.1109/TCSII.2015.2435691)] [[phd thesis](https://s-space.snu.ac.kr/bitstream/10371/119111/1/000000066677.pdf)]

Deog-Kyoon Jeong. Topics in IC (Wireline Transceiver Design). Lec 3 - All-Digital PLL [[https://ocw.snu.ac.kr/sites/default/files/NOTE/Lec%203%20-%20ADPLL.pdf](https://ocw.snu.ac.kr/sites/default/files/NOTE/Lec%203%20-%20ADPLL.pdf)]

—. Topics in IC (Wireline Transceiver Design). Lec 6 - Clock and Data Recovery [[https://ocw.snu.ac.kr/sites/default/files/NOTE/Lec%206%20-%20Clock%20and%20Data%20Recovery.pdf](https://ocw.snu.ac.kr/sites/default/files/NOTE/Lec%206%20-%20Clock%20and%20Data%20Recovery.pdf)]

Lee Hae-Chang.: ‘*An estimation approach to clock and data recovery*’, PhD Thesis, Stanford University, November 2006 [[pdf](https://www-vlsi.stanford.edu/people/alum/pdf/0611_HaechangLee_Phase_Estimation.pdf)]

J. Kim, Design of CMOS Adaptive-Supply Serial Links, Ph.D. Thesis, Stanford University, December 2002. [[pdf](https://vlsiweb.stanford.edu/people/alum/pdf/0212_Kim_______Design_Of_CMOS_AdaptiveSu.pdf)]

High-speed Serial Interface 2013. Lect. 16 – Clock and Data Recovery 3 [[http://tera.yonsei.ac.kr/class/2013_1_2/lecture/Lect16_CDR-3.pdf](http://tera.yonsei.ac.kr/class/2013_1_2/lecture/Lect16_CDR-3.pdf)]

CC Chen. Why Hunting Jitter Happens in CDR: The Role of Input Jitter and Latency? [[https://youtu.be/hPDielPsFgY](https://youtu.be/hPDielPsFgY)]
