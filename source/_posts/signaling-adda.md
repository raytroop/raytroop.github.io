---
title: Signaling for Data Converter
date: 2025-06-21 18:54:55
tags:
categories:
- analog
mathjax: true
---

## Sigma-Delta DAC

Sigma-delta digital-to-analog converters (SD DAC’s) are often used for *discrete-time signals* with *sample rate much higher than their bandwidth*

- Because of the high sample rate relative to signal bandwidth, ***a very simple DAC reconstruction filter* (*Analog lowpass filter*)** suffices, often just a *one-pole RC lowpass*

![image-20250616000829208](signaling-adda/image-20250616000829208.png)





```matlab
R= 4.7e3;                 % ohms resistor value
C= .01e-6;                % F capacitor value
fs= 1e6;                  % Hz DAC sample rate
% input signal
x= [zeros(1,20) .9*ones(1,200) .1*ones(1,200)];
% find output y of SD DAC and output y_filt of RC filter
[y,y_filt]= sd_dacRC(x,R,C,fs);

t = linspace(0,length(x)-1, length(x))*1/fs*1e3;
subplot(3,1,1)
plot(t, x, '.'); title('x'); grid on
subplot(3,1,2)
plot(t, y, '.'); title('y'); grid on
subplot(3,1,3)
plot(t, y_filt); title('y_{filt}'); xlabel('t(ms)'); grid on
```

![image-20250621223451691](signaling-adda/image-20250621223451691.png)



---

```matlab
% https://www.dsprelated.com/showarticle/1642.php
% Neil Robertson, Model a Sigma-Delta DAC Plus RC Filter

% function [y,y_filt] = sd_dacRC(x,R,C,fs)  2/5/24 Neil Robertson
% 1-bit sigma-delta DAC with RC filter
% Model does not include a zero-order hold.
%
% x = input signal vector, 0 <= x < 1
% R = series resistor value, Ohms.  Normally R > 1000 for 3.3 V logic.
% C = shunt capacitor value, Farads
% fs = sample frequency, Hz
% y = DAC output signal vector, y(n) = 0 or 1
% y_filt = RC filter output signal vector
%
function [y,y_filt] = sd_dacRC(x,R,C,fs)
N= length(x);
x= fix(x*2^16)/2^16;        % quantize x to 16 bits
%I 1-bit Sigma-delta DAC
s= [x(1) zeros(1,N-1)];
for n= 2:N
    u= x(n) + s(n-1);
    s(n)= mod(u,1);        % sum
    y(n)= fix(u);          % carry
end

%II One-pole RC filter model
% Matched z-Transform https://ocw.mit.edu/courses/2-161-signal-processing-continuous-and-discrete-fall-2008/cc00ac6d468dc9dcf2238fc1d1a194d4_lecture_19.pdf
Ts= 1/fs;
Wc= 1/(R*C);               % rad -3 dB frequency
fc= Wc/(2*pi);             % Hz -3 dB frequency
a1= -exp(-Wc*Ts);
b0= 1 + a1;                % numerator coefficient
a= [1 a1];                 % denominator coeffs
y_filt= filter(b0,a,y);    % filter the DAC's output signal y

```



## DAC ZOH

![image-20250628204404959](signaling-adda/image-20250628204404959.png)

> The last D2C is in human vision, which connect discrete time $y(m)$ with line, implicitly

![image-20250628203216965](signaling-adda/image-20250628203216965.png)





## Noise-Shaping SAR ADCs

*TODO* &#128197;



## DC Gain in Interpolation Filtering

> [[https://raytroop.github.io/2025/06/21/data-converter-in-action/#dac-zoh](https://raytroop.github.io/2025/06/21/data-converter-in-action/#dac-zoh)]

DC gain is used to compensate the ratio of sampling rate before and after upsample

![image-20250701070539064](signaling-adda/image-20250701070539064.png)

Given
$$
X_e = X =  \propto \frac{1}{T} = \frac{1}{L\cdot T_i}
$$
Then, the lowpass filter (ZOH, FOH .etc) gain shall be $L$

---

Employ definition of DTFT,  $X(e^{j\hat{\omega}})
=\sum_{n=-\infty}^{+\infty}x[n]e^{-j\hat{\omega} n}$, and set $\hat{\omega} = 0$
$$
X(e^{j0}) = \sum_{n=-\infty}^{+\infty}x[n]
$$
That is, $\sum_{n=-\infty}^{+\infty}x[n] = \sum_{n=-\infty}^{+\infty}x_e[n]$, so
$$
\overline{x_e[n]} = \frac{1}{L} \overline{x[n]}
$$
It also indicate that dc gain of upsampling is $1/L$




### ZOH

> Zero-Order Hold (ZOH)

![image-20250630235534325](signaling-adda/image-20250630235534325.png)

> dc gain = $N$

### FOH

> First-Order Hold (FOH) 

![image-20250630235714996](signaling-adda/image-20250630235714996.png)

> dc gain = $N$





## reference

Dan Boschen. sigma delta modulator for DAC [[https://dsp.stackexchange.com/a/88357/59253](https://dsp.stackexchange.com/a/88357/59253)]

Neil Robertson, Model a Sigma-Delta DAC Plus RC Filter [[https://www.dsprelated.com/showarticle/1642.php](https://www.dsprelated.com/showarticle/1642.php)]

—, Modeling a Continuous-Time System with Matlab [[https://www.dsprelated.com/showarticle/1055.php](https://www.dsprelated.com/showarticle/1055.php)]

—, Modeling Anti-Alias Filters [[https://www.dsprelated.com/showarticle/1418.php](https://www.dsprelated.com/showarticle/1418.php)]

—, DAC Zero-Order Hold Models [[https://www.dsprelated.com/showarticle/1627.php](https://www.dsprelated.com/showarticle/1627.php)]

—, “A Simplified Matlab Function for Power Spectral Density”, DSPRelated.com, March, 2020, [[https://www.dsprelated.com/showarticle/1333.php](https://www.dsprelated.com/showarticle/1333.php)]

Jason Sachs. Return of the Delta-Sigma Modulators, Part 1: Modulation [[https://www.dsprelated.com/showarticle/1517/return-of-the-delta-sigma-modulators-part-1-modulation](https://www.dsprelated.com/showarticle/1517/return-of-the-delta-sigma-modulators-part-1-modulation)]

Woogeun Rhee. ISCAS 2019 Mini Tutorials: Single-Bit Delta-Sigma Modulation Techniques for Robust Wireless Systems [[https://youtu.be/OEyTM4-_OyA?si=vllJ5Pe8I3lqb_Vl](https://youtu.be/OEyTM4-_OyA?si=vllJ5Pe8I3lqb_Vl)]

---

Venkatesh Srinivasan, ISSCC 2019 T5: Noise Shaping in Data Converters

Nan Sun,IEEE CAS 2020: Break the kT/C Noise Limit [[https://www.facebook.com/ieeecas/videos/break-the-ktc-noise-limit/322899188976197/](https://www.facebook.com/ieeecas/videos/break-the-ktc-noise-limit/322899188976197/)]

Yun-Shiang Shu, ISSCC 2022 T3: Noise-Shaping SAR ADCs

Xiyuan Tang, CICC 2025 ES2-1: Noise-Shaping SAR ADCs - From Fundamentals to Recent Advances

---

Qasim Chaudhari. On Analog-to-Digital Converter (ADC), 6 dB SNR Gain per Bit, Oversampling and Undersampling [[https://wirelesspi.com/on-analog-to-digital-converter-adc-6-db-snr-gain-per-bit-oversampling-and-undersampling/](https://wirelesspi.com/on-analog-to-digital-converter-adc-6-db-snr-gain-per-bit-oversampling-and-undersampling/)]

---

Pavan, Shanthi, Richard Schreier, and Gabor Temes. (2016) 2016. Understanding Delta-Sigma Data Converters. 2nd ed. Wiley. 

