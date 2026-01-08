---
title: Resonant Circuits
date: 2025-06-06 20:38:14
tags:
categories:
- analog
mathjax: true
---

A ***resonant circuit*** refers to an electrical circuit using circuit elements such as an inductor (L) and a capacitor (C) to cause resonance at a specific frequency. 

There are two types of resonant circuits: 

- series resonant circuits
- parallel resonant circuits 

In a series resonant circuit, the impedance of the circuit reaches its minimum value at resonance, whereas in a parallel resonant circuit, the impedance reaches its maximum value

![image-20251027213420942](resonant/image-20251027213420942.png)

---

![image-20260108233832631](resonant/image-20260108233832631.png)

> ***antiresonance***
>
> ![image-20260108234008061](resonant/image-20260108234008061.png)



## Resonant Frequency

> $\zeta \lt 1$: ***Complex-Conjugate Poles***, but not *resonant peak*
>
> $\zeta \lt \sqrt{2}/2$: ***resonant peak***

![image-20251205220247644](resonant/image-20251205220247644.png)



> [[https://lpsa.swarthmore.edu/Bode/underdamped/underdampedApprox.html](https://lpsa.swarthmore.edu/Bode/underdamped/underdampedApprox.html)]
>
> ![image-20251205233053573](resonant/image-20251205233053573.png)



---

> Prof. M. Green / U.C. Irvine EECS 270C / Winter 2013 [[pdf](https://picture.iczhiku.com/resource/eetop/WhKTaAlgfKwzLxXM.pdf)]

![image-20251205232150381](resonant/image-20251205232150381.png)
$$
s^2 + \frac{R}{L}s + \frac{1}{LC_L} = s^2 + 2\zeta \omega_n s + \omega_n^2
$$
where $\omega_n = \frac{1}{\sqrt{LC_L}}$ and $\zeta=\frac{R}{2}\sqrt{\frac{C_L}{L}}$

Resonant frequency is
$$
\omega_r = \omega_n \sqrt{1-2\zeta^2} = \frac{1}{\sqrt{LC_L}}\left(1-\frac{C_LR^2}{2L}\right)
$$
To have no resonant $\zeta^2 >\frac{1}{2}$, i.e
$$
\frac{L}{C_LR^2} < \frac{1}{2}
$$






## LC Resonator

![image-20240826223955851](resonant/image-20240826223955851.png)

> ***Complex Conjugate Zeros***



![image-20240826224132736](resonant/image-20240826224132736.png)

> ***Complex Conjugate Poles***
>
> $\zeta \to 0$ push $|G(s)\approx \frac{1}{2\zeta} \to+\infty$
>
> ![image-20251027212546424](resonant/image-20251027212546424.png)

![image-20240826224317197](resonant/image-20240826224317197.png)

---

![image-20240826224651954](resonant/image-20240826224651954.png)

![image-20240826224823886](resonant/image-20240826224823886.png)



## Frequency selectivity

> EEE 211 ANALOG ELECTRONICS [[https://www.ee.bilkent.edu.tr/~eee211/LectureNotes/Chapter%20-%2004.pdf](https://www.ee.bilkent.edu.tr/~eee211/LectureNotes/Chapter%20-%2004.pdf)]

###  Parallel resonance

![image-20251213165220671](resonant/image-20251213165220671.png)



assuming $i(t) = I_p\cos\omega_0 t$, where $\omega_0 =1/\sqrt{LC}$ , suppose all current flow into $R$
$$
V(t) = I_pR\cdot \cos\omega_0 t
$$
$I_C$, the current flow through $C$
$$
\color{red}I_C(t)=C\frac{dV(t)}{dt}=-C\omega_0\cdot I_pR\cdot \sin\omega_0 t
$$
Then, we have voltage between $L$, given $I_L = -I_C$
$$
V_L(t) = L\frac{dI_L(t)}{dt} = LC\omega_0^2\cdot I_pR\cdot \cos\omega_0 t = I_pR\cdot \cos\omega_0 t
$$


### Series resonance

![image-20251213165337258](resonant/image-20251213165337258.png)

assuming $V(t)=V_s\cos\omega_0t$, where $\omega_0 =1/\sqrt{LC}$ , suppose all current flow into $V_C+V_L=0$
$$
V_R(t) = V(t) = V_s\cos\omega_0t
$$
then
$$
I_s(t) = \frac{V_s}{R}\cos\omega_0 t
$$
$V_L(t)$ is obtained
$$
V_L(t) = L\frac{dI_s(t)}{dt} = -L\omega_0\cdot \frac{V_s}{R}\sin\omega_0 t
$$
Then
$$
V_C(t) = V(t) - (V_L(t) + V_R(t)) = -V_L(t)
$$
Therefore,  $I_C$ current flow through $C$
$$
I_C(t) = C\frac{dV_C(t)}{dt}= LC\omega_0^2\cdot \frac{V_s}{R}\cos\omega_0 t= \frac{V_s}{R}\cos\omega_0 t
$$
voltage potential between $L$ and $C$
$$
\color{red}V_m(t) = V_R(t) + V_L(t) = V_s\cos\omega_0t -L\omega_0\cdot \frac{V_s}{R}\sin\omega_0 t = V_s\sqrt{1+L/R^2C}\cos(\omega_0t+\phi)
$$
![image-20251213180419366](resonant/image-20251213180419366.png)



## Non ideal capacitor & inductor

> Tank Circuits/Impedances [[https://stanford.edu/class/ee133/handouts/lecturenotes/lecture5_tank.pdf](https://stanford.edu/class/ee133/handouts/lecturenotes/lecture5_tank.pdf)]
>
> Resonant Circuits  [[https://web.ece.ucsb.edu/~long/ece145b/Resonators.pdf](https://web.ece.ucsb.edu/~long/ece145b/Resonators.pdf)]
>
> Series & Parallel Impedance Parameters and Equivalent Circuits [[https://assets.testequity.com/te1/Documents/pdf/series-parallel-impedance-parameters-an.pdf](https://assets.testequity.com/te1/Documents/pdf/series-parallel-impedance-parameters-an.pdf)]
>
> ES Lecture 35: Non ideal capacitor, Capacitor Q and series RC to parallel RC conversion [[https://youtu.be/CJ_2U5pEB4o?si=4j4CWsLSapeu-hBo](https://youtu.be/CJ_2U5pEB4o?si=4j4CWsLSapeu-hBo)]



### Non ideal Capacitor

![image-20231224163730529](resonant/image-20231224163730529.png)

---

![image-20251009211423154](resonant/image-20251009211423154.png)

> ![image-20251009211708604](resonant/image-20251009211708604.png)

$$
Q_s = \frac{X_s}{R_s} = X_p\frac{Q_p^2}{Q_p^2+1}\cdot \frac{Q_p^2+1}{R_p} =\frac{Q_p^2}{R_p/X_p}=Q_p
$$


So long as $Q_s\gg 1$
$$\begin{align}
R_p &\approx Q_s^2R_s \\
C_p &\approx C_s
\end{align}$$


---



![image-20251011224853381](resonant/image-20251011224853381.png)

![image-20240119001309410](resonant/image-20240119001309410.png)






### Non ideal Inductor

![image-20231224163740411](resonant/image-20231224163740411.png)

So long as $Q_s\gg 1$
$$\begin{align}
R_p &\approx Q_s^2R_s \\
L_p &\approx L_s
\end{align}$$





## SRF (Self-Resonant Frequency)

> [Understanding RF Inductor Specifications, [https://www.ece.uprm.edu/~rafaelr/inel5325/SupportDocuments/doc671_Selecting_RF_Inductors.pdf](https://www.ece.uprm.edu/~rafaelr/inel5325/SupportDocuments/doc671_Selecting_RF_Inductors.pdf)]
>
> [RFIC-GPT Wiki, [https://wiki.icprophet.net/](https://wiki.icprophet.net/)]

![image-20240802210109935](resonant/image-20240802210109935.png)


$$
f_\text{SRF} = \frac{1}{2\pi \sqrt{LC}}
$$
The SRF of an inductor is the frequency at which the parasitic capacitance of the inductor resonates with the ideal inductance of the inductor, resulting in an extremely high impedance. The inductance only acts like an inductor below its SRF

![image-20241221092745311](resonant/image-20241221092745311.png)

- For **choking** applications, chose an inductor whose SRF is at or near the frequency to be attenuated

- For other applications, the SRF should be at least **10** times higher than the operating frequency

  it is more important to have a *relatively flat inductance curve* (constant inductance vs. frequency) near the required frequency



## reference

Hossein Hashemi, RF Circuits, [[https://youtu.be/0f3yZMvD2Jg?si=2c1Q4y6WJq8Jj8oN](https://youtu.be/0f3yZMvD2Jg?si=2c1Q4y6WJq8Jj8oN)]

Resonant Circuits: Resonant Frequency and Q Factor [[https://techweb.rohm.com/product/circuit-design/electric-circuit-design/18332/](https://techweb.rohm.com/product/circuit-design/electric-circuit-design/18332/)]

J. Nako, G. Tsirimokou, C. Psychalinos and A. S. Elwakil, "Approximation of First–Order Complex Resonators in the Frequency–Domain," in *IEEE Access*, vol. 13, pp. 54494-54503, 2025 [[pdf](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=10937072)]

How to generate **complex poles without inductor**? [[https://a2d2ic.wordpress.com/2020/02/19/basics-on-active-rc-low-pass-filters/](https://a2d2ic.wordpress.com/2020/02/19/basics-on-active-rc-low-pass-filters/)]

Visvesh Sathe. Resonant Clock Design for a Power-efficient, High-volume x86 -64 Microprocessor [[https://ewh.ieee.org/r5/denver/sscs/Presentations/2012_05_Sathe.pdf](https://ewh.ieee.org/r5/denver/sscs/Presentations/2012_05_Sathe.pdf)]

Pozar, David M. *Microwave Engineering*. 4th ed. Wiley, 2012. [[pdf](https://hajaress.wordpress.com/wp-content/uploads/2019/09/microwave_engineering_david_m_pozar_4ed_wiley_2012.pdf)]
