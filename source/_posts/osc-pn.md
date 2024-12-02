---
title: Jitter and Phase Noise in Oscillators
date: 2024-10-16 12:16:48
tags:
categories:
- noise
mathjax: true
---



## Integration Limits

> Y. Zhao and B. Razavi, "Phase Noise Integration Limits for Jitter Calculation,"[[https://www.seas.ucla.edu/brweb/papers/Conferences/YZ_ISCAS_22.pdf](https://www.seas.ucla.edu/brweb/papers/Conferences/YZ_ISCAS_22.pdf)]

*TODO* &#128197;



## narrowband approximation & limitation

A sine wave with phase modulation is expressed as
$$
y(t) = A_0 \sin(2\pi f_0 t + \phi _0 +\phi (t))
$$
where $\phi (t)$ is a time-varying phase modulation function



Assuming a *narrowband phase modulation (PM)*, that is, the absolute amount of modulated phase is small enough

> *otherwise the modulation becomes frequency modulation (FM) and its analysis becomes more complex*

$$
y(t) \simeq A_0 \sin(2\pi f_0 t +\phi _0) + A_0 \phi (t)\cos(2\pi f_0 t + \phi _0)
$$

> Because $\cos \phi(t)$ and $\sin \phi(t)$ are approximated to $1$ and $\phi (t)$, respectively



The Fourier transform of $y(t)$ is
$$
Y(f) = \frac{1}{2}A_0 e^{j\phi _0}\delta(f-f_0) -\frac{1}{2}A_0e^{-j\phi_0}\delta(f+f_0)+\frac{1}{2}A_0e^{j\phi_0}\Phi(f-f_0)-\frac{1}{2}A_0e^{-j\phi_0}\Phi(f+f_0)
$$

> where $\Phi(f)$ is the Fourier transform pair of $\phi(t)$



The autocorrelation of $y(t)$ is

$$\begin{align}
R(\tau) &= E(y(t)y(t+\tau))\\
&= E([A_0\sin(2\pi f_0 t + \phi_0)+A_0\phi(t)\cos(2\pi f_0 t+\phi _0)]\\
&= \frac{1}{2}A_0^2 \cos(2\pi f_0 \tau)(1+R_{\phi}(\tau))
\end{align}$$

Fourier transform of $R(\tau)$ is
$$
S_y(f) = \frac{1}{4}A_0^2 \delta (f-f_0) + \frac{1}{4}A_0\delta(f+f_0) + \frac{1}{4}A_0^2S_\phi (f-f_0)+\frac{1}{4}A_0^2S_\phi (f+f_0)
$$
![image-20240511221119938](osc-pn/image-20240511221119938.png)



> Bae, Woorham; Jeong, Deog-Kyoon: 'Analysis and Design of CMOS Clocking Circuits for Low Phase Noise' (Materials, Circuits and Devices, 2020)



---



**approximation limitation**

**Don't** retain the same total power

![image-20240720101133749](osc-pn/image-20240720101133749.png)



## Leeson's model

Leeson's equation is an *empirical* expression that describes an oscillator's phase noise spectrum

![image-20240718230819186](osc-pn/image-20240718230819186.png)

Limitation:

​	that the PSD diverges to *infinity* for very low values of the frequency offset $f$​



## Lorentzian Spectrum

![image-20240720134811859](osc-pn/image-20240720134811859.png)

We typically use the two spectra, $S_{\phi n}(f)$ and $S_{out}(f)$, interchangeably, but we must resolve these inconsistencies. **voltage spectrum**  is called **Lorentzian spectrum**



---



The periodic signal $x(t)$ can be expanded in Fourier series as:

![image-20240720141514040](osc-pn/image-20240720141514040.png)

Assume that the signal is subject to excess phase noise, which is modeled by adding a time-dependent noise component $\alpha(t)$. The noisy signal can be written $x(t+\alpha(t))$, the added excess phase $\phi(t)= \frac{\alpha(t)}{\omega_0}$

The autocorrelation of the noisy signal is by definition:

![image-20240720141525576](osc-pn/image-20240720141525576.png)

The *autocorrelation averaged over time* results in:

![image-20240720141659415](osc-pn/image-20240720141659415.png)

By taking the Fourier transform of the autocorrelation, the spectrum of the signal $x(t + \alpha(t))$​ can be expressed as

![image-20240720141813256](osc-pn/image-20240720141813256.png)

It is also interesting to note how the integral in Equation 9.80 around each harmonic is equal to the power of the harmonic itself $|X_n|^2$

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





## VCO ISF Simulation

### PSS + PXF Method

> Yizhe Hu, "A Simulation Technique of Impulse Sensitivity Function (ISF) Based on Periodic Transfer Function (PXF)" [[https://bbs.eetop.cn/thread-869343-1-1.html](https://bbs.eetop.cn/thread-869343-1-1.html)]



*TODO* &#128197;



### Transient Method

> David Dolt. ECEN 620 Network Theory - Broadband Circuit Design: "VCO ISF Simulation" [[https://people.engr.tamu.edu/spalermo/ecen620/ISF_SIM.pdf](https://people.engr.tamu.edu/spalermo/ecen620/ISF_SIM.pdf)]



![image-20241016211020230](osc-pn/image-20241016211020230.png)

![image-20241016211101204](osc-pn/image-20241016211101204.png)

![image-20241016211115630](osc-pn/image-20241016211115630.png)



> To compare the ring oscillator and VCO the **total injected charge** to both should be the **same**



## Spurs

> Timing 101 #6: The Case of the Spurious Phase Noise, Silicon Labs,  [[Part I](https://community.silabs.com/s/share/a5U1M000000knzQUAQ/timing-101-6-the-case-of-the-spurious-phase-noise-part-i)], [[Part II](https://community.silabs.com/s/share/a5U1M000000knzQUAQ/timing-101-6-the-case-of-the-spurious-phase-noise-part-i?language=en_US)], [[Part III](https://community.silabs.com/s/share/a5U1M000000ko4DUAQ/timing-201-2-the-case-of-the-phase-noise-that-wasnt-part-2?language=en_US)]
>
> W. Rhee, "Design of high-performance CMOS charge pumps in phase-locked loops," *1999 IEEE International Symposium on Circuits and Systems (ISCAS)*, Orlando, FL, USA, 1999, pp. 545-548 vol.2 [[https://citeseerx.ist.psu.edu/document?repid=rep1&type=pdf&doi=3006edc15fdef2e71674d4170c10c62fd69f96a3](https://citeseerx.ist.psu.edu/document?repid=rep1&type=pdf&doi=3006edc15fdef2e71674d4170c10c62fd69f96a3)]
>
> Rhee, W. and Yu, Z., 2024. *Phase-Locked Loops: System Perspectives and Circuit Design Aspects*. John Wiley & Sons.
>
> H. -G. Ko, W. Bae, G. -S. Jeong and D. -K. Jeong, "Reference Spur Reduction Techniques for a Phase-Locked Loop," in *IEEE Access*, vol. 7, pp. 38035-38043, 2019 [[https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=8671476](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=8671476)]
>
> Mike Shuo-Wei Chen, CICC2020 ES 2-3: "Low-Spur PLL Architectures and Techniques"
>
> Saurabh Saxena, Problems in Charge Pump PLL - Reference Spur [[https://youtu.be/IcJOZAh9a1w?si=ehJ3ox90wN46_KMb](https://youtu.be/IcJOZAh9a1w?si=ehJ3ox90wN46_KMb)]
>
> Chembiyan T, PLLs and reference spurs. [[https://www.linkedin.com/posts/chembiyan-t-0b34b910_pll-rfdesign-circuits-activity-7111435571448713216-9jng?utm_source=share&utm_medium=member_desktop](https://www.linkedin.com/posts/chembiyan-t-0b34b910_pll-rfdesign-circuits-activity-7111435571448713216-9jng?utm_source=share&utm_medium=member_desktop)]



![chart](osc-pn/1695498362810.gif)

**spurs** are carrier or clock frequency spectral imperfections measured in the frequency domain just like phase noise. However, unlike phase noise they are *discrete* frequency components.

- Spurs are deterministic.

- Spur power is independent of bandwidth.

- Spurs contribute bounded peak jitter in the time domain.



***Sources of Spurs:***

- External (coupling from other noisy block)
  Supply, substrate, bond wires, etc.
- Internal (int-N/fractional-N operation)
  - **Frac spur**: Fractional divider (multi-modulus and frequency accumulation)
  - **Ref. spur**: PFD/charge pump/analog loop filter non-idealities, clock coupling





### reference spurs

*TODO* &#128197;





### charge pump mismatch

Matching of the CP currents is also a critical part of PLL design. Leakage and mismatch in the CP will lead to *deterministic jitter* on the PLL output

Any difference between the charging and discharging currents can cause static phase offset as well as *dynamic jitter*, known as **reference spur**



peak2peak deterministic jitter
$$
\text{DJ}_\text{PP} = \frac{\phi_{PP}}{2\pi}T_{osc}
$$


```matlab
kvco = 1e9;
Icp = 600e-6;
deltaI_Icp = 3e-2;
deltaI = deltaI_Icp*Icp;
ton = 100e-12;
C2 =0.5e-12;
Tosc = 1/15e9;

DJpp = kvco*deltaI*ton^2/(2*C2)*(deltaI_Icp + 1)*Tosc
```



## Wandering Spurs

Fractional-N frequency synthesizers exhibit strange moving spurs and pulsating spectra. These are manifestations of a phenomenon called "wandering spurs."

*TODO* &#128197;





## reference

A. Hajimiri and T. H. Lee, "A general theory of phase noise in electrical oscillators," in *IEEE Journal of Solid-State Circuits*, vol. 33, no. 2, pp. 179-194, Feb. 1998 [[paper](https://people.engr.tamu.edu/spalermo/ecen620/general_pn_theory_hajimiri_jssc_1998.pdf)], [[slides](http://www-smirc.stanford.edu/papers/Orals98s-ali.pdf)]

—, "Corrections to "A General Theory of Phase Noise in Electrical Oscillators"" [[https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=678662](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=678662)]

—, RFIC2024 "Noise in Oscillators from Understanding to Design"

Carlo Samori, "Phase Noise in LC Oscillators: From Basic Concepts to Advanced Topologies" [[https://www.ieeetoronto.ca/wp-content/uploads/2020/06/DL-VCO-short.pdf](https://www.ieeetoronto.ca/wp-content/uploads/2020/06/DL-VCO-short.pdf)]

—, "Understanding Phase Noise in LC VCOs: A Key Problem in RF Integrated Circuits," in *IEEE Solid-State Circuits Magazine*, vol. 8, no. 4, pp. 81-91, Fall 2016 [[https://picture.iczhiku.com/resource/eetop/whIgTikLswaaTVBv.pdf](https://picture.iczhiku.com/resource/eetop/whIgTikLswaaTVBv.pdf)]

—, ISSCC2016, "Understanding Phase Noise in LC VCOs"

F. L. Traversa, M. Bonnin and F. Bonani, "The Complex World of Oscillator Noise: Modern Approaches to Oscillator (Phase and Amplitude) Noise Analysis," in *IEEE Microwave Magazine*, vol. 22, no. 7, pp. 24-32, July 2021 [[https://iris.polito.it/retrieve/handle/11583/2903596/e384c433-b8f5-d4b2-e053-9f05fe0a1d67/MM%20noise%20-%20v5.pdf](https://iris.polito.it/retrieve/handle/11583/2903596/e384c433-b8f5-d4b2-e053-9f05fe0a1d67/MM%20noise%20-%20v5.pdf)]

Poddar, Ajay & Rohde, Ulrich & Apte, Anisha. (2013). How Low Can They Go?: Oscillator Phase Noise Model, Theoretical, Experimental Validation, and Phase Noise Measurements. Microwave Magazine, IEEE. [[http://time.kinali.ch/rohde/noise/how_low_can_they_go-2013-poddar_rohde_apte.pdf](http://time.kinali.ch/rohde/noise/how_low_can_they_go-2013-poddar_rohde_apte.pdf)]

Pietro Andreani, "RF Harmonic Oscillators Integrated in Silicon Technologies" [[https://www.ieeetoronto.ca/wp-content/uploads/2020/06/DL-Toronto.pdf](https://www.ieeetoronto.ca/wp-content/uploads/2020/06/DL-Toronto.pdf)]

Chembiyan T, "Brownian Motion And The Oscillator Phase Noise" [[link](https://www.linkedin.com/posts/chembiyan-t-0b34b910_vco-perturbed-by-a-brownian-motion-activity-6994691057045159936-nqaN?utm_source=share&utm_medium=member_desktop)]

—, "Jitter and Phase Noise in Oscillators" [[link](https://www.linkedin.com/posts/chembiyan-t-0b34b910_jitter-and-phase-noise-activity-7028431979649929216-KsZw?utm_source=share&utm_medium=member_desktop)]

—, "Jitter and Phase Noise in Phase Locked Loops" [[link](https://www.linkedin.com/posts/chembiyan-t-0b34b910_jitter-and-phase-noise-activity-7031985595304345600-uSx3?utm_source=share&utm_medium=member_desktop)]

—, "PLLs and reference spurs" [[link](https://www.linkedin.com/posts/chembiyan-t-0b34b910_pll-rfdesign-circuits-activity-7111435571448713216-9jng?utm_source=share&utm_medium=member_desktop)]

