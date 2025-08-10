---
title: Noise Analysis
date: 2024-04-27 09:54:25
tags:
categories: noise
mathjax: true
---



![image-20241208103218870](noise/image-20241208103218870.png)

---



## noise power at filter output

> Chembian Thambidurai, "Comparison Of Noise Power At Lowpass Filter Output" [[link](https://www.linkedin.com/posts/chembiyan-t-0b34b910_noise-power-at-filter-output-activity-7006486487093456896-W0Rt?utm_source=share&utm_medium=member_desktop)]
>
> —, "On Noise Power At The Bandpass Filter Output" [[link](https://www.linkedin.com/posts/chembiyan-t-0b34b910_bandpass-noise-activity-7008896204507922432-ZRXF?utm_source=share&utm_medium=member_desktop)]
>
> —, "Integrated Power of Thermal and Flicker Noise" [[link](https://www.linkedin.com/posts/chembiyan-t-0b34b910_flicker-and-thermal-noise-power-on-a-log-activity-7003063399781711872-62nh?utm_source=share&utm_medium=member_desktop)]

*TODO* &#128197;



## Sampling Noise

> Chembian Thambidurai, "Noise, Sampling and Zeta Functions" [[link](https://www.linkedin.com/posts/chembiyan-t-0b34b910_sampling-noise-signals-activity-7018929654627520512-QYr0)]

A random signal $v_n(t)$ is sampled using an ***ideal impulse sampler***

![image-20241201165157743](noise/image-20241201165157743.png)

*TODO* &#128197;



## Pulsed Noise Signals

> Chembian Thambidurai, "Power Spectral Density of Pulsed Noise Signals" [[link](https://www.linkedin.com/posts/chembiyan-t-0b34b910_psd-of-pulsed-noise-signal-activity-6992527460886040577-a0im?utm_source=share&utm_medium=member_desktop)]

![image-20241208075822212](noise/image-20241208075822212.png)

> Above,  the output of the multiplier be $y(t)$ is passed through a ideal brick wall low pass filter with a bandwidth of $f_0/2$

When a random signal is multiplied by a *pulse function*, the resulting signal becomes a *cyclo-stationary random process*. 

As rule of thumb, the spectrum of such a pulsed noise signal  

- *thermal noise* is multiplied by $D$

-  *flicker noise* is multiplied by $D^2$, 


where $D$ is the duty cycle of the pulse signal



![image-20241208111744647](noise/image-20241208111744647.png)

### banlimited input

![image-20241208113904927](noise/image-20241208113904927.png)



###  wideband white noise input

![image-20241208114442705](noise/image-20241208114442705.png)

### flicker noise input

with $S_x(f)=\frac{K_f}{f}$

![image-20241208121027250](noise/image-20241208121027250.png)

![image-20241208121402724](noise/image-20241208121402724.png)

Assuming $\Delta f \ll f_0$

![image-20241208121645637](noise/image-20241208121645637.png)



---

![image-20241208111506517](noise/image-20241208111506517.png)





## ADC SNR & clock jitter

> ***cyclostationary*** random process

![image-20250809170358612](noise/image-20250809170358612.png)

---

![image-20250525134220901](noise/image-20250525134220901.png)

![image-20250525135503671](noise/image-20250525135503671.png)

$$\begin{align}
\text{SNR}_\text{ADC}[\text{dB}] &= -20\cdot \log \sqrt{\left(10^{-\frac{\text{SNR}_\text{Quantization Noise}}{20}}\right)^2 + \left(10^{-\frac{\text{SNR}_\text{Jitter}}{20}}\right)^2} \\
&= -10\cdot \log \left(\left(10^{-\frac{\text{SNR}_\text{Quantization Noise}}{20}}\right)^2 + \left(10^{-\frac{\text{SNR}_\text{Jitter}}{20}}\right)^2\right) \\
&= -10\cdot \log \left(\left(10^{-\frac{10\log(\frac{3\times2^{2N}}{2})}{20}}\right)^2 + \left(10^{-\frac{-20\log{(2\pi f_\text{in}\sigma_\text{jitter})}}{20}}\right)^2\right) \\
&= -10\cdot \log \left( \frac{2}{3\times 2^{2N}} + (2\pi f_\text{in}\sigma_\text{jitter})^2 \right)
\end{align}$$



> Ayça Akkaya, "High-Speed ADC Design and Optimization for Wireline Links" [[https://infoscience.epfl.ch/server/api/core/bitstreams/96216029-c2ff-48e5-a675-609c1e26289c/content](https://infoscience.epfl.ch/server/api/core/bitstreams/96216029-c2ff-48e5-a675-609c1e26289c/content)]
>
> CC Chen, Why Absolute Jitter Matters for ADCs & DACs? [[https://youtu.be/jBgDDFFDq30?si=XFyTEfApN86Ef-RG](https://youtu.be/jBgDDFFDq30?si=XFyTEfApN86Ef-RG)]
>
> Thomas Neu, TIPL 4704. Jitter vs SNR for ADCs [[https://www.ti.com/content/dam/videos/external-videos/en-us/2/3816841626001/5529003238001.mp4/subassets/TIPL-4704-Jitter-vs-SNR.pdf](https://www.ti.com/content/dam/videos/external-videos/en-us/2/3816841626001/5529003238001.mp4/subassets/TIPL-4704-Jitter-vs-SNR.pdf)]

![image-20250525141523199](noise/image-20250525141523199.png)

![image-20250525143507747](noise/image-20250525143507747.png)

```python
import numpy as np
import matplotlib.pyplot as plt

N = 12  # ADC bit
fin = 100e6 # the frequency of the sinusoidal input signal
jrms = np.linspace(0, 10, 1000)*1e-12 #ps

# ADC (SNR) with Quantization Noise & Jitter degradation
SNR_ADC = -10 * np.log10(10**(-np.log10(3*2**(2*N)/2)) + (2*np.pi*fin*jrms)**2)
ENOB = (SNR_ADC - 1.76) / 6.02

plt.plot(jrms*1e12, ENOB, label='100 MHZ input')
plt.plot([0, 10], [12, 12], '--', label='12-bit limit')
plt.plot([0, 10], [6, 6], '--', label='6-bit limit')

plt.xscale('linear')
plt.xlim([0, 10])
plt.ylim([5, 15])
plt.xlabel('RMS Jitter (ps)')
plt.ylabel('Effective Number of Bits (ENOB')
plt.grid(which='both')
plt.title('ENOB vs. RMS Clock Jitter (100 MHz)')
plt.legend()
plt.show()
```

---

> Chun-Hsien Su (蘇純賢).  Design of Oversampled Sigma-Delta Data Converters. July, 2006 [[pdf](https://picture.iczhiku.com/resource/eetop/wHIHwgULoQJZLNCV.pdf)]

![image-20250809182751263](noise/image-20250809182751263.png)

---

> Chembian Thambidurai, "SNR of an ADC in the presence of clock jitter" [[https://www.linkedin.com/posts/chembiyan-t-0b34b910_adcsnrjitter-activity-7171178121021304833-f2Wd/](https://www.linkedin.com/posts/chembiyan-t-0b34b910_adcsnrjitter-activity-7171178121021304833-f2Wd/)]

Unlike the quantization noise and the thermal noise, the impact of the clock jitter on the ADC performance depends on the input signal properties like its PSD

![image-20241123205352661](noise/image-20241123205352661.png)

The error between *the ideal sampled signal* and *the sampling with clock jitter* can be treated as noise and it results in the degradation of the SNR of the ADC

![image-20241124004634365](noise/image-20241124004634365.png)



***For sinusoid input:***

![image-20241210235817281](noise/image-20241210235817281.png)



![image-20241222140258960](noise/image-20241222140258960.png)

```python
import numpy as np
import matplotlib.pyplot as plt

ENOB = 8
fin = np.logspace(8, 11, 60)

# quantization noise: SNR = 6.02*ENOB + 1.76 dB
Ps_PnQ = 10**((6.02*ENOB + 1.76)/10)
PnQ = 1/Ps_PnQ

# jitter noise: SNR = 6 - 20log10(2*pi*fin*Jrms) dB @ref. Chembiyan T
Jrms_list = [25e-15, 50e-15, 100e-15, 250e-15, 500e-15, 1000e-15]
for Jrms in Jrms_list:
    # Ps_PnJ_lcl = 10**((6-20*np.log10(2*np.pi*fin*Jrms))/10)     # ref. Chembiyan T
    Ps_PnJ_lcl = 10**((0 - 20 * np.log10(2 * np.pi * fin * Jrms)) / 10)  # ref. Nicola Da Dalt
    PnJ_lcl = 1/Ps_PnJ_lcl
    SNR_lcl = 10*np.log10(1/(PnQ+PnJ_lcl))
    plt.plot(fin, SNR_lcl, label=r'$\sigma_{jitter}$'+'='+str(int(Jrms*1e15))+'fs')

plt.xscale('log')
plt.ylim([0, 55])
plt.xlabel(r'$f_{in}$ [Hz]')
plt.ylabel(r'SNR [dB]')
plt.grid(which='both')
# plt.title(r'ref. Chembiyan T')
plt.title(r'ref. Nicola Da Dalt')
plt.legend()
plt.show()

```

> K. Tyagi and B. Razavi, "Performance Bounds of ADC-Based Receivers Due to Clock Jitter," in *IEEE Transactions on Circuits and Systems II: Express Briefs*, vol. 70, no. 5, pp. 1749-1753, May 2023 [[https://www.seas.ucla.edu/brweb/papers/Journals/KT_TCAS_2023.pdf](https://www.seas.ucla.edu/brweb/papers/Journals/KT_TCAS_2023.pdf)]
>
> N. Da Dalt, M. Harteneck, C. Sandner and A. Wiesbauer, "On the jitter requirements of the sampling clock for analog-to-digital converters," in *IEEE Transactions on Circuits and Systems I: Fundamental Theory and Applications*, vol. 49, no. 9, pp. 1354-1360, Sept. 2002 [[https://sci-hub.se/10.1109/TCSI.2002.802353](https://sci-hub.se/10.1109/TCSI.2002.802353)]
>
> M. Shinagawa, Y. Akazawa and T. Wakimoto, "Jitter analysis of high-speed sampling systems," in IEEE Journal of Solid-State Circuits, vol. 25, no. 1, pp. 220-224, Feb. 1990 [[https://sci-hub.se/10.1109/4.50307](https://sci-hub.se/10.1109/4.50307)]
>
> ![image-20241210232716862](noise/image-20241210232716862.png)
>
> Ayça Akkaya, "High-Speed ADC Design and Optimization for Wireline Links" [[https://infoscience.epfl.ch/server/api/core/bitstreams/96216029-c2ff-48e5-a675-609c1e26289c/content](https://infoscience.epfl.ch/server/api/core/bitstreams/96216029-c2ff-48e5-a675-609c1e26289c/content)]



##  Sampled Thermal Noise

The **aliasing of the noise**, or **noise folding**, plays an important role in switched-capacitor as it does in all switched-capacitor filters

![image-20240425215938141](noise/image-20240425215938141.png)

Assume for the moment that the switch is *always closed* (that there is no hold phase), the single-sided noise density would be

![image-20240428182816109](noise/image-20240428182816109.png)

---

![image-20240428180635082](noise/image-20240428180635082.png)



$v_s[n]$ is the sampled version of $v_{RC}(t)$, i.e. $v_s[n]= v_{RC}(nT_C)$
$$
S_s(e^{j\omega}) = \frac{1}{T_C} \sum_{k=-\infty}^{\infty}S_{RC}(j(\frac{\omega}{T_C}-\frac{2\pi k}{T_C})) \cdot d\omega
$$
where $\omega \in [-\pi, \pi]$,  furthermore $\frac{d\omega}{T_C}= d\Omega$
$$
S_s(j\Omega) = \sum_{k=-\infty}^{\infty}S_{RC}(j(\Omega-k\Omega_s)) \cdot d\Omega
$$

> ![image-20240428215559780](noise/image-20240428215559780.png)

![image-20240425220033340](noise/image-20240425220033340.png)

The noise in $S_{RC}$ is a *stationary process* and so is *uncorrelated* over $f$ allowing the $N$ rectangles to be combined by simply summing their noise powers


![image-20240428225949327](noise/image-20240428225949327.png)

![image-20240425220400924](noise/image-20240425220400924.png)

where $m$ is the duty cycle

> Kundert, Ken. (2006). Simulating Switched-Capacitor Filters with SpectreRF [[https://designers-guide.org/analysis/sc-filters.pdf](https://designers-guide.org/analysis/sc-filters.pdf)]
>
> Pavan, Schreier and Temes, "Understanding Delta-Sigma Data Converters, Second Edition" ISBN 978-1-119-25827-8
>
> Boris Murmann, EE315B VLSI Data Conversion Circuits, Autumn 2013
>
> Tania Khanna, ESE568 Fall 2019, Mixed Signal Circuit Design and Modeling URL: [https://www.seas.upenn.edu/~ese568/fall2019/](https://www.seas.upenn.edu/~ese568/fall2019/)
>
> Matt Pharr, Wenzel Jakob, and Greg Humphreys. 2016. Physically Based Rendering: From Theory to Implementation (3rd. ed.). Morgan Kaufmann Publishers Inc., San Francisco, CA, USA.
>
> R. Gregorian and G. C. Temes. Analog MOS Integrated Circuits for Signal Processing. Wiley-Interscience, 1986
>
> Trevor Caldwell, Lecture 9 Noise in Switched-Capacitor Circuits  [[http://individual.utoronto.ca/trevorcaldwell/course/NoiseSC.pdf](http://individual.utoronto.ca/trevorcaldwell/course/NoiseSC.pdf)]
>
> Christian-Charles Enz. High precision CMOS micropower amplifiers [[pdf](https://picture.iczhiku.com/resource/eetop/wYItQFykkAQDFccB.pdf)]

---

*Below analysis focusing on sampled noise*

> Boris Murmann. Noise Analysis in Switched-Capacitor Circuits, ISSCC 2011 / tutorials [[slides](https://www.nishanchettri.com/isscc-slides/2011%20ISSCC/TUTORIALS/ISSCC2011Visuals-T8.pdf), [transcript](https://www.nishanchettri.com/isscc-slides/2011%20ISSCC/TUTORIALS/Transcription_T9.pdf)]

![image-20250810085721440](noise/image-20250810085721440.png)



> - Calculate autocorrelation function of noise at the output of the RC filter
> - Calculate the spectrum by taking the **discrete** time Fourier transform of the autocorrelation function

---

> Bernhard E. Boser . Advanced Analog Integrated Circuits Switched Capacitor Gain Stages [[https://people.eecs.berkeley.edu/~boser/courses/240B/lectures/M05%20SC%20Gain%20Stages.pdf](https://people.eecs.berkeley.edu/~boser/courses/240B/lectures/M05%20SC%20Gain%20Stages.pdf)]

![image-20240427183700971](noise/image-20240427183700971.png)





## Cyclostationary Noise (Modulated Noise)

> [[https://ece-research.unm.edu/bsanthan/ece541/cyclo.pdf](https://ece-research.unm.edu/bsanthan/ece541/cyclo.pdf)]
>
> Chembian Thambidurai, "Power Spectral Density of Pulsed Noise Signals" [[link](https://www.linkedin.com/posts/chembiyan-t-0b34b910_psd-of-pulsed-noise-signal-activity-6992527460886040577-a0im?utm_source=share&utm_medium=member_desktop)]



![image-20241123230025107](noise/image-20241123230025107.png)

![image-20241123230049341](noise/image-20241123230049341.png)

> ![image-20241123215631264](noise/image-20241123215631264.png)

### White Noise Modulation

> Noisy Resistor & Clocked Switch

$$
v_t (t) = v_i(t)\cdot m_t(t)
$$

where  $v_i(t)$ is input *white* noise, whose autocorrelation is $A\delta(\tau)$, and $m_t(t)$ is periodically operating switch, then autocorrelation of $v_t(t)$
$$\begin{align}
R_t (t_1, t_2) &= E[v_t(t_1)\cdot v_t(t_2)] \\
&= R_i(t_1, t_2)\cdot  m_t(t_1)m_t(t_2)
\end{align}$$

Then
$$\begin{align}
R_t(t, t-\tau) &= R_i(\tau)\cdot m_t(t)m_t(t-\tau) \\
& = A\delta(\tau) \cdot m_t(t)m_t(t-\tau) \\
& = A\delta(\tau) \cdot m_t(t)
\end{align}$$
Because $m_t(t)=m_t(t+T)$, $R_t(t, t-\tau)$ is is periodic in the variable $t$ with period $T$

The time-averaged ACF is denoted as $\tilde{R_t}(\tau)$

$$
\tilde{R}_{t}(\tau) = m\cdot A\delta(\tau)
$$
That is,
$$
S_t(f) = m\cdot S_{A}(f)
$$


---

![image-20241118212505205](noise/image-20241118212505205.png)

![image-20241118212242823](noise/image-20241118212242823.png)

> ![image-20241116170450589](noise/image-20241116170450589.png)



### Colored Noise Modulation

![tavg_factor.drawio](noise/tavg_factor.drawio.svg)
$$
\tilde{R_t}(\tau) = R_i(\tau)\cdot m_{tac}(\tau)
$$

where $m_t(t)m_t(t-\tau)$ averaged on $t$  is denoted as $m_{tac}(\tau)$ or $\overline{m_t(t)m_t(t-\tau)}$

The DC value of $m_{tac}(\tau)$ can be calculated as below

1. for $m\le 0.5$, the DC value of $m_{tac}(\tau)$
   $$
   \frac{m\cdot mT}{T} = m^2
   $$

2. for $m\gt 0.5$, the DC value of $m_{tac}(\tau)$
   $$
   \frac{(m+2m-1)(1-m)T + (2m-1)\{mT -(1-m)T\}}{T} = m^2
   $$

Therefore, time-average power spectral density and total power are *scaled by $m^2$ in fundamental frequency sideband*



---

![image-20241118213007400](noise/image-20241118213007400.png)

![image-20241118215846751](noise/image-20241118215846751.png)




>![image-20241117205422217](noise/image-20241117205422217.png)

---


### Switched-Capacitor Track signal

![image-20241118213830893](noise/image-20241118213830893.png)

![image-20241116165632847](noise/image-20241116165632847.png)



#### track signal pnoise (sc)

![image-20241118220145885](noise/image-20241118220145885.png)

![image-20241118215956843](noise/image-20241118215956843.png)



zoom in first harmonic by linear step of pnoise

![image-20241118220904802](noise/image-20241118220904802.png)

> decreasing the rising/falling time of clock, the harmonics still retain

#### equivalent circuit for pnoise (eq)

1. thermal noise of R is *modulated at first*
2. *then filtered* by ideal filter

![image-20241118214320950](noise/image-20241118214320950.png)

![image-20241118220027598](noise/image-20241118220027598.png)



---

#### sc vs eq

![image-20241118222730383](noise/image-20241118222730383.png)



- sc: harmonic distortion
- eq: no harmonic distortion



## Non-Stationary Processes (Comparator)

> T. Sepke, P. Holloway, C. G. Sodini and H. -S. Lee, "Noise Analysis for Comparator-Based Circuits," in IEEE Transactions on Circuits and Systems I: Regular Papers, vol. 56, no. 3, pp. 541-553, March 2009 [[https://dspace.mit.edu/bitstream/handle/1721.1/61660/Speke-2009-Noise%20Analysis%20for%20Comparator-Based%20Circuits.pdf](https://dspace.mit.edu/bitstream/handle/1721.1/61660/Speke-2009-Noise%20Analysis%20for%20Comparator-Based%20Circuits.pdf)]
>
> Sepke, Todd. "Comparator design and analysis for comparator-based switched-capacitor circuits." (2006). [[https://dspace.mit.edu/handle/1721.1/38925](https://dspace.mit.edu/handle/1721.1/38925)]

### Wide-Sense-Stationary Noise

Much like sinusoidal-steady-state signal analysis, **steady-state noise** analysis methods assume an input $x(t)$ of **infinite duration**, which is a **Wide-Sense Stationary (WSS) random process**

#### Frequency-domain Analysis

![image-20241122233117654](noise/image-20241122233117654.png)

#### Time-domain Analysis

The output $y(t)$ of a linear time-invariant (LTI) system $h(t)$ 
$$\begin{align}
R_{yy}(\tau) &= R_{xx}(\tau)*[h(\tau)*h(-\tau)] \\
&= S_{xx}(0)\delta(\tau) * [h(\tau)*h(-\tau)] \\
&= S_{xx}(0)[h(\tau)*h(-\tau)] \\
&= S_{xx}(0) \int_\alpha h(\alpha)h(\alpha-\tau)d\alpha
\end{align}$$

with WSS white noise input $x(t)$, $R_{xx}(\tau)=S_{xx}(0)\delta(\tau)$, therefore

![image-20241122232641188](noise/image-20241122232641188.png)

### Non-stationary Noise

Assuming the noise applied duration is much less than the time constant, the *output voltage does not reach steady-state and WSS noise analysis does not apply*

> In order to determine the response of an LTI system to a **step noise input**, the problem is *more conveniently solved in the time-domain*

input signal: step ramp input

noise current: step

#### Time-domain Analysis

![image-20241123005612107](noise/image-20241123005612107.png)

The step noise input $x(t) = \nu(t)u(t)$
$$
R_{xx}(t_1,t_2) = E[x(t_1)x(t_2)] = R_{\nu\nu}(t_1, t_2)u(t_1)u(t_2)=R_{\nu\nu}(t_1, t_2)
$$
![image-20241123005644828](noise/image-20241123005644828.png)

>$$
>R_{xy}(t_1, t_2) = E[x(t_1)y(t_2)] = E[x(t_1)(x(t_2)*h(t_2))] = E(x(t_1)x(t_2))*h(t_2) = R_{xx}(t_1,t_2)*h(t_2)
>$$
>
>$$
>R_{yy}(t_1,t_2) = E[y(t_1)y(t_2)] = E[(x(t_1)*h(t_1))y(t_2)] = E[x(t_1)y(t_2)]*h(t_1)=R_{xy}(t_1,t_2)*h(t_1)
>$$

![image-20241123011304449](noise/image-20241123011304449.png)

> the absolute value of each time index is important for a non-stationary signal, and only the time difference was important for WSS signals

 $$\begin{align}
R_{yy}(t_1,t_2) &= h(t_1)*R_{\nu\nu}(t_1, t_2)*h(t_2) \\
&= h(t_1)*S_{xx}(0)\delta(t_2-t_1)*h(t_2) \\
&=S_{xx}(0) h(t_1)*(\delta(t_2-t_1)*h(t_2)) \\
&= S_{xx}(0)h(t_1)*h(t_2-t_1) \\
&= S_{xx}(0)\int_\tau h(\tau)h(t_2-t_1+\tau))d\tau
\end{align}$$

That is
$$
\sigma^2_y (t)= R_{yy}(t_1,t_2)|_{t_1=t_2=t}=S_{xx}(0)\int_{-\infty}^t |h(\tau)|^2d\tau
$$

> $t$, the upper limit of integration is just intuitive,  which lacks strict derivation
>
> Because stable systems have impulse responses that decay to *zero* as time goes to *infinity*, **the output noise variance approaches the WSS result as time approaches infinity**  

![image-20241123074316370](noise/image-20241123074316370.png)

#### Frequency-domain Analysis  

Because the definition of the PSD assumes that the variance of the noise process is independent of time, the PSD of a non-stationary process is not very meaningful

![image-20241123084051824](noise/image-20241123084051824.png)

![image-20241123084118787](noise/image-20241123084118787.png)

---

> Richard Schreier. ECE1371 Advanced Analog Circuits Lecture 8 - COMPARATOR & FLASH ADC DESIGN [[http://individual.utoronto.ca/schreier/lectures/2015/8-6.pdf](http://individual.utoronto.ca/schreier/lectures/2015/8-6.pdf)]

![image-20250710221018596](noise/image-20250710221018596.png)

> $$
> R_{yy}(0) = \frac{1}{2\pi}\int_{-\infty}^{\infty}|H(\omega)|^2S_{xx}(\omega)d\omega = S \cdot \frac{1}{2\pi}\int_{-\infty}^{\infty}|H(\omega)|^2d\omega \overset{\text{Parseval's Relation}}{=} S\cdot \int_{-\infty}^{\infty}|h(t)|^2dt
> $$



#### Input Referred Noise  

![image-20241123094924184](noise/image-20241123094924184.png)

***Noise Voltage to Timing Jitter Conversion & noise gain***

![image-20241123100031499](noise/image-20241123100031499.png)

with a step ramp input  $v_X(t) = Mtu(t)$

The **noise gain** is
$$
|A_N(t_i)| = A_0 (1-e^{t_i/\tau_o})u(t)
$$
where $t_i$ is crossing time of ideal threshold comparator

$$\begin{align}
\overline{v_n^2} &= \frac{\overline{v_{on}^2}}{|A_N|^2} \\
&= \frac{G_n}{G_m}\frac{kT}{C}\frac{1}{A_0}\frac{1+e^{-t_i/\tau_o}}{1-e^{-t_i/\tau_o}} \\
&=4kT\frac{G_n}{G_m^2}\frac{1}{4R_oC} \coth(\frac{t_i}{2\tau_o}) \\
&= 4kTR_n\frac{1}{4\tau_o} \coth(\frac{t_i}{2\tau_o})
\end{align}$$

where $R_n = \frac{G_n}{G_m^2}$, the equivalent thermal noise resistance

> ![image-20241123111642852](noise/image-20241123111642852.png)





## reference

David Herres, The difference between signal under-sampling, aliasing, and folding URL: [https://www.testandmeasurementtips.com/the-difference-between-signal-under-sampling-aliasing-and-folding-faq/](https://www.testandmeasurementtips.com/the-difference-between-signal-under-sampling-aliasing-and-folding-faq/)

Pharr, Matt; Humphreys, Greg. (28 June 2010). Physically Based Rendering: From Theory to Implementation. Morgan Kaufmann. ISBN 978-0-12-375079-2. [Chapter 7 (Sampling and reconstruction)](https://web.archive.org/web/20131016055332/http://graphics.stanford.edu/~mmp/chapters/pbrt_chapter7.pdf)

Alan V Oppenheim, Ronald W. Schafer. Discrete-Time Signal Processing, 3rd edition

