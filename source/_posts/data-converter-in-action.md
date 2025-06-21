---
title: Data Converter in Action
date: 2025-06-21 18:54:55
tags:
categories:
- analog
mathjax: true
---

## Sigma-Delta DAC

Sigma-delta digital-to-analog converters (SD DAC’s) are often used for *discrete-time signals* with *sample rate much higher than their bandwidth*

- Because of the high sample rate relative to signal bandwidth, ***a very simple DAC reconstruction filter* (*Analog lowpass filter*)** suffices, often just a *one-pole RC lowpass*

![image-20250616000829208](data-converter-in-action/image-20250616000829208.png)





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

![image-20250621223451691](data-converter-in-action/image-20250621223451691.png)





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

