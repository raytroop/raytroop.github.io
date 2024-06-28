---
title: Signal and System insight
date: 2024-05-02 23:04:55
tags:
categories:
- dsp
mathjax: true
---



## NRZ Bandwidth

![image-20240607221359970](ss-insight/image-20240607221359970.png)

> Maxim Integrated,NRZ Bandwidth - HF Cutoff vs. SNR [[https://pdfserv.maximintegrated.com/en/an/AN870.pdf](https://pdfserv.maximintegrated.com/en/an/AN870.pdf)]



## $0.35/T_r$

![image-20240607222440796](ss-insight/image-20240607222440796.png)



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

Then the equaion for the error is simply
$$
E(s) = \frac{1}{1+T(s)}R(s)
$$


Apllication of the *Final Value Theorem* to the error formula gives the result

$$\begin{align}
\lim _{t\to \infty} e(t) &= e_{ss} = \lim _{s\to 0} sE(s) \\
&= \lim _{s\to 0} s\frac{1}{1+\frac{K_n(s)}{s^n}}\frac{1}{s^{k+1}} \\
&= \lim _{s\to 0} \frac{s^n}{s^n + K_n(0)}\frac{1}{s^k}
\end{align}$$

- if $n > k$, $e=0$
- if $n < k$, $e\to \infty$
- if $n=k$
  - $e_{ss} = \frac{1}{1+K_0}$ if $n=k=0$
  - $e_{ss} = \frac{1}{K_n}$ if $n=k \neq 0$


## PID

*TODO* &#128197;

- a Proportional term to close the feedback loop
- an Integral term to assure zero error to constant reference and disturbance inputs
- a Derivative term to improve (or realize!) stability and good dynamic response



## Nyquist Criterion

*TODO* &#128197;



## group delay

*TODO* &#128197;



## Conversion Between the $s$- and $z$-Domains

![image-20240429220303281](ss-insight/image-20240429220303281.png)

![image-20240429215455332](ss-insight/image-20240429215455332.png)

> Staszewski, Robert Bogdan, and Poras T. Balsara. All-digital frequency synthesizer in deep-submicron CMOS. John Wiley & Sons, 2006.


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

## Initial Value Theorem & Final Value Theorem

Two valuable *Laplace transform* theorem

- Initial Value Theorem, which states that it is always possible to determine the **initial value** of the time function $f(t)$ from its Laplace transform
  $$
  \lim _{s\to \infty}sF(s) = f(0^+)
  $$

- Final Value Theorem allows us to compute the **constant steady-state value** of a time function given its Laplace transform
  $$
  \lim _{s\to 0}sF(s) = f(\infty)
  $$

  > If $f(t)$ is step response, then $f(0^+) = H(\infty)$ and $f(\infty) = H(0)$, where $H(s)$ is transfer function





## Butterworth filter

> function varargout = butter(n, Wn, varargin)
>
> %   BUTTER Butterworth digital and analog filter design.
>
> %   [B,A] = BUTTER(N,Wn) designs an Nth order lowpass digital
>
> %   Butterworth filter and returns the filter coefficients in length
>
> %   N+1 vectors B (numerator) and A (denominator). The coefficients
>
> %   are listed in descending powers of z. The cutoff frequency
>
> %   Wn must be **0.0 < Wn < 1.0**, with 1.0 corresponding to
>
> %   half the sample rate.

$$
w_n = \frac{f_c}{0.5f_s}
$$

where $f_c$ is cutoff frequency, $f_s$ is sampling frequency


$$
\Phi = \omega T_s \text { ,}\Phi \in [0,2\pi]
$$

Find the relationship between $\omega_n$ and \Phi

$$\begin{align}
\Phi &= 2\pi f_c \frac{1}{f_s}  \\
&=\pi \frac{f_c}{0.5f_s} \\
&= \pi \omega _n
\end{align}$$



Given $f_c$ is 300 Hz and $f_s$ is 1000 Hz, we get
$$
\omega_n = \frac{f_c}{0.5*f_s} = 0.6
$$
and in `rad/sample` unit, cutoff frequency is 
$$
\Phi = \pi * \omega_n = 0.6 \pi \text {, unit: rad/sample}
$$

### Z-transform

$$
z= e^{-j\Phi}
$$

```matlab
fc = 300;
fs = 1000;

[b,a] = butter(6,fc/(fs/2));
fprintf('The numerator b is:\n ');
fprintf('%g ', b);
fprintf('\n');
fprintf('The denominator a is:\n ');
fprintf('%g ', a);
fprintf('\n');

figure(1)
freqz(b, a);
ylim([-400, 100])
```

> The numerator (`b`) and denominator (`a`) depend on the cutoff frequency and the order; the cutoff frequency is denominated with $\omega_n$ . Just multiply the $\pi$, we get the Z-transform $\Phi$ rad/sample, which is the plot of `freqz(b, a)`

![image-20220407100948965](ss-insight/image-20220407100948965.png)



### Transfer function with sample information

$$
z = e^{-j\omega T_s}
$$

![image-20220407103451265](ss-insight/image-20220407103451265.png)

```verilog
figure(2)
ylim([-400, 100])
[h,f] = freqz(b,a,[],fs);
hdb20 = 20*log10(abs(h));
subplot(3,1,1)
plot(f, hdb20, 'b')
ylim([-400, 100])
title('DTFT with freqz and sample rate')
xlabel('Frequency (Hz)')
ylabel('Mag (dB)')
grid on;

subplot(3,1,2)
sys = tf(b, a, 1/fs);
[mag, phs, wout] = bode(sys);
wout = wout(:);
whz = wout/2/pi;
hdb = 20*log10(mag(:));
plot(whz, hdb, 'r-o');
ylim([-400, 100])
title('DTFT with bode and sample period')
xlabel('Frequency (Hz)')
ylabel('Mag (dB)')
grid on;


subplot(3,1,3)
plot(f, hdb20,'b', whz, hdb, 'ro');
legend('freqz', 'bode')
ylim([-400, 100])
title('overlay and comparision')
xlabel('Frequency (Hz)')
ylabel('Mag (dB)')
grid on;

```

### Time Domain from Frequency Domain

Assume input is **sampled by** $f_s$

```verilog
figure(3)
% assume x is sampled by fs
x = rand(1, 50);
y = filter(b, a, x);
xt = (1:50);
plot(xt, x, '-s', xt, y, '-o')
legend('input', 'output')
xlabel('Sample')
ylabel('mag')
title('filter in Time domain')
grid on;
```

![image-20220407113330972](ss-insight/image-20220407113330972.png)



## Bilinear Transformation

**Bilinear Transformation**, also known as **Bilinear Approximation**,  an algebraic transformation between the variables $s$ and $z$ that maps the entire $j\Omega$-axis in the $s$-plane to *one revolution of the unit circle* in the $z$-plane. 

That is, with this approach, $-\infty \le \Omega \le +\infty$ maps onto $-\pi \le \omega \le +\pi$, the transformation between the continuous-time and discrete-time frequency variables is necessarily **nonlinear**.

With $H_c(s)$ denoting the continuous-time system function and $H(z)$ the discrete-time system function, the bilinear transformation corresponds to replacing $s$ by
$$
s=\frac{2}{T_d}\left( \frac{1-z^{-1}}{1+z^{-1}} \right)
$$


that is,
$$
H(z) = H_c\left( \frac{2}{T_d}\left( \frac{1-z^{-1}}{1+z^{-1}} \right) \right)
$$





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
