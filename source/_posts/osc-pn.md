---
title: Oscillator Phase Noise
date: 2024-10-16 12:16:48
tags:
categories:
- osc
mathjax: true
---

![image-20260616221239668](osc-pn/image-20260616221239668.png)

> Poddar, Ajay & Rohde, Ulrich & Apte, Anisha. (2013). How Low Can They Go?: Oscillator Phase Noise Model, Theoretical, Experimental Validation, and Phase Noise Measurements. Microwave Magazine, IEEE. [[http://time.kinali.ch/rohde/noise/how_low_can_they_go-2013-poddar_rohde_apte.pdf](http://time.kinali.ch/rohde/noise/how_low_can_they_go-2013-poddar_rohde_apte.pdf)]
>
> F. L. Traversa, M. Bonnin and F. Bonani, "The Complex World of Oscillator Noise: Modern Approaches to Oscillator (Phase and Amplitude) Noise Analysis," in *IEEE Microwave Magazine*, vol. 22, no. 7, pp. 24-32, July 2021 [[https://sci-hub.ru/10.1109/MMM.2021.3069535](https://sci-hub.ru/10.1109/MMM.2021.3069535)]

## Phase Noise Definition

![image-20250104080553842](osc-pn/image-20250104080553842.png)

> Eq. (3.25) is widely adopted by industry and academia



![image-20250104080619943](osc-pn/image-20250104080619943.png)

> *using the narrow angle assumption*, the two definitions above are equivalent
>
> If the *narrow angle* condition is not satisfied, however, the two definitions differ

---

> Sam Palermo, ECEN620: Network Theory Broadband Circuit Design Fall 2025, Lecture 7: Voltage-Controlled Oscillators[[https://people.engr.tamu.edu/spalermo/ecen620/lecture07_ee620_vcos.pdf](https://people.engr.tamu.edu/spalermo/ecen620/lecture07_ee620_vcos.pdf)]

![image-20260609234730501](osc-pn/image-20260609234730501.png)



## Phase Noise Profile

> Power Spectral Density of Brownian Motion despite non-stationary [[https://dsp.stackexchange.com/a/75043/59253](https://dsp.stackexchange.com/a/75043/59253)]



***white noise*** — $1/f^2$ Phase Noise Profile

![image-20250104084510063](osc-pn/image-20250104084510063.png)

![image-20250104084814395](osc-pn/image-20250104084814395.png)



> ![image-20250104085222610](osc-pn/image-20250104085222610.png)



![image-20250104084925644](osc-pn/image-20250104084925644.png)

![image-20250104085722649](osc-pn/image-20250104085722649.png)

---

![image-20250601101355166](osc-pn/image-20250601101355166.png)

> Sudhakar Pamarti. CICC 2020 ES2-2: Basics of Closed- and Open-Loop Fractional Frequency Synthesis [[https://youtu.be/t1TY-D95CY8](https://youtu.be/t1TY-D95CY8)]



---

---

***flicker noise*** — $1/f^3$ Phase Noise Profile
$$
S_{\phi n} = \frac{K}{f}\left(\frac{K_{VCO}}{2\pi f}\right)^2 \propto \frac{1}{f^3}
$$



---



![image-20250104092711462](osc-pn/image-20250104092711462.png)



> [[https://dsp.stackexchange.com/a/75152/59253](https://dsp.stackexchange.com/a/75152/59253)]



## Free-running Oscillator

![image-20250103224818171](osc-pn/image-20250103224818171.png)

> Note that $f_{min}$ is related to the observation time. The longer we observe the device under test, the smaller $f_{min}$ must be

![image-20250524081737793](osc-pn/image-20250524081737793.png)

---

![image-20250104111025626](osc-pn/image-20250104111025626.png)

---

> Ali Sheikholeslami ISSCC 2008 T5: Basics of Chip-to-Chip and Backplane Signaling

![image-20250524082246710](osc-pn/image-20250524082246710.png)





---

![image-20250606204607565](osc-pn/image-20250606204607565.png)

> B. Casper and F. O'Mahony, "Clocking Analysis, Implementation and Measurement Techniques for High-Speed Data Links-A Tutorial," in IEEE Transactions on Circuits and Systems I. [[https://people.engr.tamu.edu/spalermo/ecen689/clocking_analysis_hs_links_casper_tcas1_2009.pdf](https://people.engr.tamu.edu/spalermo/ecen689/clocking_analysis_hs_links_casper_tcas1_2009.pdf)]





## Leeson's Model — LTI

> M.H. Perrott, Short Course On Phase-Locked Loops and Their Applications Day 2, AM Lecture Basic *Building Blocks Voltage-Controlled Oscillators* [[https://www.cppsim.com/PLL_Lectures/day2_am.pdf](https://www.cppsim.com/PLL_Lectures/day2_am.pdf)]
>
> —, 6.976 High Speed Communication Circuits and Systems *Lecture 12 Noise in Voltage Controlled Oscillators* [[https://ocw.mit.edu/courses/6-976-high-speed-communication-circuits-and-systems-spring-2003/ceb3d539691d5393a29af71ae98afb62_lec12.pdf](https://ocw.mit.edu/courses/6-976-high-speed-communication-circuits-and-systems-spring-2003/ceb3d539691d5393a29af71ae98afb62_lec12.pdf)]

Leeson's model is outcome of ***linearized*** VCO noise analysis

![image-20260614183453498](osc-pn/image-20260614183453498.png)



![image-20260614183309639](osc-pn/image-20260614183309639.png)

Assuming voltage noise tone $(\omega_0+\omega_m)$  and $(\omega_0-\omega_m)$ are **independent** and **symmetric**

![two_offset_folding_into_pm_sidebands](osc-pn/two_offset_folding_into_pm_sidebands.svg)



---

***Leeson's limitations***

![image-20251122144811362](osc-pn/image-20251122144811362.png)



## Hajimiri's ISF— LTV in Time Domain

> A. Hajimiri and T. H. Lee, "A general theory of phase noise in electrical oscillators," in *IEEE Journal of Solid-State Circuits*, vol. 33, no. 2, pp. 179-194, Feb. 1998 [[paper](https://people.engr.tamu.edu/spalermo/ecen620/general_pn_theory_hajimiri_jssc_1998.pdf)], [[slides](http://www-smirc.stanford.edu/papers/Orals98s-ali.pdf)]
>
> —, RFIC 2024 Technical Lecture: *Noise in Oscillators from Understanding to Design*
>
> Thomas H. Lee. Linearity, Time-Variation, Phase Modulation and Oscillator Phase Noise [[https://class.ece.iastate.edu/djchen/ee507/PhaseNoiseTutorialLee.pdf](https://class.ece.iastate.edu/djchen/ee507/PhaseNoiseTutorialLee.pdf)]
>
> Aditya Varma Muppala, [[https://adityamuppala.github.io/assets/Notes_YouTube/Oscillators_ISF_model.pdf](https://adityamuppala.github.io/assets/Notes_YouTube/Oscillators_ISF_model.pdf)]

![image-20260613113055683](osc-pn/image-20260613113055683.png)

![image-20260621160607012](osc-pn/image-20260621160607012.png)



![image-20260623012755556](osc-pn/image-20260623012755556.png)

![image-20260621110835891](osc-pn/image-20260621110835891.png)



### Pure sinusoidal voltage

Consider the **ideal parallel *LC* network** — pure sinusoid wave

Suppose a current pulse with area $q$ suddenly changes the charge across the capacitor, its voltage changes by $\Delta v_c=\Delta q/C$

![phase_kick_decomposition_radial_tangential](osc-pn/phase_kick_decomposition_radial_tangential-1781624282026-1.svg)

Decompose the horizontal kick $\Delta\vec r=(\Delta x,0) $ and $\Delta x=\Delta v_C/A_0$, with tangential direction $\hat t=(-\sin\theta,\cos\theta)$ and radial direction  $\hat r=(\cos\theta,\sin\theta)$
$$
\Delta \phi = \arctan\left(\frac{\Delta\vec r\cdot \hat t}{1 + \Delta\vec r\cdot \hat r}\right) = \arctan\left(\frac{-\Delta x \sin \theta}{1 + \Delta x \cos \theta}\right)\approx -\frac{\Delta v_C}{A_0} \sin(\omega_0 \tau)
$$

![image-20260613191539886](osc-pn/image-20260613191539886.png)


Therefore, the **ISF of an ideal parallel LC resonator** can be expressed as $\boxed{\Gamma(\omega \tau)=-\sin(\omega_0 \tau)}$, which is independent of peak voltage value $A_0$ 

![image-20260622231558562](osc-pn/image-20260622231558562.png)

![image-20260623014318589](osc-pn/image-20260623014318589.png)

###  White-noise Folding

![image-20260623011047045](osc-pn/image-20260623011047045.png)

Suppose a low frequency sinusoidal perturbation current $i(t) = I_m \cos[(m\omega_0 +\Delta \omega)t]$,

$$\begin{align}
\phi(t) &= \frac{1}{q_\text{max}}\left[\frac{C_0}{2}\int_{-\infty}^t I_m\cos((m\omega_0 +\Delta \omega)\tau)d\tau + \sum_{n=1}^\infty C_n\int_{-\infty}^t I_m\cos((m\omega_0 +\Delta \omega)\tau)\cos(n\omega_0\tau)d\tau\right] \\
&= \frac{I_m}{q_\text{max}}\left[\frac{C_0}{2}\int_{-\infty}^t \cos((m\omega_0 +\Delta \omega)\tau)d\tau + \sum_{n=1}^\infty C_n\int_{-\infty}^t \frac{\cos((m\omega_0 + \Delta \omega+ n\omega_0)\tau)+ \cos((m\omega_0+\Delta \omega - n\omega_0)\tau)}{2}d\tau\right]
\end{align}$$

If $m=0$
$$
\phi(t) \approx \frac{I_0C_0}{2q_\text{max}\Delta \omega}\sin(\Delta\omega t)
$$
If $m\neq 0$ and $m=n$
$$
\phi(t) \approx \frac{I_mC_m}{2q_\text{max}\Delta \omega}\sin(\Delta\omega t)
$$

When performing the ***phase noise computation integral***, there will be a negligible contribution from all terms, other than $n=m$

![image-20260623011353874](osc-pn/image-20260623011353874.png)

> apply equation (18) derived from ***sinusoidal*** to ***white noise***

![image-20260623011536856](osc-pn/image-20260623011536856.png)

> ![image-20260621101558719](osc-pn/image-20260621101558719.png)



---

***Corrections to "A General Theory of Phase Noise in Electrical Oscillators"***

>  A. Hajimiri and T. H. Lee, "Corrections to "A General Theory of Phase Noise in Electrical Oscillators"," in *IEEE Journal of Solid-State Circuits*, vol. 33, no. 6, pp. 928-928, June 1998 [[https://sci-hub.se/10.1109/4.678662](https://sci-hub.se/10.1109/4.678662)]
>
>  L. Lu, Z. Tang, P. Andreani, A. Mazzanti and A. Hajimiri, "Comments on “Comments on “A General Theory of Phase Noise in Electrical Oscillators””," in *IEEE Journal of Solid-State Circuits*, vol. 43, no. 9, pp. 2170-2170, Sept. 2008 [[https://sci-hub.se/10.1109/JSSC.2008.2005028](https://sci-hub.se/10.1109/JSSC.2008.2005028)]

Noise power around the frequency $\color{blue}n\omega_0 + \Delta\omega$ causes two equal sidebands at $\omega_0 \pm \Delta\omega$. However, the 
noise power at $\color{blue}n\omega_0 - \Delta\omega$ has a similar effect as  mentioned in the paper. Therefore, twice the power of noise at  $n\omega_0 + \Delta\omega$ should be taken into account

![image-20260623010902374](osc-pn/image-20260623010902374.png)

![image-20260623010700154](osc-pn/image-20260623010700154.png)





Given $i(t) = I_m \cos[(m\omega_0 - \Delta \omega)t]$ and $m \ge 1$

$$\begin{align}
\phi(t) &= \frac{1}{q_\text{max}}\left[\frac{C_0}{2}\int_{-\infty}^t I_m\cos((m\omega_0 -\Delta \omega)\tau)d\tau + \sum_{n=1}^\infty C_n\int_{-\infty}^t I_m\cos((m\omega_0 -\Delta \omega)\tau)\cos(n\omega_0\tau)d\tau\right] \\
&= \frac{I_m}{q_\text{max}}\left[\frac{C_0}{2}\int_{-\infty}^t \cos((m\omega_0 -\Delta \omega)\tau)d\tau + \sum_{n=1}^\infty C_n\int_{-\infty}^t \frac{\cos((m\omega_0 - \Delta \omega+ n\omega_0)\tau)+ \cos((m\omega_0-\Delta \omega - n\omega_0)\tau)}{2}d\tau\right]
\end{align}$$



If $m\ge 1$ and $m=n$
$$
\phi(t) \approx \frac{I_mC_m}{2q_\text{max}\Delta \omega}\sin(\Delta\omega t)
$$
That is

|                          | $m = 0$                                                      | $m\gt 0$ & $m\omega_0+\Delta \omega$                         | $m\gt 0$ & $m\omega_0-\Delta \omega$                         |
| ------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| $\phi(t)$                | $\frac{I_0C_0}{2q_\text{max}\Delta \omega}\sin(\Delta\omega t)$ | $\frac{I_mC_m}{2q_\text{max}\Delta \omega}\sin(\Delta\omega t)$ | $\frac{I_mC_m}{2q_\text{max}\Delta \omega}\sin(\Delta\omega t)$ |
| $P_{SBC}(\Delta \omega)$ | $10\log(\frac{I_0^2C_0^2}{16q_\text{max}^2\Delta \omega^2})$ | $10\log(\frac{I_m^2C_m^2}{16q_\text{max}^2\Delta \omega^2})$ | $10\log(\frac{I_m^2C_m^2}{16q_\text{max}^2\Delta \omega^2})$ |

$$\begin{align}
\mathcal{L}\{\Delta \omega\} &= 10\log\left(\frac{I_0^2C_0^2}{16q_\text{max}^2\Delta \omega^2} +  2\frac{I_m^2C_m^2}{16q_\text{max}^2\Delta \omega^2}\right) = 10\log\left(\frac{\overline{i_n^2/\Delta f}\cdot \frac{C_0^2}{2} }{4q_\text{max}^2\Delta \omega^2} + \frac{\overline{i_n^2/\Delta f}\cdot\sum_{m=1}^\infty C_m^2 }{4q_\text{max}^2\Delta \omega^2}\right) \\
&= 10\log \frac{\overline{i_n^2/\Delta f}(C_0^2/2+\sum_{m=1}^\infty C_m^2)}{4q_\text{max}^2\Delta \omega^2} = 10\log \frac{\overline{i_n^2/\Delta f}\cdot \Gamma_\text{rms}^2}{2q_\text{max}^2\Delta \omega^2}
\end{align}$$



---

---

 [[pdf](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9530265)]

![image-20260616235441690](osc-pn/image-20260616235441690.png)

![image-20260621105213052](osc-pn/image-20260621105213052.png)



![image-20260617004658323](osc-pn/image-20260617004658323.png)



### 1/f-noise Upconversion

![image-20260623020547145](osc-pn/image-20260623020547145.png)

![image-20260617004812519](osc-pn/image-20260617004812519.png)

![image-20260617005703943](osc-pn/image-20260617005703943.png)


---

Suppose $c_0\neq 0$, corresponding phase noise in response to injected noise $i_n(t)$ is equal to:

$$
\phi_{n,c_0} = \int_{-\infty}^t c_0 i_n(\tau) d\tau \qquad \boxed{S_{\phi n,c_0}(f) = \frac{c_0^2}{\omega^2}S_i(f)= \frac{\mathcal{\Gamma}_\text{dc}^2}{\omega^2}S_i(f)}
$$



### Cyclostationary Noise Sources

Cyclostationary noise can be viewed as stationary noise, $i_{n0}(t)$, multiplied by a periodic envelope, $\alpha(\omega_0 t)$.

***Effective ISF* — *ISF* multiplied with *Noise Modulating Function (NMF)***

![image-20260617010019682](osc-pn/image-20260617010019682.png)

![image-20260617010125436](osc-pn/image-20260617010125436.png)

For Colpitts Oscillator, $\Gamma_\text{eff}(x)$ is different from $\Gamma(x)$, however  $\Gamma_\text{eff}(x)$ and $\Gamma(x)$ are almost identical for ring oscillator



### alternative derivation

> Michael Perrott August 12, 2008, Short Course On Phase-Locked Loops and Their Applications Day 2, AM Lecture *Basic Building Blocks Voltage-Controlled Oscillators* [[https://www.cppsim.com/PLL_Lectures/day2_am.pdf](https://www.cppsim.com/PLL_Lectures/day2_am.pdf)]

![image-20260624205523543](osc-pn/image-20260624205523543.png)

***White Noise Input***

![image-20260624210533972](osc-pn/image-20260624210533972.png)

***1/f Noise in Input Current***

![image-20260624210650690](osc-pn/image-20260624210650690.png)

***Current Noise Modulation***

![image-20260624211311029](osc-pn/image-20260624211311029.png)

![image-20260624211359445](osc-pn/image-20260624211359445.png)



### another alternative derivation



![image-20260627184837586](osc-pn/image-20260627184837586.png)



![image-20260627185121907](osc-pn/image-20260627185121907.png)

![another_isf.drawio](osc-pn/another_isf.drawio.svg)
$$
S_{\phi,USB} = \frac{S_n^{''}}{q_\text{max}^2\Delta\omega^2}\left(a_0^2+\sum_{k\neq0}a_k^2\right)=\frac{S_n^{''}}{q_\text{max}^2\Delta\omega^2}\left(\frac{c_0^2}{4}+\sum_{k=1}^\infty \frac{c_k^2}{2}\right)=\frac{S_n^{'}}{4q_\text{max}^2\Delta\omega^2}\left(\frac{c_0^2}{2}+\sum_{k=1}^\infty c_k^2\right)
$$
where $S_n^{''}$ is two sided PSD,  $S_n^{}$ is one sided PSD



### Diff. Pair Noise with ISF

![image-20260621114354471](osc-pn/image-20260621114354471.png)

Given $\Gamma_{MOS}$ shown as above slide
$$
F_{rms,MOS}^2 = \frac{1/4\cdot T_\text{w}}{T_0/2} = \frac{T_\text{w}}{2T_0}
$$

![diff_pair_isf_20260623.PNG](osc-pn/diff_pair_isf_20260623.PNG)

---

![image-20260624201443189](osc-pn/image-20260624201443189.png)

![image-20260624201510173](osc-pn/image-20260624201510173.png)







### ISF calculating

*TODO* &#128197;

***A. Direct Measurement of Impulse Response***

***B. Closed-Form Formula for the ISF***

***C. Calculation of ISF Based on the First Derivative***

![image-20260624205015362](osc-pn/image-20260624205015362.png)







## Murphy's Model — LTV in Frequency Domain

> C. Samori, A. L. Lacaita, F. Villa and F. Zappa, "Spectrum folding and phase noise in LC tuned oscillators," in *IEEE Transactions on Circuits and Systems II: Analog and Digital Signal Processing*, vol. 45, no. 7, pp. 781-790, July 1998 [[https://sci-hub.ru/10.1109/82.700925](https://sci-hub.ru/10.1109/82.700925)]
>
> D. Murphy, J. J. Rael and A. A. Abidi, "Phase Noise in LC Oscillators: A Phasor-Based Analysis of a General Result and of Loaded  Q ," in IEEE Transactions on Circuits and Systems I: Regular Papers, vol. 57, no. 6, pp. 1187-1203, June 2010 [[https://sci-hub.ru/10.1109/TCSI.2009.2030110](https://sci-hub.ru/10.1109/TCSI.2009.2030110)]



The differential pair plays two distinct roles. Toward its own noise it acts as a sampling gate — each transistor contributes only within the short conduction windows at the zero crossings — and the resulting injection is almost purely phase-modulating. 

Toward the tail noise it acts as a single-balanced mixer, commutating the upstream current with a square wave and folding it as a single sideband that splits equally into AM and PM



### Diff. Pair Noise

> For diff. pair noise, the diff. pair is its own ***noise gate***

![image-20260615005115044](osc-pn/image-20260615005115044.png)

![image-20260615005234730](osc-pn/image-20260615005234730.png)

A reference pulse train centered at $t=0$ would have plain positive coefficients ($\tfrac{T_w}{T_0}$, with $\operatorname{sinc} \approx 1$).
$$
c_n = \frac{1}{2}\cdot \frac{T_w}{T_0/2}\operatorname{sinc}\left(\frac{nT_w}{T_0/2}\right)=\frac{T_w}{T_0}\operatorname{sinc}\left(\frac{2nT_w}{T_0}\right)
$$
The real injection sits at $t=T_0/4$, and since the pulse-train period is $P=T_0/2$, that offset is exactly $P/2$ — a half-period shift. Every coefficient therefore picks up $(-1)^m$ — $e^{j2m\omega_0\cdot T_0/4}=e^{jm\pi}$
$$
c_{2m} = \underbrace{(-1)^m}_{\text{position}}\,
         \underbrace{\frac{T_w}{T_0}}_{\text{area / period}}\,
         \underbrace{\operatorname{sinc}\!\left(\frac{2mT_w}{T_0}\right)}_{\to\,1 \text{ as } T_w \ll T_0}
$$
![image-20260615005921381](osc-pn/image-20260615005921381.png)

Consequently, excess noise arises solely from the components at $\omega_0\pm \omega_m$, since all other spectral components lie outside the tank bandwidth and are therefore suppressed by the resonator's frequency-selective filtering

![image-20260620203920911](osc-pn/image-20260620203920911.png)



With *Cyclostationary Noise (Modulated Noise) [[https://raytroop.github.io/2024/04/27/noise/#cyclostationary-noise-modulated-noise](https://raytroop.github.io/2024/04/27/noise/#cyclostationary-noise-modulated-noise)]*

For one MOS, Two-Sided PSD is
$$
S_O = S_I \cdot \mathcal{D}\cdot \mathcal{h}^2 = 2kT\gamma g_m\cdot \frac{2T_W}{T_0}\cdot\frac{1}{4} = \frac{T_W}{2T_0}\cdot 2kT\gamma g_m
$$
yield **One-Sided PSD** of **one MOS**
$$
S_O' = \textcolor{blue}{\frac{T_W}{2T_0}}\cdot 4kT\gamma g_m
$$
![image-20260620204007657](osc-pn/image-20260620204007657.png)

The **single-tone analysis** establishes that the differential-pair current is injected as **almost pure phase noise**, while **summing the white-noise power over all harmonics** of the gating function ($\overline{H^2}=T_W/2T_0 $) sets its **magnitude**; together these yield the differential-pair contribution to the oscillator phase noise.

 

---

phase noise is independent of the transconductance of the transistors

![img](osc-pn/image-20260618063842453.png)



### Tail Noise

> For the tail noise, the **diff. pair is a mixer**

![image-20260620171318943](osc-pn/image-20260620171318943.png)
$$
V_{AM} = \tfrac{1}{2}\big(C_+ + \overline{C}_-\big) = \tfrac{1}{2}\Big(\tfrac{c_1^* i}{2} + \tfrac{c_3^* i}{2}\Big)\qquad
V_{PM} = \tfrac{1}{2}\big(C_+ - \overline{C}_-\big) = \tfrac{1}{2}\Big(\tfrac{c_1^* i}{2} - \tfrac{c_3^* i}{2}\Big)
$$
$V_{AM}\approx V_{PM}$ for a square wave $|c_1|=3|c_3|$ — modulated tail noise is divided into ***AM and phase noise almost equally***
$$
S_{I,PN} = S_{nI,T} \cdot \mathcal{D}\cdot \mathcal{h}^2 \cdot \frac{1}{2} = S_{nI,T} \cdot 1 \cdot \frac{1}{4}\cdot \frac{1}{2} = \boxed{\frac{1}{8}\cdot S_{nI,T}}
$$
The commutation folds  tail noise as **a (near) single sideband**, which is equivalent to equal AM and PM — and only the PM half counts toward phase noise

Noise at $\boxed{2\omega_0 \pm\omega_m}$ dominate phase noise due to $|c_1|, |c_3| \gg |c_{2m+1}| \space\space\space\space \forall m>1$

![image-20260620234423406](osc-pn/image-20260620234423406.png)

---

> E. Hegazi, H. Sjoland and A. Abidi, "A filtering technique to lower oscillator phase noise," *2001 IEEE International Solid-State Circuits Conference. Digest of Technical Papers. ISSCC (Cat. No.01CH37177)*, San Francisco, CA, USA, 2001 [[paper](https://engineering.purdue.edu/oxidemems/conferences/isscc2001/DATA/D23_4.pdf), [slides](https://engineering.purdue.edu/oxidemems/conferences/isscc2001/DATA/SS23_4.pdf)]

![image-20260624165720693](osc-pn/image-20260624165720693.png)



## Demir's Model — NLTV

> A. Demir, A. Mehrotra and J. Roychowdhury, "Phase noise in oscillators: a unifying theory and numerical methods for characterization," in *IEEE Transactions on Circuits and Systems I: Fundamental Theory and Applications*, vol. 47, no. 5, pp. 655-674, May 2000 [[https://sci-hub.se/10.1109/81.847872](https://sci-hub.se/10.1109/81.847872)]


Demir's theory is essentially Floquet theory applied to the limit cycle of an autonomous oscillator, and the PPV is one specific Floquet vector

![image-20251122143914081](osc-pn/image-20251122143914081.png)

![image-20250920101142887](osc-pn/image-20250920101142887.png)

### PPV (Perturbation Projection Vector)

> A. Demir and J. Roychowdhury, "A reliable and efficient procedure for oscillator PPV computation, with phase noise macromodeling applications," in *IEEE Transactions on Computer-Aided Design of Integrated Circuits and Systems*, vol. 22, no. 2, pp. 188-197, Feb. 2003  [[https://sci-hub.se/10.1109/TCAD.2002.806599](https://sci-hub.se/10.1109/TCAD.2002.806599)]
>
> Helene Thibieroz, Customer Support CIC. Using Spectre RF Noise-Aware PLL Methodology to Predict PLL Behavior Accurately  [[https://citeseerx.ist.psu.edu/document?repid=rep1&type=pdf&doi=3056e59ea76165373f90152f915a829d25dabebc](https://citeseerx.ist.psu.edu/document?repid=rep1&type=pdf&doi=3056e59ea76165373f90152f915a829d25dabebc)]
>
> Aditya Varma Muppala. Perturbation Projection Vector (PPV) Theory | Oscillators 11 | MMIC 16 [[youtu.be](https://youtu.be/rbbHfZGT6Jo), [notes](https://adityamuppala.github.io/assets/Notes_YouTube/PPV_Theory_Notes.pdf)]





### Limit Cycles

> [[https://adityamuppala.github.io/assets/Notes_YouTube/MMIC_Limit_Cycles.pdf](https://adityamuppala.github.io/assets/Notes_YouTube/MMIC_Limit_Cycles.pdf)]

***Nonlinear*** Dynamics

 ![image-20250622202023590](osc-pn/image-20250622202023590.png)

![image-20250920101927173](osc-pn/image-20250920101927173.png)



### Lorentzian spectrum

![image-20240720134811859](osc-pn/image-20240720134811859.png)

We typically use the two spectra, $S_{\phi n}(f)$ and $S_{out}(f)$, interchangeably, but we must resolve these inconsistencies. **voltage spectrum**  is called **Lorentzian spectrum**

---

The periodic signal $x(t)$ can be expanded in Fourier series as:

![image-20240720141514040](osc-pn/image-20240720141514040.png)

Assume that the signal is subject to *excess phase noise*, which is modeled by adding a **time-dependent** noise component $\alpha(t)$. The noisy signal can be written $x(t+\alpha(t))$, the added excess phase $\phi(t)= \frac{\alpha(t)}{\omega_0}$

> ![image-20250103211650043](osc-pn/image-20250103211650043.png)



The autocorrelation of the noisy signal is by definition:

![image-20240720141525576](osc-pn/image-20240720141525576.png)

The *autocorrelation averaged over time* results in:

![image-20240720141659415](osc-pn/image-20240720141659415.png)

By taking the Fourier transform of the autocorrelation, the spectrum of the signal $x(t + \alpha(t))$​ can be expressed as

![image-20240720141813256](osc-pn/image-20240720141813256.png)

It is also interesting to note how the integral in *Equation 9.80* around each harmonic is equal to the power of the harmonic itself $|X_n|^2$

The integral $S_x(f)$ around harmonic is
$$\begin{align}
P_{x,n} &= \int_{f=-\infty}^{\infty} |X_n|^2\frac{\omega_0^2n^2c}{\frac{1}{4}\omega_0^4n^4c^2+(\omega +n\omega_0)^2}df \\
&= |X_n|^2\int_{\Delta f=-\infty}^{\infty}\frac{2\beta}{\beta^2+(2\pi\cdot\Delta f)^2}d\Delta f \\
&= |X_n|^2\frac{1}{\pi}\arctan(\frac{2\pi \Delta f}{\beta})|_{-\infty}^{\infty} \\
&= |X_n|^2
\end{align}$$



***The phase noise does not affect the total power in the signal, it only affects its distribution***

- Without phase noise, $S_v(f)$ is a series of impulse functions at the harmonics of $f_o$.
- With phase noise, the impulse functions spread, becoming fatter and shorter but retaining the *same total power*



> ![image-20250626213351673](osc-pn/image-20250626213351673.png)
>
> [[https://community.cadence.com/cadence_technology_forums/f/rf-design/51484/comparing-transient-noise-pnoise-and-pnoise-with-lorentian-approximation-of-a-ring-oscillator/1382911](https://community.cadence.com/cadence_technology_forums/f/rf-design/51484/comparing-transient-noise-pnoise-and-pnoise-with-lorentian-approximation-of-a-ring-oscillator/1382911)]



---

![image-20250815232359572](osc-pn/image-20250815232359572.png)

![image-20250815234653864](osc-pn/image-20250815234653864.png)



## Phase Perturbation

> Chembiyan T, "Brownian Motion And The Oscillator Phase Noise" [[link](https://www.linkedin.com/posts/chembiyan-t-0b34b910_vco-perturbed-by-a-brownian-motion-activity-6994691057045159936-nqaN?utm_source=share&utm_medium=member_desktop)]
>
> —, "Jitter and Phase Noise in Oscillators" [[link](https://www.linkedin.com/posts/chembiyan-t-0b34b910_jitter-and-phase-noise-activity-7028431979649929216-KsZw?utm_source=share&utm_medium=member_desktop)]
>
> —, "Jitter and Phase Noise in Phase Locked Loops" [[link](https://www.linkedin.com/posts/chembiyan-t-0b34b910_jitter-and-phase-noise-activity-7031985595304345600-uSx3?utm_source=share&utm_medium=member_desktop)]
>
> —, "PLLs and reference spurs" [[link](https://www.linkedin.com/posts/chembiyan-t-0b34b910_pll-rfdesign-circuits-activity-7111435571448713216-9jng?utm_source=share&utm_medium=member_desktop)]




### w/ stationary noise with Gaussian PDF

![image-20241227233228376](osc-pn/image-20241227233228376.png)

![image-20241228022311313](osc-pn/image-20241228022311313.png)

---

If keep $\phi_{rms}$ in $R_x(\tau)$, i.e.
$$
R_x(\tau)=\frac{A^2}{2}e^{-\phi_{rms}^2}\cos(2\pi f_0 \tau)e^{R_\phi(\tau)}\approx \frac{A^2}{2}e^{-\phi_{rms}^2}\cos(2\pi f_0 \tau)(1+R_\phi(\tau))
$$
The PSD of the signal is
$$
S_x(f) = \mathcal{F} \{ R_x(\tau) \} = \frac{P_c}{2}e^{-\phi_{rms}^2}\left[S_\phi(f+f_0)+S_\phi(f-f_0)\right] + \frac{P_c}{2}e^{-\phi_{rms}^2}\left[\delta(f+f_0)+\delta(f-f_0)\right]
$$
&#10071;&#10071;above Eq **isn't** consistent with stationary white noise process - the following section



### w/ stationary white noise



![image-20241207091104944](osc-pn/image-20241207091104944.png)

Assuming that the delay line is *noiseless*

![image-20241207100921644](osc-pn/image-20241207100921644.png)

---

![image-20241207091457850](osc-pn/image-20241207091457850.png)

Expanding the cosine function we get
$$\begin{align}
R_y(t,\tau) &= \frac{A^2}{2}\left\{\cos(2\pi f_0\tau)E[\cos(\phi(t)-\phi(t-\tau))] - \sin(2\pi f_0\tau)E[\sin(\phi(t)-\phi(t-\tau))]\right\} \\
&+ \frac{A^2}{2}\left\{\cos(4\pi f_0(t+\tau/2-T_D))E[\cos(\phi(t)+\phi(t-\tau))] - \sin(4\pi f_0(t+\tau/2-T_D))E[\sin(\phi(t)+\phi(t-\tau))] \right\}
\end{align}$$

where, both the process $\phi(t)-\phi(t-\tau)$ and $\phi(t)+\phi(t-\tau)$ are independent of time $t$, i.e. $E[\cos(\phi(t)+\phi(t-\tau))] = m_{\cos+}(\tau)$, $E[\cos(\phi(t)-\phi(t-\tau))] = m_{\cos-}(\tau)$,  $E[\sin(\phi(t)+\phi(t-\tau))] = m_{\sin+}(\tau)$ and  $E[\sin(\phi(t)-\phi(t-\tau))] = m_{\sin-}(\tau)$

we obtain
$$\begin{align}
R_y(t,\tau) &= \frac{A^2}{2}\left\{\cos(2\pi f_0\tau)m_{\cos-}(\tau) - \sin(2\pi f_0\tau)m_{\sin-}(\tau)\right\} \\
&+ \frac{A^2}{2}\left\{\cos(4\pi f_0(t+\tau/2-T_D))m_{\cos+}(\tau) - \sin(4\pi f_0(t+\tau/2-T_D))m_{\sin+}(\tau) \right\}
\end{align}$$

The second term in the above expression is periodic in $t$ and to estimate its PSD, we compute the ***time-averaged* autocorrelation function**
$$
R_y(\tau) = \frac{A^2}{2}\left\{\cos(2\pi f_0\tau)m_{\cos-}(\tau) - \sin(2\pi f_0\tau)m_{\sin-}(\tau)\right\}
$$
![image-20241207095906575](osc-pn/image-20241207095906575.png)

After nontrivial derivation

![image-20241207104018395](osc-pn/image-20241207104018395.png)

![image-20241227205459845](osc-pn/image-20241227205459845.png)





---

> ![image-20241207103912086](osc-pn/image-20241207103912086.png)



### w/ Weiner process

![image-20241207103414365](osc-pn/image-20241207103414365.png)

![image-20241207105127885](osc-pn/image-20241207105127885.png)

The phase process $\phi(t)$ is also gaussian but with *an increasing **variance** which grows **linearly** with time* $t$

![image-20241207110524419](osc-pn/image-20241207110524419.png)

$$\begin{align}
R_y(t,\tau) &= \frac{A^2}{2}\left\{\cos(2\pi f_0\tau)E[\cos(\phi(t)-\phi(t-\tau))] - \sin(2\pi f_0\tau)E[\sin(\phi(t)-\phi(t-\tau))]\right\} \\
&+ \frac{A^2}{2}\left\{\cos(4\pi f_0(t+\tau/2-T_D)E[\cos(\phi(t)+\phi(t-\tau))] - \sin(4\pi f_0(t+\tau/2-T_D)E[\sin(\phi(t)+\phi(t-\tau))] \right\}
\end{align}$$



**The spectrum of $y(t)$ is determined by the asymptotic behavior of $R_y(t,\tau)$ as $t\to \infty$**

> &#10071;&#10071; $\lim_{t\to\infty}R_y(t,\tau)$ rather than *time-averaged autocorrelation function* of cyclostationary process, ref. Demir's paper



We define $\zeta(t, \tau)=\phi(t)+\phi(t-\tau) = \phi(t)-\phi(t-\tau) + 2\phi(t-\tau)$, the expected value of $\zeta(t,\tau)$ is 0, the variance is $\sigma_{\zeta}^2=(k\sigma)^2(\tau + 4(t-\tau))=(k\sigma)^2(4t-3\tau)$
$$
E[\cos(\zeta(t,\tau))]=\frac{1}{\sqrt{2\pi \sigma_{\zeta}^2}}\int_{-\infty}^{\infty}e^{-\zeta^2/2\sigma_{\zeta}^2}\cos(\zeta)d\zeta = e^{-\sigma_{\zeta}^2/2}=e^{-(k\sigma)^2(4t-\tau)}
$$
i.e., $\lim _{t\to \infty} E[\cos(\zeta(t,\tau))] = \lim_{t\to \infty}e^{-(k\sigma)^2(4t-\tau)} = 0$

For $E[\sin(\zeta(t,\tau))]$, we have
$$
E[\sin(\zeta(t,\tau))] = \frac{1}{\sqrt{2\pi \sigma_{\zeta}^2}}\int_{-\infty}^{\infty}e^{-\zeta^2/2\sigma_{\zeta}^2}\sin(\zeta)d\zeta
$$
i.e., $E[\sin(\zeta(t,\tau))]$ is *odd function*, therefore $E[\sin(\zeta(t,\tau))]=0$

Finally, we obtain

![image-20241207114053083](osc-pn/image-20241207114053083.png)

![image-20241227210018613](osc-pn/image-20241227210018613.png)

![image-20241207114805792](osc-pn/image-20241207114805792.png)



---

![image-20241207174403033](osc-pn/image-20241207174403033.png)

![image-20241207181038749](osc-pn/image-20241207181038749.png)

![image-20241208100556466](osc-pn/image-20241208100556466.png)





## ISF & PPV simulation

> David Dolt. ECEN 620 Network Theory - Broadband Circuit Design: "VCO ISF Simulation" [[https://people.engr.tamu.edu/spalermo/ecen620/ISF_SIM.pdf](https://people.engr.tamu.edu/spalermo/ecen620/ISF_SIM.pdf)]
>
> Hu, Yizhe. (2019). A Simulation Technique of Impulse Sensitivity Function (ISF) Based on Periodic Transfer Function (PXF). 10.13140/RG.2.2.32151.60323. [[link](https://www.researchgate.net/publication/331072119_A_Simulation_Technique_of_Impulse_Sensitivity_Function_ISF_Based_on_Periodic_Transfer_Function_PXF)]
>
> —, "Intuitive Understanding of Flicker Noise Reduction via Narrowing of Conduction Angle in Voltage-Biased Oscillators," in IEEE Transactions on Circuits and Systems II: Express Briefs, vol. 66, no. 12, pp. 1962-1966, Dec. 2019 [[https://sci-hub.se/10.1109/TCSII.2019.2896483](https://sci-hub.se/10.1109/TCSII.2019.2896483)]
>
> Aditya Varma Muppala, ISF Simulation in Cadence Using Transient Analysis | Oscillators 07 | MMIC 12 [[https://youtu.be/yiMn2rCtTXY](https://youtu.be/yiMn2rCtTXY)]
>
> Aditya Varma Muppala, Fast Simulation of ISF and PPV using PSS and PXF in Cadence | Oscillators 12 | MMIC 19 [[https://youtu.be/Lu6VEWEEdxo](https://youtu.be/Lu6VEWEEdxo)]
>
> S. Galeone and M. P. Kennedy, "A comparison of simulation strategies for estimating phase noise in oscillators," 2017 13th Conference on Ph.D. Research in Microelectronics and Electronics (PRIME), Giardini Naxos - Taormina, Italy, 2017 
>
> PPV values from pss/pnoise simulation in spectreRF [[https://community.cadence.com/cadence_technology_forums/f/rf-design/35062/ppv-values-from-pss-pnoise-simulation-in-spectrerf](https://community.cadence.com/cadence_technology_forums/f/rf-design/35062/ppv-values-from-pss-pnoise-simulation-in-spectrerf)]
>
> ISF Function Extraction in Cadence Virtuoso [[https://community.cadence.com/cadence_technology_forums/f/custom-ic-design/43969/isf-function-extraction-in-cadence-virtuoso](https://community.cadence.com/cadence_technology_forums/f/custom-ic-design/43969/isf-function-extraction-in-cadence-virtuoso)]



### ISF using Transient Analysis

![image-20241016211020230](osc-pn/image-20241016211020230.png)

![image-20241016211101204](osc-pn/image-20241016211101204.png)

![image-20241016211115630](osc-pn/image-20241016211115630.png)



> To compare the ring oscillator and VCO the **total injected charge** to both should be the **same**



### ISF using PSS + PXF

*TODO* &#128197;



### PPV using PSS + PXF

*TODO* &#128197;







## References

Jun Yin. ISSCC 2025 T10: mm-Wave Oscillator Design

Pietro Andreani. ISSCC 2011 T1: Integrated LC oscillators

—. ISSCC 2017 F2: Integrated Harmonic Oscillators

—. SSCS Distinguished Lecture: RF Harmonic Oscillators Integrated in Silicon Technologies [[https://www.ieeetoronto.ca/wp-content/uploads/2020/06/DL-Toronto.pdf](https://www.ieeetoronto.ca/wp-content/uploads/2020/06/DL-Toronto.pdf)]

—. ESSCIRC 2019 Tutorials: RF Harmonic Oscillators Integrated in Silicon Technologies [[https://youtu.be/k1I9nP9eEHE](https://youtu.be/k1I9nP9eEHE)]

—. "Harmonic Oscillators in CMOS—A Tutorial Overview," in IEEE Open Journal of the Solid-State Circuits Society, vol. 1, pp. 2-17, 2021 [[pdf](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9530265)]

C. Samori, ISSCC2016 T1 "Tutorial: Understanding Phase Noise in LC VCOs"

—, "Understanding Phase Noise in LC VCOs: A Key Problem in RF Integrated Circuits," in *IEEE Solid-State Circuits Magazine*, vol. 8, no. 4, pp. 81-91, Fall 2016 [[https://sci-hub.ru/10.1109/MSSC.2016.2573979](https://sci-hub.ru/10.1109/MSSC.2016.2573979)]

—, Phase Noise in LC Oscillators: From Basic Concepts to Advanced Topologies [[https://www.ieeetoronto.ca/wp-content/uploads/2020/06/DL-VCO-short.pdf](https://www.ieeetoronto.ca/wp-content/uploads/2020/06/DL-VCO-short.pdf)]

Akihide Sai, Toshiba. ISSCC 2023 T5: All-digital PLLs From Fundamental Concepts to Future Trends

A. Hajimiri, RFIC2024 "Noise in Oscillators from Understanding to Design"

Antonio Liscidini, ESSCIRC 2019 Tutorials: Phase Noise in Wireless Applications [[https://youtu.be/nGmQ0JdoSE4](https://youtu.be/nGmQ0JdoSE4)]

Aditya Varma Muppala. Oscillators [[https://youtube.com/playlist?list=PL9Trid0A4Da2fOmYTEjhAnUkGPxyiH7H6&si](https://youtube.com/playlist?list=PL9Trid0A4Da2fOmYTEjhAnUkGPxyiH7H6)]

P.E. Allen - 2003. ECE 6440 - Frequency Synthesizers: Lecture 160 – Phase Noise - II [[https://pallen.ece.gatech.edu/Academic/ECE_6440/Summer_2003/L160-PhNoII(2UP).pdf](https://pallen.ece.gatech.edu/Academic/ECE_6440/Summer_2003/L160-PhNoII(2UP).pdf)]

---

---

***ISF, PPV, and Flicker-Noise Analysis***



S. Levantino, P. Maffezzoni, F. Pepe, A. Bonfanti, C. Samori and A. L. Lacaita, "Efficient Calculation of the Impulse Sensitivity Function in Oscillators," in IEEE Transactions on Circuits and Systems II: Express Briefs, vol. 59, no. 10, pp. 628-632, Oct. 2012 [[https://sci-hub.se/10.1109/TCSII.2012.2208679](https://sci-hub.se/10.1109/TCSII.2012.2208679)]

S. Levantino and P. Maffezzoni, "Computing the Perturbation Projection Vector of Oscillators via Frequency Domain Analysis," in IEEE Transactions on Computer-Aided Design of Integrated Circuits and Systems, vol. 31, no. 10, pp. 1499-1507, Oct. 2012 [[https://sci-hub.se/10.1109/TCAD.2012.2194493](https://sci-hub.se/10.1109/TCAD.2012.2194493)]

---

---

Bae, Woorham, and Deog-Kyoon Jeong. *Analysis and Design of CMOS Clocking Circuits for Low Phase Noise*. Institution of Engineering and Technology, 2020.

Lacaita, Andrea Leonardo, Salvatore Levantino, and Carlo Samori. *Integrated frequency synthesizers for wireless systems*. Cambridge University Press, 2007.

Hegazi, Emad, Asad Abidi, and Jacob Rael. *The Designer's Guide to High-purity Oscillators*. [New York]: Kluwer Academic Publishers, 2005. *The Designer's Guide to High-Purity Oscillators*

A. A. Abidi and D. Murphy, "How to Design a Differential CMOS LC Oscillator," in IEEE Open Journal of the Solid-State Circuits Society, vol. 5, pp. 45-59, 2025 [[https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=10818782](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=10818782)]

Jaeha Kim. Lecture 8. Special Topics: Design Trade -Offs in LC -Tuned Oscillators [[https://ocw.snu.ac.kr/sites/default/files/NOTE/7033.pdf](https://ocw.snu.ac.kr/sites/default/files/NOTE/7033.pdf)]

M. Babaie, M. Shahmohammadi, R. B. Staszewski, (2019) "RF CMOS Oscillators for Modern Wireless Applications" River Publishers [[https://www.riverpublishers.com/pdf/ebook/RP_E9788793609488.pdf](https://www.riverpublishers.com/pdf/ebook/RP_E9788793609488.pdf)]

---

---

***Mathematical Background***

Jiří Lebl. **Notes on Diffy Qs: Differential Equations for Engineers** [[link](https://www.jirka.org/diffyqs/)]

Matt Charnley. **Differential Equations: An Introduction for Engineers** [[link](https://sites.rutgers.edu/matthew-charnley/course-materials/differential-equations-an-introduction-for-engineers/)]

Åström, K.J. & Murray, Richard. (2021). **Feedback Systems: An Introduction for Scientists and Engineers Second Edition** [[https://www.cds.caltech.edu/~murray/books/AM08/pdf/fbs-public_24Jul2020.pdf](https://www.cds.caltech.edu/~murray/books/AM08/pdf/fbs-public_24Jul2020.pdf)]

Strogatz, S.H. (2015). **Nonlinear Dynamics and Chaos: With Applications to Physics, Biology, Chemistry, and Engineering (2nd ed.)**. CRC Press [[https://www.biodyn.ro/course/literatura/Nonlinear_Dynamics_and_Chaos_2018_Steven_H._Strogatz.pdf](https://www.biodyn.ro/course/literatura/Nonlinear_Dynamics_and_Chaos_2018_Steven_H._Strogatz.pdf)]

Cadence Blog, "Resonant Frequency vs. Natural Frequency in Oscillator Circuits" [[link](https://resources.pcb.cadence.com/blog/2019-resonant-frequency-vs-natural-frequency-in-oscillator-circuits)]

Godone, A. & Micalizio, Salvatore & Levi, Filippo. (2008). RF spectrum of a carrier with a random phase modulation of arbitrary slope. [[https://sci-hub.se/10.1088/0026-1394/45/3/008](https://sci-hub.se/10.1088/0026-1394/45/3/008)]