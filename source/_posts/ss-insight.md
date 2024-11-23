---
title: Signal and System insight
date: 2024-05-02 23:04:55
tags:
categories:
- dsp
mathjax: true
---





## dBc

*TODO* &#128197;





## dBFS

*TODO* &#128197;



## Nyquist rate & Nyquist frequency

- **Nyquist rate**

  The Nyquist rate is the **minimum sample rate** required to accurately measure a signal's highest frequency. It's equal to ***twice*** the highest frequency of the signal

- **Nyquist frequency**

  The Nyquist frequency is the highest frequency that can be **represented without aliasing** in a discrete signal. It's equal to ***half*** the sampling frequency

![https://upload.wikimedia.org/wikipedia/commons/d/d8/Nyquist_frequency_%26_rate.svg](ss-insight/Nyquist_frequency_&_rate.svg)

> **Oversampling Ratio (OSR)** is defined as the ratio of the *Nyquist frequency* $f_s/2$ to the *signal bandwidth* $B$ given by $\text{OSR}=f_s/2B$

## Summation & Integration 

|             | impulse response | Transform            | ROC                       |
| ----------- | ---------------- | -------------------- | ------------------------- |
| Summation   | $u(t)$           | $\frac{1}{s}$        | $\mathfrak{Re}\{s\}\gt 0$ |
| Integration | $u[n]$           | $\frac{1}{1-z^{-1}}$ | $|z| \gt 1$               |

> both are **NOT** stable



## sinc filter

![image-20241002143413907](ss-insight/image-20241002143413907.png)

where $W$ is sampling frequency in Hz

![sinc.drawio](ss-insight/sinc.drawio.svg)



> ![image-20241002143219224](ss-insight/image-20241002143219224.png)




## Zero-order hold (ZOH)

![image-20240928101832121](ss-insight/image-20240928101832121.png)
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


> ![image-20240928103227690](ss-insight/image-20240928103227690.png)



## frequency convention

- radian frequency $\omega_0$ in **rad/s**
- cyclic frequency $f_0$ in **Hz**




##  Energy signals vs Power signal

> Topic 5 Energy & Power Signals, Correlation & Spectral Density [[https://www.robots.ox.ac.uk/~dwm/Courses/2TF_2021/N5.pdf](https://www.robots.ox.ac.uk/~dwm/Courses/2TF_2021/N5.pdf)]

---

![image-20240427155046131](ss-insight/image-20240427155046131.png)

> ![image-20240719203550628](ss-insight/image-20240719203550628.png)

---

---

![image-20240427155100927](ss-insight/image-20240427155100927.png)

> ![image-20240719204148098](ss-insight/image-20240719204148098.png)





## modulation & demodulation

![image-20240826221237312](ss-insight/image-20240826221237312.png)

![image-20240826221251379](ss-insight/image-20240826221251379.png)



> Hossein Hashemi, RF Circuits, [[https://youtu.be/0f3yZMvD2Jg?si=2c1Q4y6WJq8Jj8oN](https://youtu.be/0f3yZMvD2Jg?si=2c1Q4y6WJq8Jj8oN)]



## Coherent Sampling

To avoid **spectral leakage** completely, the method of **coherent sampling** is recommended. Coherent sampling requires that the input- and clock-frequency generators are **phase locked**, and that the input frequency be chosen based on the following relationship:
$$
\frac{f_{\text{in}}}{f_{\text{s}}}=\frac{M_C}{N_R}
$$

where:

- $f_{\text{in}}$ = the desired input frequency
- $f_s$ = the clock frequency of the data converter under test
- $M_C$ = the number of cycles in the data window (to make all samples unique, choose odd or prime numbers)
- $N_R$ = the data record length (for an 8192-point FFT, the data record is 8192s long)



$$\begin{align}
f_{\text{in}} &=\frac{f_s}{N_R}\cdot M_C \\
&= f_{\text{res}}\cdot M_C
\end{align}$$

---

**irreducible ratio**

An **irreducible ratio** ensures identical code sequences not to be repeated multiple times. Unnecessary repetition of the same code is not desirable as it increases ADC test time.

> Given that $\frac{M_C}{N_R}$ is irreducible, and $N_R$ is a power of 2, an **odd number** for $M_C$ will always produce an **irreducible ratio**



Assuming there is a common factor $k$ between $M_C$ and $N_R$, i.e. $\frac{M_C}{N_R}=\frac{k M_C'}{k N_R'}$

The samples  ($n\in[1, N_R]$)

$$\begin{align}
y[n] &= \sin\left( \omega_{\text{in}} \cdot t_n \right) \\
&= \sin\left( \omega_{\text{in}} \cdot n\frac{1}{f_s} \right)  \\
& = \sin\left( \omega_{\text{in}} \cdot n\frac{1}{f_{\text{in}}}\frac{M_C}{N_R} \right) \\
& = \sin\left( 2\pi n\frac{M_C}{N_R} \right)
\end{align}$$

Then

$$\begin{align}
y[n+N_R'] &= \sin\left( 2\pi (n+N_R')\frac{M_C}{N_R} \right) \\
& = \sin\left( 2\pi n \frac{M_C}{N_R} + 2\pi N_R'\frac{M_C}{N_R}\right) \\
& = \sin\left( 2\pi n \frac{M_C}{N_R} + 2\pi N_R'\frac{kM_C'}{kN_R'} \right) \\
& = \sin\left( 2\pi n \frac{M_C}{N_R} + 2\pi M_C' \right) \\
& = \sin\left( 2\pi n \frac{M_C}{N_R}\right) 
\end{align}$$



So,  the samples is repeated $y[n] = y[n+N_R']$.  Usually, no additional information is gained by repeating with the same sampling points.

---

**Example**
$$
N \cdot \frac{1}{F_s} = M \cdot \frac{1}{F_{in}}
$$

where $F_s$ is sample frequency, $F_{in}$ input signal frequency. 

And $N$ often is 256, 512; M is 3, 5, 7, 11.





## channel loss

- skin effect loss
- dielectric loss

![image-20240810102618245](ss-insight/image-20240810102618245.png)



## phase delay & group delay

![image-20240810094519487](ss-insight/image-20240810094519487.png)



- Phase delay directly measures the device or system time delay of *individual sinusoidal frequency components* in the **steady-state conditions**.
- In the ideal case the envelope delay is equal to the phase delay
- envelope delay is a more sensitive measure of aberrations than phase delay


### phase delay

![image-20240808212730768](ss-insight/image-20240808212730768.png)


> If the phase delay peaks (exceeds the low-frequency value) you can expect to see high-frequency
> components late in the step response. This causes ***ringing***. 



### group delay

![image-20240808213806803](ss-insight/image-20240808213806803.png)





![image-20240808220657443](ss-insight/image-20240808220657443.png)

![image-20240808220740349](ss-insight/image-20240808220740349.png)



---

steady-state at this frequency is a polarity flip; a 180 degrees phase shift; which is a transfer function of H(s)=-1. 
$$
H(s) = e^{j\pi}
$$
That is $\phi(\omega) = \pi$
$$
\tau_p = \frac{\pi}{\omega}
$$
and
$$
\tau_g = \frac{\partial \pi}{\partial \omega}=0
$$




---


> Hollister, Allen L. *Wideband Amplifier Design*. Raleigh, NC: SciTech Pub., 2007.
>
> Pupalaikis, Peter. (2006). Group Delay and its Impact on Serial Data Transmission and Testing.  [[https://cdn.teledynelecroy.com/files/whitepapers/group_delay-designcon2006.pdf](https://cdn.teledynelecroy.com/files/whitepapers/group_delay-designcon2006.pdf)]
>
> [Pupalaikis et al., “Eye Patterns in Scopes”, DesignCon, Santa Clara CA, 2005[https://cdn.teledynelecroy.com/files/whitepapers/eye_patterns_in_scopes-designcon_2005.pdf](https://cdn.teledynelecroy.com/files/whitepapers/eye_patterns_in_scopes-designcon_2005.pdf)]
>
> Starič, P. & Margan, E.. (2006). Wideband Amplifiers. 10.1007/978-0-387-28341-8. 
>
> Alan V. Oppenheim, Alan S. Willsky, and S. Hamid Nawab. 1996. Signals & systems (2nd ed.). Prentice-Hall, Inc., USA.
>
> Phase delay vs group delay: Common misconceptions. [[https://audiosciencereview.com/forum/index.php?threads/phase-delay-vs-group-delay-common-misconceptions.39591/](https://audiosciencereview.com/forum/index.php?threads/phase-delay-vs-group-delay-common-misconceptions.39591/)]





## Feedback Rearrange

![loop-refactor.drawio](ss-insight/loop-refactor.drawio.svg)

The closed loop transfer function of $Y/X$ and $Y_1/X_1$ are almost same, except sign

$$\begin{align}
\frac{Y}{X} &= +\frac{H_1(s)H_2(s)}{1+H_1(s)H_2(s)} \\
\frac{Y_1}{X_1} &= -\frac{H_1(s)H_2(s)}{1+H_1(s)H_2(s)}
\end{align}$$

![loop-refactor-partion.drawio](ss-insight/loop-refactor-partion.drawio.svg)

define $-Y_1=Y_n$, then
$$
\frac{Y_n}{X_1} = \frac{H_1(s)H_2(s)}{1+H_1(s)H_2(s)}
$$
![loop-refactor-partion-general.drawio](ss-insight/loop-refactor-partion-general.drawio.svg)

> ![image-20240805231921946](ss-insight/image-20240805231921946.png)
>
> Saurabh Saxena, IIT Madras. CICC2022 Clocking for Serial Links - Frequency and Jitter Requirements, Phase-Locked Loops, Clock and Data Recovery





## Convolution of probability distributions

The probability distribution of the *sum of two or more **independent** random variables* is the **convolution** of their individual distributions.

![image-20240804104528903](ss-insight/image-20240804104528903.png)





## Thermal noise

Thermal noise in an ideal resistor is approximately **white**, meaning that its power spectral density is nearly **constant** throughout the frequency spectrum.

When limited to a *finite bandwidth* and viewed in the time domain, thermal noise has a nearly **Gaussian amplitude distribution**



> ![image-20240804102454281](ss-insight/image-20240804102454281.png)



## Barkhausen criteria

Barkhausen criteria are *necessary* but **not sufficient conditions** for sustainable **oscillations**

![image-20240720090654883](ss-insight/image-20240720090654883.png)

it simply *"latches up"* rather than oscillates



## NRZ Bandwidth

![image-20240607221359970](ss-insight/image-20240607221359970.png)

> Maxim Integrated,NRZ Bandwidth - HF Cutoff vs. SNR [[https://pdfserv.maximintegrated.com/en/an/AN870.pdf](https://pdfserv.maximintegrated.com/en/an/AN870.pdf)]



## $0.35/T_r$

![image-20240607222440796](ss-insight/image-20240607222440796.png)



## $0.5/T_r$

*TODO* &#128197;



## System Type

> Control of Steady-State Error to Polynomial Inputs: System Type

![image-20240502232125317](ss-insight/image-20240502232125317.png)

control systems are assigned a **type** number according to the maximum degree of the 
input polynominal for which the steady-state error is a *finite constant*. i.e.

> - Type 0: Finite error to a step (position error) 
> - Type 1: Finite error to a ramp (velocity error)
> - Type 2: Finite error to a parabola (acceleration error)

The open-loop transfer function can be expressed as
$$
T(s) = \frac{K_n(s)}{s^n}
$$

where we collect all the terms except the pole ($s$) at eh origin into $K_n(s)$, 

The polynomial inputs, $r(t)=\frac{t^k}{k!} u(t)$, whose transform is
$$
R(s) = \frac{1}{s^{k+1}}
$$

Then the equation for the error is simply
$$
E(s) = \frac{1}{1+T(s)}R(s)
$$


Application of the *Final Value Theorem* to the error formula gives the result

$$\begin{align}
\lim _{t\to \infty} e(t) &= e_{ss} = \lim _{s\to 0} sE(s) \\
&= \lim _{s\to 0} s\frac{1}{1+\frac{K_n(s)}{s^n}}\frac{1}{s^{k+1}} \\
&= \lim _{s\to 0} \frac{s^n}{s^n + K_n}\frac{1}{s^k}
\end{align}$$

- if $n > k$, $e=0$
- if $n < k$, $e\to \infty$
- if $n=k$
  - $e_{ss} = \frac{1}{1+K_n}$ if $n=k=0$
  - $e_{ss} = \frac{1}{K_n}$ if $n=k \neq 0$​

where we define $K_n(0) = K_n$



## Nyquist's Stability Criterion

*TODO* &#128197;





[[Michael H. Perrott, High Speed Communication Circuits and Systems, Lecture 15 Integer-N Frequency Synthesizers](https://www.cppsim.com/CommCircuitLectures/lec15.pdf)]






## Spectral content of NRZ

![image-20231111100420675](ss-insight/image-20231111100420675.png)

![image-20231111101322771](ss-insight/image-20231111101322771.png)

![image-20231110224237933](ss-insight/image-20231110224237933.png)



> Lecture 26 Autocorrelation Functions of Random Binary Processes [[https://bpb-us-w2.wpmucdn.com/sites.gatech.edu/dist/a/578/files/2003/12/ECE3075A-26.pdf](https://bpb-us-w2.wpmucdn.com/sites.gatech.edu/dist/a/578/files/2003/12/ECE3075A-26.pdf)]
>
> Lecture 32 Correlation Functions & Power Density Spectrum, Cross-spectral Density [[https://bpb-us-w2.wpmucdn.com/sites.gatech.edu/dist/a/578/files/2003/12/ECE3075A-32.pdf](https://bpb-us-w2.wpmucdn.com/sites.gatech.edu/dist/a/578/files/2003/12/ECE3075A-32.pdf)]



## sinusoidal steady-state and frequency response

![image-20231104104933781](ss-insight/image-20231104104933781.png)

![image-20231104104946203](ss-insight/image-20231104104946203.png)

![image-20231104105056345](ss-insight/image-20231104105056345.png)

![image-20231104105139814](ss-insight/image-20231104105139814.png)

![image-20231104105223549](ss-insight/image-20231104105223549.png)

Due to KCL and $u(t)=e^{j\omega t}$ and $y(t)=H(j\omega)e^{j\omega t}$, we have ODE:

$$\begin{align}
\frac{u(t) - y(t)}{R} = C \frac{dy(t)}{dt} \\
e^{j\omega t} - H(j\omega) e^{j\omega t} = H(j\omega)\cdot j\omega e^{j\omega t} \\
\end{align}$$

$H(j\omega)$ is obtained as below
$$
H(j\omega) = \frac{1}{1+j\omega}
$$



![image-20231104135855739](ss-insight/image-20231104135855739.png)



## Different Variants of the PSD Definition

In the practice of engineering, it has become customary to use slightly different variants of the PSD definition, depending on the particular application or research field. 

- **Two-Sided PSD**, $S_x(f)$

  this is a synonym of the PSD defined as the Fourier Transform of the **autocorrelation**.

- **One-Sided PSD**, $S'_x(f)$

   this is a variant derived from the *two-sided PSD* by considering only the *positive frequency* semi-axis.

  To **conserve the total power**, the value of the one-sided PSD is **twice** that of the two-sided PSD
  $$
  S'_x(f) = \left\{ \begin{array}{cl}
  0 & : \ f \geq 0 \\
  S_x(f) & : \ f = 0 \\
  2S_x(f) & : \ f \gt 0 
  \end{array} \right.
  $$
  



![image-20230603185546658](ss-insight/image-20230603185546658.png)  



> Note that the one-sided PSD definition makes sense only if the two-sided is an even function of $f$



If $S'_x(f)$ is even symmetrical around a positive frequency $f_0$, then two additional definitions can be adopted:

- **Single-Sideband PSD**, $S_{SSB,x}(f)$

  This is obtained from $S'_x(f)$ by moving the origin of the frequency axis to $f_0$
  $$
  S_{SSB,x}(f) =S'_x(f+f_0)
  $$
  This concept is particularly useful for describing phase or amplitude modulation schemes in wireless communications, where $f_0$ is the carrier frequency. 

  > Note that there is no difference in the values of the one-sided versus the SSB PSD; it is just a pure translation on the frequency axis. 

- **Double-Sideband PSD**, $S_{DSB,x}(f)$

  this is a variant of the SSB PSD obtained by considering only the positive frequency semi-axis.

  As in the case of the one-sided PSD, to conserve total power, the value of the DSB PSD is twice that of the SSB
  $$
  S_{DSB,x}(f) = \left\{ \begin{array}{cl}
  0 & : \ f \geq 0 \\
  S_{SSB,x}(f) & : \ f = 0 \\
  2S_{SSB,x}(f) & : \ f \gt 0 
  \end{array} \right.
  $$
  

![image-20230603222054506](ss-insight/image-20230603222054506.png)



> Note that the DSB definition makes sense only if the SSB PSD is even symmetrical around zero



## Poles and Zeros of transfer function

### poles

$$
H(s) = \frac{1}{1+s/\omega_0}
$$

magnitude and phase at $\omega_0$ and $-\omega_0$
$$\begin{align}
H(j\omega_0) &=  \frac{1}{1+j} = \frac{1}{\sqrt{2}}e^{-j\pi/4} \\
H(-j\omega_0) &=  \frac{1}{1-j} = \frac{1}{\sqrt{2}}e^{j\pi/4}
\end{align}$$

system response $y(t)$ of input $\cos(\omega_0 t)$, note $\cos(\omega_0t) = \frac{1}{2}(e^{j\omega_0 t} + e^{-j\omega_0 t})$
$$\begin{align}
y(t) &= H(j\omega_0)\cdot \frac{1}{2}e^{j\omega_0 t} + H(-j\omega_0)\cdot \frac{1}{2}e^{-j\omega_0 t} \\
&=  \frac{1}{\sqrt{2}}\cos(\omega_0t-\pi/4)
\end{align}$$

> $\cos(\omega_0 t)$, with frequency same with *pole* **DON'T** have *infinite response*
>
> That is,  pole indicate decrease trending 



### zeros

> similar with poles, $\cos(\omega_0 t)$, with frequency same with *zero* **DON'T** have *zero response*

$$
H(s) = 1+s/\omega_0
$$

magnitude and phase at $\omega_0$ and $-\omega_0$
$$\begin{align}
H(j\omega_0) &= 1+j = \sqrt{2}e^{j\pi/4} \\
H(-j\omega_0) &= 1-j = \sqrt{2}e^{-j\pi/4}
\end{align}$$

system response $y(t)$ of input $\cos(\omega_0 t)$, note $\cos(\omega_0t) = \frac{1}{2}(e^{j\omega_0 t} + e^{-j\omega_0 t})$
$$\begin{align}
y(t) &= H(j\omega_0)\cdot \frac{1}{2}e^{j\omega_0 t} + H(-j\omega_0)\cdot \frac{1}{2}e^{-j\omega_0 t} \\
&=  \sqrt{2}\cos(\omega_0t+\pi/4)
\end{align}$$


## baud rate

**symbol rate**, **modulation rate** or **baud rate** is the number of symbol changes per unit of time.

- Bit rate refers to the number of **bits** transmitted between two devices per unit of time
- The baud or symbol rate refers to the number of **symbols** that can be sent in the same amount of time



## reference

Stephen P. Boyd. EE102 Lecture 10 Sinusoidal steady-state and frequency response [[https://web.stanford.edu/~boyd/ee102/freq.pdf](https://web.stanford.edu/~boyd/ee102/freq.pdf)]

*Gene F. Franklin, J. David Powell, and Abbas Emami-Naeini. 2018. Feedback Control of Dynamic Systems (8th Edition) (8th. ed.). Pearson.*

Inter-Symbol Interference (or Leaky Bits) [[http://blog.teledynelecroy.com/2018/06/inter-symbol-interference-or-leaky-bits.html](http://blog.teledynelecroy.com/2018/06/inter-symbol-interference-or-leaky-bits.html)]

[AN001] Designing from zero an IIR filter in Verilog using biquad structure and bilinear discretization. URL:[[https://www.controlpaths.com/articles/an001_designing_iir_biquad_filter_bilinear/](https://www.controlpaths.com/articles/an001_designing_iir_biquad_filter_bilinear/)]

Frequency warping using the bilinear transform. URL:[[https://www.controlpaths.com/2022/05/09/frequency-warping-using-the-bilinear-transform/](https://www.controlpaths.com/2022/05/09/frequency-warping-using-the-bilinear-transform/)]

Digital control loops. Theoretical approach. URL:[[https://www.controlpaths.com/2022/02/28/digital-control-loops-theoretical-approach/](https://www.controlpaths.com/2022/02/28/digital-control-loops-theoretical-approach/)]

Simulation of DSP algorithms in Verilog. URL:[[https://www.controlpaths.com/2023/05/20/simulation-of-dsp-algorithms-in-verilog/](https://www.controlpaths.com/2023/05/20/simulation-of-dsp-algorithms-in-verilog/)]

Implementing a digital biquad filter in Verilog. URL:[[https://www.controlpaths.com/2021/04/19/implementing-a-digital-biquad-filter-in-verilog/](https://www.controlpaths.com/2021/04/19/implementing-a-digital-biquad-filter-in-verilog/)]

Implementing a FIR filter using folding. URL:[[https://www.controlpaths.com/2021/05/17/implementing-a-fir-filter-using-folding/](https://www.controlpaths.com/2021/05/17/implementing-a-fir-filter-using-folding/)]

Oppenheim, Alan V. and Cram. “Discrete-time signal processing : Alan V. Oppenheim, 3rd edition.” (2011).

Extras: PID Compensator with Bilinear Approximation URL:[[https://ctms.engin.umich.edu/CTMS/index.php?aux=Extras_PIDbilin](https://ctms.engin.umich.edu/CTMS/index.php?aux=Extras_PIDbilin)]

