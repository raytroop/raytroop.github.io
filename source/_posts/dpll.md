---
title: Digital Phase-Locked Loops
date: 2025-05-13 17:30:16
tags:
categories:
- link
mathjax: true
---



## Hunting Jitter

***Hunting jitter*** is often referred to as ***dithering jitter***, the *periodic* time error between *data clock* and input data, which exhibits a ***limit-cycle*** behavior

![image-20250819202727871](dpll/image-20250819202727871.png)

![image-20250819203806711](dpll/image-20250819203806711.png)

![image-20250819210031102](dpll/image-20250819210031102.png)



## BB PD

> Youngdon Choi, Deog-Kyoon Jeong and W. Kim, "Jitter transfer analysis of tracked oversampling techniques for multigigabit clock and data recovery," in IEEE Transactions on Circuits and Systems II: Analog and Digital Signal Processing, vol. 50, no. 11, pp. 775-783, Nov. 2003 [[https://sci-hub.st/10.1109/TCSII.2003.819070](https://sci-hub.st/10.1109/TCSII.2003.819070)]
>
> John T. Stonick, ISSCC 2011 TUTORIALS *T5: DPLL-Based Clock and Data Recovery* [[slides](https://www.nishanchettri.com/isscc-slides/2011%20ISSCC/TUTORIALS/ISSCC2011Visuals-T5.pdf) [transcript](https://www.nishanchettri.com/isscc-slides/2011%20ISSCC/TUTORIALS/Transcription_T5.pdf)]
>
> Walker, Richard. (2003). Designing Bang-Bang PLLs for Clock and Data Recovery in Serial Data Transmission Systems.  [[pdf](https://www.omnisterra.com/walker/pdfs.papers/BBPLL.pdf)]
>
> —, Clock and Data Recovery for Serial Data Communications, focusing on bang-bang CDR design methodology, ISSCC Short Course, February 2002. [[slides](https://www.omnisterra.com/walker/pdfs.talks/ISSCC2002.pdf)]

It's **ternary**, because *early*, *late* and *no transition*

notice the ***transition density = 1*** in digital PLL

### Linearization

The effective PD gain is a function of the **input jitter pdf**, it enables one to anticipate the effects of input jitter on loop characteristics


BB Gain is the slope of average BB output $\mu$, versus phase offset $\phi$, i.e. $\frac {\partial \mu}{\partial \phi}$,

BB only produces output for a transition and this de-rates the gain. ***Transition density = 0.5*** for ***random*** data

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



### gain simulation

> L. Avallone, M. Mercandelli, A. Santiccioli, M. P. Kennedy, S. Levantino and C. Samori, "A Comprehensive Phase Noise Analysis of Bang-Bang Digital PLLs," in IEEE Transactions on Circuits and Systems I: Regular Papers, vol. 68, no. 7, pp. 2775-2786, July 2021 [[https://sci-hub.st/10.1109/TCSI.2021.3072344](https://sci-hub.st/10.1109/TCSI.2021.3072344)]
>
> T. -K. Kuan and S. -I. Liu, "A Bang Bang Phase-Locked Loop Using Automatic Loop Gain Control and Loop Latency Reduction Techniques," in IEEE Journal of Solid-State Circuits, vol. 51, no. 4, pp. 821-831, April 2016 [[https://sci-hub.st/10.1109/JSSC.2016.2519391](https://sci-hub.st/10.1109/JSSC.2016.2519391)]

![image-20250902215541227](dpll/image-20250902215541227.png)

![image-20250913192552933](dpll/image-20250913192552933.png)

```python
import matplotlib.pyplot as plt
import numpy as np

N = 2**10
sigma = 0.1
dt = np.random.normal(sigma,size=N)
et = np.sign(dt)

# Eq-(2)
coef_form = np.mean(np.abs(dt)) / np.mean(np.power(dt, 2))
print(f'coef_form: {coef_form}')

# Eq-(9)
coef_gauss = (2/np.pi)**0.5/sigma
print(f'coef_gauss: {coef_gauss}')

# polyfit
coef_fit = np.polyfit(dt, et, 1)
print(f'coef_fit: {coef_fit}')

x = np.linspace(-3.5, 3.5, 1000)
y = coef_fit[0]*x + coef_fit[1]

plt.figure(figsize=(12,6))
plt.plot(dt, et, 'o')
plt.plot(x, y, linewidth=2, linestyle='--')

# Calculate histogram counts and bin edges
counts, bin_edges = np.histogram(dt, bins=100)
# Find the maximum count
max_count = counts.max()
# Create weights to normalize the maximum height to 1
weights = np.ones_like(dt) / max_count
plt.hist(dt, bins=100, weights=weights)

plt.xlabel(r'$\Delta t$')
plt.grid(True)
plt.legend([r'$\Delta t \sim \varepsilon $', r'$x_{fit} \sim y_{fit}$', r'$ \text{hist}_{\Delta t}$'])
plt.show()


# coef_form: 0.7910794009505085
# coef_gauss: 7.978845608028654
# coef_fit: [0.79013999 0.0204332 ]
```



---

> Pavan, Shanthi, Richard Schreier, and Gabor Temes. (2016). Understanding Delta-Sigma Data Converters. 2nd ed. Wiley.  - *2.2.1 Quantizer Modeling*

![image-20250902212931083](dpll/image-20250902212931083.png)
$$
\frac{\mathrm{d}\sigma_e^2}{\mathrm{d}k} =0\space\space\Rightarrow\space\space k=\frac{\left\langle  v,y\right\rangle}{\left\langle y,y \right\rangle}
$$

![image-20250902231449843](dpll/image-20250902231449843.png)

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



> CC Chen. Circuit Image: Why Understanding and Optimizing Loop Latency for A CDR Design? [[https://youtu.be/Jyy18865jv8](https://youtu.be/Jyy18865jv8)]


## Impulse Train Modulator (ITM)

*TODO* &#128197;



## DT & CT Spectral Density

> Sam Palermo, ECEN620: Network Theory Broadband Circuit Design Fall 2025 *Lecture 9: Digital PLLs* [[https://people.engr.tamu.edu/spalermo/ecen620/lecture09_ee620_digital_PLLs.pdf](https://people.engr.tamu.edu/spalermo/ecen620/lecture09_ee620_digital_PLLs.pdf)]
>
> Michael Perrott, Short Course On Phase-Locked Loops and Their Applications Day 4, AM Lecture *Digital Frequency Synthesizers* [[https://www.cppsim.com/PLL_Lectures/day4_am.pdf](https://www.cppsim.com/PLL_Lectures/day4_am.pdf)]
>
> Hsu, Chun-Ming, Ph. D. Massachusetts Institute of Technology. "Techniques for high-performance digital frequency synthesis and phase control." 2008. [[http://hdl.handle.net/1721.1/45870](http://hdl.handle.net/1721.1/45870)]



*TODO* &#128197;

??

$T$ of DT-CT comes from ZOH approximation of impulse train

$\frac{1}{T}$ of CT-DT comes from CT to sampled sequence to impulse train


---

---


***DT to CT***

![image-20260625221638670](dpll/image-20260625221638670.png)

![image-20260625221753608](dpll/image-20260625221753608.png)

Here, $\boxed{S_x(e^{j2\pi fT}) = S_d(e^{j2\pi fT})\cdot \textcolor{blue}{ f_s}}$,   For example, the quantization noise spectrum is given by $S_x(e^{j2\pi fT}) = \frac{1}{12f_s}\cdot f_s = \frac{1}{12}$. To convert the sequence spectrum into a continuous impulse train spectrum, we multiply by $\color{blue}\frac{1}{T^2}$
$$
S_y(f) = S_x(e^{j2\pi fT}) \cdot \textcolor{blue}{\frac{1}{f_s}\cdot \frac{1}{T^2}\cdot |H(f)|^2 } = S_x(e^{j2\pi fT}) \cdot \textcolor{blue}{\frac{1}{T}|H(f)|^2}
$$


![image-20260625222247558](dpll/image-20260625222247558.png)

![image-20250512230604969](dpll/image-20250512230604969.png)

---

---





![image-20260625233049546](dpll/image-20260625233049546.png)





![image-20260625234115193](dpll/image-20260625234115193.png)

![image-20260625233852702](dpll/image-20260625233852702.png)

![image-20260625234008676](dpll/image-20260625234008676.png)

![image-20260625233243905](dpll/image-20260625233243905.png)

## reference

Topics in IC (Wireline Transceiver Design) [[https://ocw.snu.ac.kr/sites/default/files/NOTE/Lec%203%20-%20ADPLL.pdf](https://ocw.snu.ac.kr/sites/default/files/NOTE/Lec%203%20-%20ADPLL.pdf)]

Michael H. Perrott, ISSCC 2008 Tutorial on Digital Phase-Locked Loops 

—, CICC 2009 Tutorial on Digital Phase-Locked Loops [[https://www.cppsim.com/PLL_Lectures/digital_pll_cicc_tutorial_perrott.pdf](https://www.cppsim.com/PLL_Lectures/digital_pll_cicc_tutorial_perrott.pdf)]

Robert Bogdan Staszewski,  CICC 2020:  Beyond All-Digital PLL for RF and Millimeter-Wave Frequency Synthesis [[link](https://www.researchgate.net/profile/Yizhe-Hu/publication/342702810_Beyond_All-Digital_PLL_for_RF_and_Millimeter-Wave_Frequency_Synthesis/links/5f02305692851c52d619ce21/Beyond-All-Digital-PLL-for-RF-and-Millimeter-Wave-Frequency-Synthesis.pdf)]

Akihide Sai, ISSCC 2023 T5: All-digital PLLs From Fundamental Concepts to Future Trends 

Mike Shuo-Wei Chen, CICC 2020 ES2-3: Low-Spur PLL Architectures and Techniques [[https://youtu.be/sgPDchYhN-4](https://youtu.be/sgPDchYhN-4)]

S. Levantino, "Digital phase-locked loops," 2018 IEEE Custom Integrated Circuits Conference (CICC), San Diego, CA, USA, 2018

Saurabh Saxena, IIT Madras. Phase-Locked Loops: Noise Analysis in Digital PLL [[https://youtu.be/mddtxcqfiKU](https://youtu.be/mddtxcqfiKU)]

---

Y. Hu, T. Siriburanon and R. B. Staszewski, "Multirate Timestamp Modeling for Ultralow-Jitter Frequency Synthesis: A Tutorial," in *IEEE Transactions on Circuits and Systems II: Express Briefs*, vol. 69, no. 7, pp. 3030-3036, July 2022

---

Neil Robertson. Digital PLL's -- Part 1 [[https://www.dsprelated.com/showarticle/967.php](https://www.dsprelated.com/showarticle/967.php)]

—. Digital PLL's -- Part 2 [[https://www.dsprelated.com/showarticle/973.php](https://www.dsprelated.com/showarticle/973.php)]

—. Digital PLL's -- Part 3 [[https://www.dsprelated.com/showarticle/1177.php](https://www.dsprelated.com/showarticle/1177.php)]

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
