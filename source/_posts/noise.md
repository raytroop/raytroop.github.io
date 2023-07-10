---
title: Noise Analysis
date: 2024-04-27 09:54:25
tags:
categories: noise
mathjax: true
---



## spectrum analyzer

We tried to plot a *power spectral density* together with something that we want to interpret as a *power spectrum*

> - *spectrum* of a periodic signal
> - *spectral density* of a broadband signal such as noise
>
> Sine-wave components are located in individual FFT bins, but broadband signals like noise have their power spread over all FFT bins!
>
> The **noise floor** depends on the *length of the FFT*

[[http://individual.utoronto.ca/schreier/lectures/2015/1.pdf](http://individual.utoronto.ca/schreier/lectures/2015/1.pdf)]

![image-20240522214004545](noise/image-20240522214004545.png)

signal tone power
$$
P_{\text{sig}} = 2 \frac{X_{w,sig}^2}{S_1^2}
$$

noise power
$$
P_n = \frac{X_{w,n}^2}{S_2}
$$

Then, displayed **SNR** is obtained
$$\begin{align}
\mathrm{SNR} &= 10\log10\left(\frac{X_{w,sig}^2}{X_{w,n}^2}\right) \\
&= 10\log_{10}\left(\frac{P_{\text{sig}}}{P_n}\right) + 10\log_{10}\left(\frac{S_1^2}{2S_2}\right) \\
&= \mathrm{SNR}'-10\log_{10}\left(\frac{2S_2}{S_1^2}\right) \\
&= \mathrm{SNR}'-10\log_{10}(2\cdot\mathrm{NBW}) \\
\end{align}$$

> *DFT's output* $\mathrm{SNR}$

```matlab
for N=[2^6 2^8 2^10 2^12]
  wd = rectwin(N);
  nbw = enbw(wd)/N;
  snr_shift = 10*log10(nbw * 2);
  disp(snr_shift);
end
```

output:

```
-15.0515

-21.0721

-27.0927

-33.1133
```

![image-20240522214340882](noise/image-20240522214340882.png)




> The solution to the scaling problem in the case of a PSD obtained from a sine-wave scaled FFT is similarly simple. All we need do is provide the value of **NBW**



> *APPENDIX A - SPECTRAL ESTIMATION - A.2 Scaling and Noise Bandwidth*
>
> Pavan, Shanthi, Richard Schreier, and Gabor Temes. (2016) 2016. Understanding Delta-Sigma Data Converters. 2nd ed. Wiley.



- For a filter with infinitely steep roll-off, the noise bandwidth (**NBW**) is equal to the filter's bandwidth,
- while for a filter with a single-pole roll-off, **NBW** is 2 times the 3-dB bandwidth




##  Switched-Capacitor Filters

The **aliasing of the noise**, or **noise folding**, plays an important role in switched-capacitor as it does in all switched-capacitor filters

![image-20240425215938141](noise/image-20240425215938141.png)

Assume for the moment that the switch is *always closed* (that there is no hold phase), the single-sided noise density would be

![image-20240428182816109](noise/image-20240428182816109.png)

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


![image-20240428225949327](noise/sample_impulse_hold.drawio.svg)

> $$
> X(j\Omega)d\Omega = \frac{1}{T_c}X(e^{j\omega})d\omega  
> $$
>
> ref. *[[Sampling of Continuous Time Signals]](https://raytroop.github.io/2022/05/01/sampling-dft)* of EQ.(31) in the blog


![image-20240428225949327](noise/image-20240428225949327.png)





![image-20240425220400924](noise/image-20240425220400924.png)

where $m$ is the duty cycle

![image-20240427183257203](noise/image-20240427183257203.png)

![image-20240427183349642](noise/image-20240427183349642.png)

![image-20240427183516540](noise/image-20240427183516540.png)

![image-20240427183458649](noise/image-20240427183458649.png)

> - Calculate autocorrelation function of noise at the output of the RC filter
> - Calculate the spectrum by taking the **discrete** time Fourier transform of the autocorrelation function



![image-20240427183700971](noise/image-20240427183700971.png)



![image-20240427195202127](noise/image-20240427195202127.png)

- $Vo_{[n-1]}$ decay
- $Vo_{[n]}$ charge C



## Noise Aliasing

![SamplingProcess.drawio](noise/SamplingProcess.drawio.svg)

Where impulse train or "shah" function is defined as
$$
\amalg(t) = T\sum_{i=-\infty}^{\infty}\delta(x-iT)
$$
where $T$ defines the period, or sampling rate. Its Fourier transform is $2\pi \delta(\omega-i\frac{2\pi}{T})$

**Multiplication Property** of Fourier Transform
$$
x_1(t)x_2(t)\overset{FT}{\longrightarrow}\frac{1}{2\pi}X_1(\omega)*X_2(\omega)
$$


Due to $A = B+2C$, the noise in the discrete time integrated from DC to $f_s/2$ equals that of continuous time in all frequency range.

> The DFT spectrum is periodic with period **N**
>
> The DTFT spectrum is periodic  with period $2\pi$
>
> As a conclusion, the spectrum beyond $f_s/2$​ is **redundant** and don't provide information



---

The frequencies $f_{\text{sig}}$ and $N· f_s ±f_{\text{sig}}$ (N integer), are **indistinguishable** in the **discrete time domain**.

![image-20220626000016184](noise/image-20220626000016184.png)

> In order to prevent aliasing, we need $f_{\text{sig,max}}\lt \frac{f_s}{2}$. The sampling rate $f_s=2\cdot f_{\text{sig,max}}$ is called the **Nyquist Rate**.
>
> Two solution possibilities
>
> 1.  Sample fast enough to cover all spectral components, including "parasitic" ones outside band of interest
> 2. Limit $f_{\text{sig,max}}$ through filtering - Filter out "parasitic" ones 



Given below sequence
$$
X[n] =A e^{j\omega _0 T_s n}
$$

1. $kf_s + \Delta f$

$$\begin{align}
x[n] &= Ae^{j\left( kf_s+\Delta f \right)2\pi T_sn} + Ae^{j\left( -kf_s-\Delta f \right)2\pi T_sn} \\
&= Ae^{j\Delta f\cdot 2\pi T_sn} + Ae^{-j\Delta f\cdot 2\pi T_sn}
\end{align}$$

2. $kf_s - \Delta f$

$$\begin{align}
x[n] &= Ae^{j\left( kf_s-\Delta f \right)2\pi T_sn} + Ae^{j\left( -kf_s+\Delta f \right)2\pi T_sn} \\
&= Ae^{-j\Delta f\cdot 2\pi T_sn} + Ae^{j\Delta f\cdot 2\pi T_sn}
\end{align}$$

> With sampling frequency $\frac{1}{T_s}$, continuous signal of $\frac{1}{2T_s}+\Delta f$ and  $-\frac{1}{2T_s}+\Delta f$ can not be distinguished
> *real signal*

![image-20230518232314980](noise/image-20230518232314980.png)



> Generally, The frequencies $f_{\text{sig}}$ and $N· f_s ±f_{\text{sig}}$ (N integer), are **indistinguishable** in the **discrete time domain**.





## reference

David Herres, The difference between signal under-sampling, aliasing, and folding URL: [https://www.testandmeasurementtips.com/the-difference-between-signal-under-sampling-aliasing-and-folding-faq/](https://www.testandmeasurementtips.com/the-difference-between-signal-under-sampling-aliasing-and-folding-faq/)

Pharr, Matt; Humphreys, Greg. (28 June 2010). Physically Based Rendering: From Theory to Implementation. Morgan Kaufmann. ISBN 978-0-12-375079-2. [Chapter 7 (Sampling and reconstruction)](https://web.archive.org/web/20131016055332/http://graphics.stanford.edu/~mmp/chapters/pbrt_chapter7.pdf)

Kundert, Ken. (2006). Simulating Switched-Capacitor Filters with SpectreRF.

Pavan, Schreier and Temes, "Understanding Delta-Sigma Data Converters, Second Edition" ISBN 978-1-119-25827-8

Boris Murmann, EE315B VLSI Data Conversion Circuits, Autumn 2013

\- Noise Analysis in Switched-Capacitor Circuits, ISSCC 2011 / tutorials

Tania Khanna, ESE568 Fall 2019, Mixed Signal Circuit Design and Modeling URL: [https://www.seas.upenn.edu/~ese568/fall2019/](https://www.seas.upenn.edu/~ese568/fall2019/)

Matt Pharr, Wenzel Jakob, and Greg Humphreys. 2016. Physically Based Rendering: From Theory to Implementation (3rd. ed.). Morgan Kaufmann Publishers Inc., San Francisco, CA, USA.

Bernhard E. Boser . Advanced Analog Integrated Circuits Switched Capacitor Gain Stages [[https://people.eecs.berkeley.edu/~boser/courses/240B/lectures/M05%20SC%20Gain%20Stages.pdf](https://people.eecs.berkeley.edu/~boser/courses/240B/lectures/M05%20SC%20Gain%20Stages.pdf)]

Alan V Oppenheim, Ronald W. Schafer. Discrete-Time Signal Processing, 3rd edition

R. Gregorian and G. C. Temes. Analog MOS Integrated Circuits for Signal Processing. Wiley-Interscience, 1986

