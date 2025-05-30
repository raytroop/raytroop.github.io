---
title: Phase Noise and Jitter Simulation
date: 2023-10-21 11:33:58
tags:
categories:
- noise
mathjax: true
---



## Jitter and Edge phase noise

[[https://community.cadence.com/cadence_technology_forums/f/custom-ic-design/56929/how-to-derive-edge-phase-noise-from-output-noise-in-sampled-pnoise-simulation/1388888](https://community.cadence.com/cadence_technology_forums/f/custom-ic-design/56929/how-to-derive-edge-phase-noise-from-output-noise-in-sampled-pnoise-simulation/1388888)]

![ ](pn-jitter/jitter.edgePhase.Noise.png)

![ ](pn-jitter/sampledNoise-2.png)





## Phase Noise Aliasing & Integration Limits

These two types of measurements deliver the **same rms jitter** of $f_{CK}$

- both rising and falling:  integrated from $-f_{CK}$ to $+f_{CK}$
- only the rising (or falling) edges: integrated from $-f_{CK}/2$ to $+f_{CK}/2$

![image-20250524074831161](pn-jitter/image-20250524074831161.png)

![image-20250523221143537](pn-jitter/image-20250523221143537.png)

*temporal autocorrelation* and *Wiener-Khinchin theorem* is more appropriate to arise *rms value* 

> Y. Zhao and B. Razavi, "Phase Noise Integration Limits for Jitter Calculation,"[[https://www.seas.ucla.edu/brweb/papers/Conferences/YZ_ISCAS_22.pdf](https://www.seas.ucla.edu/brweb/papers/Conferences/YZ_ISCAS_22.pdf)]



## time-average noise (phase-noise) & sampled noise (edge-phase noise or jitter) spectrum

![image-20250530203348622](pn-jitter/image-20250530203348622.png)

### Time-average noise analysis

![image-20250530203720538](pn-jitter/image-20250530203720538.png)![image-20250530204820891](pn-jitter/image-20250530204820891.png)

> $S_{\Delta f}(f)$ between $[\Delta f, F_0/2]$ may be *less than* that of other harmonic window



### Sampled noise analysis

![image-20250530204030405](pn-jitter/image-20250530204030405.png)

![image-20250530204222221](pn-jitter/image-20250530204222221.png)

### correlation

![image-20250530205849830](pn-jitter/image-20250530205849830.png)

![image-20250530205919247](pn-jitter/image-20250530205919247.png)

![image-20250530210543667](pn-jitter/image-20250530210543667.png)



## VCO Phase Noise

### pnoise - timeaverage

1. *Direct Plot/Pnoise/Phase Noise* or

   ![image-20220511112856934](pn-jitter/image-20220511112856934.png)

2. manually calculate by definition

   ![image-20220511112806122](pn-jitter/image-20220511112806122.png)

3. `output noise` with unit `dBc`

   *Direct Plot/Pnoise/Output Noise Units:dBc/Hz and Noise convention: SSB*

   ![image-20220511113248984](pn-jitter/image-20220511113248984.png)

> The above method 2 and 3 only apply to `timeaveage` pnoise simulation, 

### pnoise - sampled(jitter)/Edge Crossing

![EdgePhaseNoise.drawio](pn-jitter/EdgePhaseNoise.drawio.svg)

*Direct Plot/Pnoise/**Edge** Phase Noise* or

![image-20220515214901120](pn-jitter/image-20220515214901120.png)

Another way, the following equation can also be used for `sampled(jitter)/Edge Crossing` 

```
PhaseNoise(dBc/Hz) = dB20( OutputNoise(V/sqrt(Hz)) / slopeCrossing / Tper*twoPi ) - dB10(2)
```

where `dB10(2)` is used to obtain SSB from DSB

![image-20220511150337318](pn-jitter/image-20220511150337318.png)

### Output Noise of sampled(jitter) pnoise

The last section's `Output Noise (V**2/Hz)` can be obtained by *transient noise simulation*

The idea is that sample waveform with ideal clock, subtract DC offset, then fft(psd)

- samplesRaw = sample(wv)
- samplePost = samplesRaw - average(samplesRaw)
- Output Noise (V**2/Hz) = psd(samplePost)

![image-20220516184543148](pn-jitter/image-20220516184543148.png)

![image-20220516184844296](pn-jitter/image-20220516184844296.png)

**Expression**:

![image-20220516185506348](pn-jitter/image-20220516185506348.png)

> The computation cost is typically very high, and the accuracy is lesser as compared to PSS/Pnoise



## Pnoise Sampled(jitter): Sampled Phase Option

- Identical to **noisetype=timedomain** in old GUI
- Use model:
  - Sampleds Per Period: number of ponits
  - Add Specific Points: specific time point, still time points

![image-20220712085426461](pn-jitter/image-20220712085426461.png)

![image-20220712085836315](pn-jitter/image-20220712085836315.png)

![image-20220712090011204](pn-jitter/image-20220712090011204.png)

> pss beat freq = 5GHz
>
> pnoise sweeptype: absolute, from 100k to 2.5GHz



## Transient noise

### phase noise from transient noise analysis

1. The Phase Noise function is now available in the Direct Plot form (Results-Direct Plot-Main Form) after Transient Analysis is run
   - Absolute jitter Method
   - Direct Power Spectral Density Method
2. `PN` phase noise function
   - Absolute jitter Method
   - Direct Power Spectral Density Method

> **Absolute jitter Method**: Phase noise is defined as the power spectral density of the absolute jitter of an input waveform
>
> and **absolute jitter method** is the default method 



In below discussion, we only think about the `absolute jitter method`

### PSD and Phase Noise

> - phase noise is single-sideband
> - psd is double-sideband
> - Then the  ratio is **2**

#### By PSS_Pnoise

`jee`

```
rfEdgePhaseNoise(?result "pnoise_sample_pm0" ?eventList 'nil) + 10 * log10(2)
```

> convert **single-sideband** phase noise to psd by multiplying 2 or `10 * log10(2)`

#### By trannoise `PN` function

```
PN(clip(VT("/Out1") 2.60417e-08 0.000400052) "rising" 1.65 ?Tnom (1 / 3.84e+07) ?windowName "Rectangular" ?smooth 1 ?windowSize 15000 ?detrending "None" ?cohGain 1 ?methodType "absJitter")
```

> double-sideband psd

#### By trannoise `psd` and `abs_jitter` function

```
dB10(psd(abs_jitter(clip(VT("/Out1") 2.60417e-08 0.000400052) "rising" 1.65 ?Tnom (1 / 3.84e+07)) 2.60417e-08 0.000400052 15360 ?windowName "Rectangular" ?smooth 1 ?windowSize 15000 ?detrending "None" ?cohGain 1))
```

> double-sideband psd
>
> `abs_jitter` *Y-Unit* default is `rad`

#### Comparison

![image-20220506225324377](pn-jitter/image-20220506225324377.png)

>  `PN`'s result is same with `psd`'s

### RMS value

- build the `abs_jitter` function with *seconds as the Y axis* and add the `stddev` function to determine the Jee jitter value
- or integrate psd

The RMS $x_{\text{RMS}}$ of a discrete domain signal $x(n)$ is given by
$$
x_{\text{RMS}}=\sqrt{\frac{1}{N}\sum_{n=0}^{N-1}|x(n)|^2}
$$
Inserting Parseval's theorem given by
$$
\sum_{n=0}^{N-1}|x(n)|^2=\frac{1}{N}\sum_{n=0}^{N-1}|X(k)|^2
$$
allows for computing the RMS from the spectrum $X(k)$ as
$$
x_{\text{RMS}}=\sqrt{\frac{1}{N^2}\sum_{n=0}^{N-1}|X(k)|^2}
$$


### Remarks

Cadence Spectre's `PN` function may call `abs_jitter` and `psd` function under the hood.




## reference

Article (11514536) Title: How to obtain a phase noise plot from a transient noise analysis
URL: [https://support.cadence.com/apex/ArticleAttachmentPortal?id=a1Od0000000nb1CEAQ](https://support.cadence.com/apex/ArticleAttachmentPortal?id=a1Od0000000nb1CEAQ)

Article (20500632) Title: How to simulate Random and Deterministic Jitters
URL: [https://support.cadence.com/apex/ArticleAttachmentPortal?id=a1O3w000009fiXeEAI](https://support.cadence.com/apex/ArticleAttachmentPortal?id=a1O3w000009fiXeEAI)

Cadence, Application Note: Understanding the relations between time-average noise (phase-noise) and sampled noise (edge-phase noise or jitter) in Pnoise analysis

Tutorial on Scaling of the Discrete Fourier Transform and the Implied Physical Units of the Spectra of Time-Discrete Signals Jens Ahrens, Carl Andersson, Patrik Höstmad, Wolfgang Kropp URL: [https://appliedacousticschalmers.github.io/scaling-of-the-dft/AES2020_eBrief/](https://appliedacousticschalmers.github.io/scaling-of-the-dft/AES2020_eBrief/)
