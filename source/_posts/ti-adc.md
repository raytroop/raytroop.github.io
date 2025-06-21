---
title: Time-Interleaved ADCs
date: 2025-06-07 23:17:25
tags:
categories:
- analog
mathjax: true
---

![image-20250611222614434](ti-adc/image-20250611222614434.png)

## Interleaver

![image-20250621094704819](ti-adc/image-20250621094704819.png)



### Direct Interleaver

![image-20250621101542418](ti-adc/image-20250621101542418.png)



> similar to increase the resolution of the flash ADC with *more* parallel comparators



### De-multiplexing Interleaver

![image-20250621103205333](ti-adc/image-20250621103205333.png)



> it is the *front-end samplers* that determine *timing/bandwidth mismatch errors*



### Re-sampling Interleaver

 ![image-20250621111119041](ti-adc/image-20250621111119041.png)



> back-end re-sampling occur after the front-end,  two $\frac{KT}{C}$ contribution in total noise (De-multiplexing Interleaver only one $\frac{KT}{C}$)
>
> without buffer, charging distribution reduce signal and reduce SNR, but buffers give excess noise



### Interleaver Model





## Interleaving Errors

![image-20250621072540691](ti-adc/image-20250621072540691.png)

![image-20250621093552545](ti-adc/image-20250621093552545.png)



### Offset Mismatch Error

![image-20250621072621033](ti-adc/image-20250621072621033.png)



### Gain Mismatch Error

![image-20250621072824275](ti-adc/image-20250621072824275.png)

![image-20250621072944516](ti-adc/image-20250621072944516.png)



### Timing Mismatch Error

![image-20250621090407014](ti-adc/image-20250621090407014.png)

$\pi/2$-rad phase: the maximum error occurs at the ***zero crossing*** and not on the peaks (Gain Mismatch error)

Frequency-dependent: the *higher* frequency input signal $f_\text{in}$, the *larger* error becomes

> ![image-20250621091024424](ti-adc/image-20250621091024424.png)
>
> ![image-20250621091047339](ti-adc/image-20250621091047339.png)
>
> $\pi/2$ phase shift
> $$
> e^{j\pi/2} = j
> $$
> frequency-dependent
> $$
> V^{'} \propto  f
> $$
>
> In time domain
> $$
> \frac{d\sin(\omega t)}{dt} = \omega \cos(\omega t) \propto \omega
> $$





### Bandwidth Mismatch Errors 

![image-20250621092214162](ti-adc/image-20250621092214162.png)

> ![image-20250621093321623](ti-adc/image-20250621093321623.png)



## Overlapping versus Non-overlapping track time

![image-20250611224418950](ti-adc/image-20250611224418950.png)



tracking accuracy stay same, Cin (2Cs) counteract the longer tracking





## reference

John P. Keane, ISSCC2020 T5: "Fundamentals of Time-Interleaved ADCs" [[https://www.nishanchettri.com/isscc-slides/2020%20ISSCC/TUTORIALS/T5Visuals.pdf](https://www.nishanchettri.com/isscc-slides/2020%20ISSCC/TUTORIALS/T5Visuals.pdf)]

Yohan Frans, CICC2019 ES3-3- "ADC-based Wireline Transceivers" [[pdf](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=8780306)]

Samuel Palermo, ISSCC 2018 T10: ADC-Based Serial Links: Design and Analysis [[https://www.nishanchettri.com/isscc-slides/2018%20ISSCC/TUTORIALS/T10/T10Visuals.pdf](https://www.nishanchettri.com/isscc-slides/2018%20ISSCC/TUTORIALS/T10/T10Visuals.pdf)]

ISSCC2015 F1: High-Speed Interleaved ADCs [[https://picture.iczhiku.com/resource/eetop/wykrheUfrWasiMVX.pdf](https://picture.iczhiku.com/resource/eetop/wykrheUfrWasiMVX.pdf)]

Poulton, Ken. ISSCC2015 "Interleaved ADCs Through the Ages", [(slides)](http://poulton.net/papers.public/2015isscc_interleaved.forum.pdf)

Poulton, Ken. CICC2010 "GHz ADCs: From Exotic to Mainstream", tutorial session, [(slides)](http://poulton.net/papers.public/2010_cicc_GHz_ADCs.pdf)

Poulton, Ken. ISSCC2009  "Time-Interleaved ADCs, Past and Future" [(slides)](http://poulton.net/papers.public/2009_isscc_se0604_interleaving.pdf)

Athanasios Ramkaj. January 26, 2022, IEEE SSCS Santa Clara Valley Section Technical Talk: Design Considerations Towards Optimal High-Resolution Wide-Bandwidth Time-Interleaved ADCs [[https://youtu.be/k3jY9NtfYlY?si=K9AdT9QzGxOnI5WG](https://youtu.be/k3jY9NtfYlY?si=K9AdT9QzGxOnI5WG)]

Ahmed M. A. Ali 2016, "High Speed Data Converters" [[pdf](https://picture.iczhiku.com/resource/eetop/sYKhdRGJFFGyZbcB.pdf)]

S. Jang, J. Lee, Y. Choi, D. Kim, and G. Kim, "[Recent advances in ultra-high-speed wireline receivers with ADC-DSP-based equalizers](https://ieeexplore.ieee.org/document/10767763)," *IEEE* *Open Journal of the Solid-State Circuits Society* (OJ-SSCS), vol. 4, pp. 290-304, Nov. 2024.

Yida Duan. Design Techniques for Ultra-High-Speed Time-Interleaved Analog-to-Digital Converters (ADCs) [[http://www2.eecs.berkeley.edu/Pubs/TechRpts/2017/EECS-2017-10.pdf](http://www2.eecs.berkeley.edu/Pubs/TechRpts/2017/EECS-2017-10.pdf)]

Preview Lecture #1 - "Extreme SAR ADCs" Online Course (2024) - Prof. Chi-Hang Chan (U. of Macau) [[https://youtu.be/rgMRL4QZ-wA?si=gvJGFrcsrHS8b_mN](https://youtu.be/rgMRL4QZ-wA?si=gvJGFrcsrHS8b_mN)]

