---
title: Filter Design
date: 2024-12-29 22:08:39
tags:
categories:
- dsp
mathjax: true
---



![image-20260428210651188](filters/image-20260428210651188.png)

![image-20260428203853085](filters/image-20260428203853085.png)

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy import signal

# Parameters: 4th order filter with 1kHz cutoff
order = 4
w_cutoff = 2 * np.pi * 1000
w = np.logspace(2, 5, 1000) # Frequency range from 100Hz to 100kHz

# Generate Butterworth coefficients and frequency response
b_but, a_but = signal.butter(order, w_cutoff, analog=True)
w_but, h_but = signal.freqs(b_but, a_but, worN=w)

# Generate Chebyshev (1dB ripple) response
b_cheb, a_cheb = signal.cheby1(order, 1, w_cutoff, analog=True)
w_cheb, h_cheb = signal.freqs(b_cheb, a_cheb, worN=w)

# Generate Bessel response
b_bess, a_bess = signal.bessel(order, w_cutoff, analog=True)
w_bess, h_bess = signal.freqs(b_bess, a_bess, worN=w)

freqs = w / (2 * np.pi)

t = np.linspace(0, 0.005, 1000) # 5ms window

# Calculate Step Responses
t_but, y_but = signal.step((b_but, a_but), T=t)
t_cheb, y_cheb = signal.step((b_cheb, a_cheb), T=t)
t_bess, y_bess = signal.step((b_bess, a_bess), T=t)
```



## Butterworth Filters

> Butterworth Filters [[https://people.eecs.ku.edu/~demarest/212/Butterworth%20Filters.pdf](https://people.eecs.ku.edu/~demarest/212/Butterworth%20Filters.pdf)]
>
> Stephen Roberts, Signal Processing & Filter Design B3 option: *Lecture 2 - Frequency Selective Filters* [[https://www.robots.ox.ac.uk/~sjrob/Teaching/SP/l2.pdf](https://www.robots.ox.ac.uk/~sjrob/Teaching/SP/l2.pdf)]

![image-20260507004930525](filters/image-20260507004930525.png)

![image-20260507233246993](filters/image-20260507233246993.png)

```matlab
% Parameters
wc = 100;               % Cutoff frequency in rad/s
orders = [1, 2, 6];     % Orders to compare
w = logspace(0, 3, 1000); % Frequency range (1 to 1000 rad/s)

for n = orders
    % 1. Design Analog Filter (the 's' flag is critical)
    [b, a] = butter(n, wc, 's');
    
    % 2. Calculate Complex Frequency Response
    h = freqs(b, a, w);
    
    % 3. Calculate Group Delay
    % For analog filters, we manually differentiate phase: gd = -d(phi)/dw
    phase = unwrap(angle(h));
    gd = -diff(phase) ./ diff(w);
    
    % --- Plot Magnitude (dB) ---
    subplot(3,1,1);
    semilogx(w, 20*log10(abs(h)), 'LineWidth', 2, 'DisplayName', ['n=' num2str(n)]);
    hold on;
    
    % --- Plot Phase (Degrees) ---
    subplot(3,1,2);
    semilogx(w, phase * 180/pi, 'LineWidth', 2);
    hold on;
    
    % --- Plot Group Delay ---
    subplot(3,1,3);
    semilogx(w(1:end-1), gd, 'LineWidth', 2);
    hold on;
end

% Formatting
subplot(3,1,1)
ylabel('Magnitude (dB)'); grid on; xline(wc, '--r', 'HandleVisibility','off'); legend('show');
ylim([-60 5]);

subplot(3,1,2); ylabel('Phase (deg)'); grid on; xline(wc, '--r', 'HandleVisibility','off');

subplot(3,1,3); ylabel('Group Delay (sec)'); xlabel('Frequency (rad/s)'); 
grid on; xline(wc, '--r', 'HandleVisibility','off');
```

## Bessel Filters

> Stephen Roberts, Signal Processing & Filter Design B3 option: *Lecture 3 - Transient Response and Transforms* [[https://www.robots.ox.ac.uk/~sjrob/Teaching/SP/l3.pdf](https://www.robots.ox.ac.uk/~sjrob/Teaching/SP/l3.pdf)]

**Bessel filter** is often called **Bessel–Thomson filter** or simply **Thomson filter**

![image-20260508000308350](filters/image-20260508000308350.png)

![image-20260508000240921](filters/image-20260508000240921.png)



---

`besself`: Bessel *analog* filter design `[b,a] = besself(n, Wo)`

> the transfer function coefficients of an $n$th-order lowpass analog Bessel filter, where `Wo` is the angular frequency up to which the filter's group delay is approximately constant. Larger values of `n` produce a group delay that better approximates a constant up to `Wo`.

`scipy.signal.bessel(N, Wn, btype='low', analog=True, output='ba', norm='phase')`

> `norm='phase'` — The filter is normalized such that the **phase response reaches its midpoint at angular (e.g. rad/s) frequency `Wn`**
>
> This is the default, and matches MATLAB's implementation.

```matlab
octave:8> [b,a] = besself(5,1)
b = 1
a =

   1.0000   3.8107   6.7767   6.8864   3.9363   1.0000
```

```python
b_bess, a_bess = signal.bessel(5, 1, btype='low', analog=True, norm='phase')
print(b_bess, a_bess)

# [1.] [1.         3.81070121 6.77667372 6.88636765 3.93628343 1.        ]

```

![bessel_5th_wn1](filters/bessel_5th_wn1.png)

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy import signal

order = 5
cutoff_rad = 1

b_bess, a_bess = signal.bessel(order, cutoff_rad, btype='low', analog=True, norm='phase')

# Frequency response computation (Linear scale)
w = np.linspace(0, 8 * cutoff_rad, 1000) # Frequency range 0 to 2*fc

# Frequency response for phase
w_bess, h_bess = signal.freqs(b_bess, a_bess, worN=w)

# Phase Response (unwrapped to avoid 360 degree jumps)
phase_bess = np.unwrap(np.angle(h_bess))

plt.figure(figsize=(10, 5))
plt.plot(w_bess, np.degrees(phase_bess), label='Bessel', linewidth=2, linestyle='-')
plt.axvline(cutoff_rad, color='red', linestyle=':', label='Cutoff')
plt.title('5th Order Bessel Filter Phase Response w/ Wn=1')
plt.ylabel('Phase [degrees]'); plt.xlabel('Frequency [rad/s]')
plt.grid(True); plt.legend()
```



## RC LPF

> Kwantae Kim, Integrated Analog Systems D - Lecture 02 (Continuous-Time Filters) [[https://youtu.be/B7-kr5zV3NA](https://youtu.be/B7-kr5zV3NA)]
>
> —, Integrated Analog Systems D - Lecture 03 (Continuous-Time Filters) [[https://youtu.be/6GdDiwaKDZw](https://youtu.be/6GdDiwaKDZw)]
>
> —, Integrated Analog Systems D - Lecture 05 (Continuous-Time Filters) [[https://youtu.be/LHhEK1RlC6w](https://youtu.be/LHhEK1RlC6w)]

![image-20260524100715080](filters/image-20260524100715080.png)

![image-20260524101628382](filters/image-20260524101628382.png)

![image-20260524101414457](filters/image-20260524101414457.png)

> [[Gist link](https://gist.github.com/raytroop/69a093a3569bc12226d91b5a2022bbe9)]



---

---

***2nd-Order RC LPF***

***Loading effect** & **limitation***

![image-20260524103229122](filters/image-20260524103229122.png)

![image-20260524104702612](filters/image-20260524104702612.png)

![image-20260524103715322](filters/image-20260524103715322.png)

![image-20260524103833060](filters/image-20260524103833060.png)

**Phase Magin with damping Factor $\zeta$**

![image-20260524103924774](filters/image-20260524103924774.png)
$$
\boxed{\phi_\text{PM}\approx 100\cdot \zeta}
$$


---

---

***General 2nd-Order RC LPF***

![image-20260524151528679](filters/image-20260524151528679.png)

![image-20260524151744133](filters/image-20260524151744133.png)

![image-20260524154744621](filters/image-20260524154744621.png)

***Laplace Transform***

![image-20260524152125499](filters/image-20260524152125499.png)

***Stability Analysis***

![image-20260524153121052](filters/image-20260524153121052.png)

![image-20260524152852821](filters/image-20260524152852821.png)

![image-20260524152838122](filters/image-20260524152838122.png)

![image-20260524153009904](filters/image-20260524153009904.png)



## Active Filters

> Kwantae Kim, Integrated Analog Systems D - Lecture 05 (Continuous-Time Filters) [[https://youtu.be/LHhEK1RlC6w](https://youtu.be/LHhEK1RlC6w)]

![image-20260524163246135](filters/image-20260524163246135.png)

![image-20260524173631125](filters/image-20260524173631125.png)

> [[Gist link](https://gist.github.com/raytroop/022b6cf1eb71dcb4667dc0bff110b413)]
>
> ![image-20260524160443441](filters/image-20260524160443441.png)

![image-20260524174730147](filters/image-20260524174730147.png)



*TODO* &#128197;



## Single-Pole LPF Algorithms

> Neil Robertson, Model a Sigma-Delta DAC Plus RC Filter [[https://www.dsprelated.com/showarticle/1642.php](https://www.dsprelated.com/showarticle/1642.php)]
>
> Jason Sachs, Ten Little Algorithms, Part 2: The Single-Pole Low-Pass Filter [[https://www.embeddedrelated.com/showarticle/779.php](https://www.embeddedrelated.com/showarticle/779.php)]
>
> —. Return of the Delta-Sigma Modulators, Part 1: Modulation [[https://www.dsprelated.com/showarticle/1517/return-of-the-delta-sigma-modulators-part-1-modulation](https://www.dsprelated.com/showarticle/1517/return-of-the-delta-sigma-modulators-part-1-modulation)]

- ***Derivatives Approximation*** ($H_p(s)=\frac{1}{s\tau +1}$)

  $$\begin{align}
  H_p(z)&=\frac{\frac{T_s}{T_s+\tau}}{1+(\frac{T_s}{T_s+\tau}-1)z^{-1}}\tag{EQ-0}\\
  H_p(z)&=\frac{\frac{T_s}{\tau}}{1+(\frac{T_s}{\tau}-1)z^{-1}}\tag{EQ-1}
  \end{align}$$

- ***Matched z-Transform (Root Matching)***
  $$
  H_p(z)=\frac{1-e^{-T_s/\tau}}{1-e^{-T_s/\tau}z^{-1}}\tag{EQ-2}
  $$
  EQ-2 is connected with EQ-1 by $1 - e^{-\Delta t/\tau} \approx \frac{\Delta t}{\tau}$

![image-20250907163030510](filters/image-20250907163030510.png)

```python  
import numpy as np
import matplotlib.pyplot as plt
import scipy.signal


dt=0.002; tau=0.05

T=1
t = np.arange(0,T+1e-5,dt)
x = 1-np.abs(4*t-1)
x[4*t>2] = 0.95; x[t>0.75] = 0.02

alpha_derv = dt / (dt + tau)
alpha_derv_approx = dt / tau

yfilt_derv = scipy.signal.lfilter([alpha_derv], [1, alpha_derv - 1], x)
yfilt_derv_approx = scipy.signal.lfilter([alpha_derv_approx], [1, alpha_derv_approx - 1], x)

a1 = -np.exp(-dt/tau)
b0 = [1 + a1]
a = [1, a1]
y_filt_match = scipy.signal.lfilter(b0, a, x)

plt.figure(figsize=(20,10))
plt.plot(t, x, color='k', linewidth=3, label='x')
plt.plot(t, yfilt_derv, color='red', linewidth=3, label=r'$H_p(z)=\frac{\frac{T_s}{T_s+\tau}}{1+(\frac{T_s}{T_s+\tau}-1)z^{-1}}$')
plt.plot(t, yfilt_derv_approx, color='green', marker='D', linestyle='dashed',markersize=4, linewidth=3, label=r'$H_p(z)=\frac{\frac{T_s}{\tau}}{1+(\frac{T_s}{\tau}-1)z^{-1}}$')
plt.plot(t, y_filt_match, color='m', marker='x', linestyle='dashed',markersize=4, linewidth=3, label=r'$H_p(z)=\frac{1-e^{-T_s/\tau}}{1-e^{-T_s/\tau}z^{-1}}$')

plt.legend(loc='upper right', fontsize=20)
plt.grid(which='both');plt.xlabel('Time (s)');plt.show()
```





---



```
    x(t) ──┬── R ──┬── y(t)
           │       │
           │       C
           │       │
           └───────┴── gnd
```

Three discretizations of the same continuous prototype, all valid first-order LPFs but with different sample-domain behavior $\alpha = \frac{T}{T+\tau}$:

| Form | Difference equation | Transfer function | Notes |
|---|---|---|---|
| **Backward Euler** (above) | $y_n = (1-\alpha) y_{n-1} + \alpha\, x_n$ | $\dfrac{\alpha}{1 - (1-\alpha) z^{-1}}$ | Implicit; needs $x_n$ before computing $y_n$ |
| **Delayed leaky integrator** | $y_n = (1-\alpha) y_{n-1} + \alpha\, x_{n-1}$ | $\dfrac{\alpha z^{-1}}{1 - (1-\alpha) z^{-1}}$ | One extra sample of delay; same magnitude response |
| **Bilinear (Tustin)** | $y_n = (1-\alpha)y_{n-1} + \tfrac{\alpha}{2}(x_n + x_{n-1})$ | $\dfrac{(\alpha/2)(1 + z^{-1})}{1 - (1-\alpha) z^{-1}}$ | Adds zero at $z = -1$; better frequency-response match |
| **Forward Euler** | $y_n = (1 - T/\tau)y_{n-1} + (T/\tau)\,x_{n-1}$ | $\dfrac{(T/\tau) z^{-1}}{1 - (1 - T/\tau) z^{-1}}$ | Unstable when $T > 2\tau$ |

Pole magnitude $|1-\alpha| < 1$ always — **backward Euler is unconditionally stable**, unlike forward Euler ($\alpha = T/\tau$), which goes unstable when $T > 2\tau$

All four collapse to the same continuous-time filter as $T \to 0$, but they're not interchangeable at finite $T$ — the delayed leaky integrator in particular adds one sample of group delay that the others don't.



## Discrete-Time Integrators

> Qasim Chaudhari. Discrete-Time Integrators [[https://wirelesspi.com/discrete-time-integrators/](https://wirelesspi.com/discrete-time-integrators/)]
>
> David Johns (University of Toronto) "Oversampled Data Converters" Course (2019) [[https://youtu.be/qIJ2LORYmyA](https://youtu.be/qIJ2LORYmyA)]

Delaying Integrator

Delay-free Integrator

![image-20250615124417691](filters/image-20250615124417691.png)

## Discrete-Time Differentiator

> Qasim Chaudhari. Design of a Discrete-Time Differentiator [[https://wirelesspi.com/design-of-a-discrete-time-differentiator/](https://wirelesspi.com/design-of-a-discrete-time-differentiator/)]

*TODO* &#128197;



## reference

Boris Murmann. EE315A VLSI Signal Conditioning Circuits

Bill Redman-White, ISSCC 2009 Tutorial: *T1 : Continuous-Time Filters*

Stephen Roberts, Signal Processing & Filter Design B3 option [[https://www.robots.ox.ac.uk/~sjrob/Teaching/sp_course.html](https://www.robots.ox.ac.uk/~sjrob/Teaching/sp_course.html)]

Butterworth, Chebyshev & Bessel filters [[https://analogcircuitdesign.com/butterworth-and-chebyshev-filters/](https://analogcircuitdesign.com/butterworth-and-chebyshev-filters/)]

Qasim Chaudhari. FIR vs IIR Filters – A Practical Comparison [[https://wirelesspi.com/fir-vs-iir-filters-a-practical-comparison/](https://wirelesspi.com/fir-vs-iir-filters-a-practical-comparison/)]

—. Finite Impulse Response (FIR) Filters [[https://wirelesspi.com/finite-impulse-response-fir-filters/](https://wirelesspi.com/finite-impulse-response-fir-filters/)]

—. Why FIR Filters have Linear Phase [[https://wirelesspi.com/why-fir-filters-have-linear-phase/](https://wirelesspi.com/why-fir-filters-have-linear-phase/)]

—. Moving Average Filter [[https://wirelesspi.com/moving-average-filter/](https://wirelesspi.com/moving-average-filter/)]

—. Cascaded Integrator Comb (CIC) Filters – A Staircase of DSP. [[https://wirelesspi.com/cascaded-integrator-comb-cic-filters-a-staircase-of-dsp/](https://wirelesspi.com/cascaded-integrator-comb-cic-filters-a-staircase-of-dsp/)]

Hideo Okawara's Mixed Signal Lecture Series [[https://tomverbeure.github.io/2024/01/06/Hideo-Okawara-Mixed-Signal-Lecture-Series.html](https://tomverbeure.github.io/2024/01/06/Hideo-Okawara-Mixed-Signal-Lecture-Series.html)]

How to generate complex poles without inductor? [[https://a2d2ic.wordpress.com/2020/02/19/basics-on-active-rc-low-pass-filters/](https://a2d2ic.wordpress.com/2020/02/19/basics-on-active-rc-low-pass-filters/)]
