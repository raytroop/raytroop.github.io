---
title: From phase noise to Jitter
date: 2022-03-17 18:58:38
tags:
- phase noise
- jee
- absolute jitter
categories:
- analog
mathjax: true
---

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

![image-20220415100034220](phasenoise-2-jitter/image-20220415100034220.png)



Of course, it apply to conventional pnoise simulation.

On the other hand, output rms voltage noise, $V_{out,rms}$ divied by slope should be close to $J_{ee,rms}$
$$
J_{ee,rms} = \frac {V_{out,rms}}{slope}
$$

**reference**:

Nicola Da Dalt and Ali Sheikholeslami. 2018. Understanding Jitter and Phase Noise: A Circuits and Systems Perspective (1st. ed.). Cambridge University Press, USA.

Kester, Walt. (2005). Converting Oscillator Phase Noise to Time Jitter.  [[pdf](https://www.analog.com/media/en/training-seminars/tutorials/MT-008.pdf)]

Drakhlis, B.. (2001). Calculate oscillator jitter by using phase-noise analysis: Part 2 of two parts. Microwaves and Rf. 40. 109-119. 
