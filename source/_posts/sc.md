---
title: Switched Capacitor Circuits
date: 2024-12-28 15:53:24
tags:
categories:
- analog
mathjax: true
---

![image-20260419092746250](sc/image-20260419092746250.png)



## Sampling Switch

> Kwantae Kim, Integrated Analog Systems D - Lecture 10 (ADC) [[https://youtu.be/IEdbLNJb9wQ](https://youtu.be/IEdbLNJb9wQ)]

*TODO* &#128197;

![image-20260426175351437](sc/image-20260426175351437.png)





## Switched-Capacitor Filter

***switched-Capacitor Resistor***

![image-20260319234852885](sc/image-20260319234852885.png)

> [[https://youtu.be/G0lzrMll-Ho](https://youtu.be/G0lzrMll-Ho)], [[https://youtu.be/eMOFMjuKiJQ](https://youtu.be/eMOFMjuKiJQ)]

![image-20260319235853713](sc/image-20260319235853713.png)

Due to not taking loading $C_2$ into account, actual switched-capacitor filter deviate from equivalent $R_{SC}$ + $C_2$ low pass filter as $f_p$ approaching to $f_s$

![image-20260320213653416](sc/image-20260320213653416.png)



![image-20260320225532492](sc/image-20260320225532492.png)
$$
\color{red}H(z) =\frac{V_{OUT}(z)}{V_{IN}(z)}=\frac{C_1z^{-1/2}}{C_1+C_2}\frac{1}{1-\frac{C_2}{C_1+C_2}z^{-1}}
$$


---

![image-20260320225157429](sc/image-20260320225157429.png)



![image-20260320225029809](sc/image-20260320225029809.png)

> [[https://youtu.be/eMOFMjuKiJQ](https://youtu.be/eMOFMjuKiJQ)]




## Track-and-Hold (TH)

![image-20260301151636821](sc/image-20260301151636821.png)

![image-20260301151806948](sc/image-20260301151806948.png)

![image-20260301152756691](sc/image-20260301152756691.png)

![image-20260301152723365](sc/image-20260301152723365.png)

![image-20260301153439749](sc/image-20260301153439749.png)
$$
H_\mathrm{TH}(f) \approx \frac{1}{2}
\left(
    1 + \mathrm{sinc}\left( \frac{f}{2f_s} \right)e^{-j\pi f T_s/2}
\right)
$$



![image-20260301154610913](sc/image-20260301154610913.png)

---

***PSS+PAC SImulaiton*** [[https://youtu.be/VLdcY76V9Ss](https://youtu.be/VLdcY76V9Ss)]

![image-20260304214124216](sc/image-20260304214124216.png)



## Sample-and-Hold (SH)

> ***Zero-Order Hold***

![image-20260301151336134](sc/image-20260301151336134.png)

![image-20260301155443477](sc/image-20260301155443477.png)

Given $\color{red}T_p = T_s$
$$
H_\mathrm{SH}(f) \approx
    \mathrm{sinc}\left( \frac{f}{f_s} \right)e^{-j\pi f T_s}
$$





![image-20260301155553174](sc/image-20260301155553174.png)



---



![image-20240928101832121](sc/image-20240928101832121.png)
$$
h_{ZOH}(t) = \text{rect}(\frac{t}{T} - \frac{1}{2}) = \left\{ \begin{array}{cl}
1 & : \ 0 \leq t \lt T \\
0 & : \ \text{otherwise}
\end{array} \right.
$$
The effective frequency response is the continuous Fourier transform of the impulse response
$$
H_{ZOH}(f) = \mathcal{F}\{h_{ZOH}(t)\} = T\frac{1-e^{j2\pi fT}}{j2\pi fT}=Te^{-j\pi fT}\text{sinc}(fT)
$$
where $\text{sinc}(x)$ is the normalized sinc function $\frac{\sin(\pi x)}{\pi x}$

The Laplace transform transfer function of the ZOH is found by substituting $s=j2\pi f$
$$
H_{ZOH}(s) = \mathcal{L}\{h_{ZOH}(t)\}=\frac{1-e^{-sT}}{s}
$$

![image-20260301145922192](sc/image-20260301145922192.png)

![image-20260301145958979](sc/image-20260301145958979.png)




## Clock Feedthrough

> aka. **LO leakage**

*TODO* &#128197;




## Integrator

*TODO* &#128197;





> [[https://www.eecg.utoronto.ca/~johns/ece1371/slides/10_switched_capacitor.pdf](https://www.eecg.utoronto.ca/~johns/ece1371/slides/10_switched_capacitor.pdf)]
>
> [[https://www.seas.ucla.edu/brweb/papers/Journals/BRWinter17SwCap.pdf](https://www.seas.ucla.edu/brweb/papers/Journals/BRWinter17SwCap.pdf)]
>
> [[https://class.ece.iastate.edu/ee508/lectures/EE%20508%20Lect%2029%20Fall%202016.pdf](https://class.ece.iastate.edu/ee508/lectures/EE%20508%20Lect%2029%20Fall%202016.pdf)]



## reference

Boris Murmann. EE315A VLSI Signal Conditioning Circuits [[pdf](https://picture.iczhiku.com/resource/eetop/SyIgQJfyzyuDhBXc.pdf)]

Kwantae Kim. ELEC-E3530 Integrated Analog Systems D (5 ECTS) [[video](https://youtube.com/playlist?list=PLmK06TkPUUKo-2LmZfhBpbcLTjFOxk2WJ)] [[github](https://github.com/KwantaeKim/ELEC-E3530)]

R. S. Ashwin Kumar, Analog circuits for signal processing [[https://home.iitk.ac.in/~ashwinrs/2022_EE698W.html](https://home.iitk.ac.in/~ashwinrs/2022_EE698W.html)]

R. Gregorian and G. C. Temes. Analog MOS Integrated Circuits for Signal Processing. Wiley-Interscience, 1986 [[pdf](https://picture.iczhiku.com/resource/eetop/SHkTDjaejpdzPCBv.pdf)]

Christian-Charles Enz. "High precision CMOS micropower amplifiers" [[pdf](https://picture.iczhiku.com/resource/eetop/wYItQFykkAQDFccB.pdf)]

Negar Reiskarimian. CICC 2025 Insight: Switched Capacitor Circuits [[https://youtu.be/SL3-9ZMwdJQ](https://youtu.be/SL3-9ZMwdJQ)]
