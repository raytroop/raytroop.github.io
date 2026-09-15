---
title: High-Speed ADC for SerDes
date: 2025-09-05 11:04:47
tags:
categories:
- link
mathjax: true
---



![image-20260912112631937](hs-adc-serdes/image-20260912112631937.png)



## Timing Skew for Broadband signals

> M. El-Chammas and B. Murmann, "General Analysis on the Impact of Phase-Skew Mismatch in Time-Interleaved ADCs," IEEE Trans. on Circuits and Systems I, vol. 56, No. 5, pp. 902-910, May 2009 [[https://sci-hub.ru/10.1109/TCSI.2009.2015206](https://sci-hub.ru/10.1109/TCSI.2009.2015206)]
>
> —, "Background Calibration of Timing Skew in Time-Interleaved A/D Converters," Ph.D. Thesis, Stanford University, August 2010 [[https://purl.stanford.edu/xc093xt9301](https://purl.stanford.edu/xc093xt9301)]
>
> —, "Time-Interleaved ADCs: Theory and Design," Tutorial in IEEE International Conf. on Elec., Circ., and Sys., Lebanon, December 2011 [[https://el-chammas.com/papers/Manar_ICECS_handouts.pdf](https://el-chammas.com/papers/Manar_ICECS_handouts.pdf)]
>
> —, "The World of Time-Interleaved ADCs: From Theory to Design," Tutorial in IEEE International NEWCAS Conf., Montreal, Canada, June 2012 [[https://el-chammas.com/papers/Manar_NEWCAS_TIADC_tutorial.pdf](https://el-chammas.com/papers/Manar_NEWCAS_TIADC_tutorial.pdf)]
>
> —, "A 12-GS/s 81-mW 5-bit Time-Interleaved Flash ADC With Background Timing Skew Calibration," in IEEE Journal of Solid-State Circuits, vol. 46, no. 4, pp. 838-847, April 2011

![image-20260913202344592](hs-adc-serdes/image-20260913202344592.png)



<span style="color:white; background-color:black">"Best-fit" approach</span>

![image-20260913213529847](hs-adc-serdes/image-20260913213529847.png)

Using a **normalized autocorrelation** (or equivalently assuming <span style="color:#FF5733">**unit signal power**</span>) — $\color{red}R(\tau) = \frac{R_x(\tau)}{R_x(0)}$

![image-20260913215052664](hs-adc-serdes/image-20260913215052664.png)

For this ideal low-pass-filtered white-noise input,

$$
\boxed{ \frac{1}{|R''(0)|} = \frac{3}{4\pi^2f_c^2}}
$$

Notice the difference from the sinusoidal case: for a sinusoid,

$$
|R''(0)|=(2\pi f)^2
$$

whereas for ideal LPF white noise,

$$
\boxed{ |R''(0)|=\textcolor{red}{\frac{1}{3}}(2\pi f_c)^2}
$$

That factor of $1/3$ comes from averaging all frequencies uniformly from $-f_c$ to $f_c$, rather than having all the signal power concentrated at a single frequency



<span style="color:white; background-color:black">The sinusoidal approach</span>

![image-20260913204139288](hs-adc-serdes/image-20260913204139288.png)





---

> Boris Murmann, August 2013 Lectures on Circuit and Architecture Design for High-Speed ADCs — *Determining ADC specs from system specs* [[https://bbs.eetop.cn/thread-979682-1-1.html](https://bbs.eetop.cn/thread-979682-1-1.html)]

![image-20260913205226885](hs-adc-serdes/image-20260913205226885.png)



![image-20260913223921349](hs-adc-serdes/image-20260913223921349.png)








## BER with Quantization Noise

![image-20240804110522955](hs-adc-serdes/image-20240804110522955.png)




> $$
> \text{Var}(X) = E[X^2] - E[X]^2
> $$
>
> ![image-20240804110235178](hs-adc-serdes/image-20240804110235178.png)



## reference

Samuel Palermo, ISSCC 2018 T10: ADC-Based Serial Links: Design and Analysis

Yohan Frans, CICC2019 ES3-3- "ADC-based Wireline Transceivers" [[pdf](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=8780306)]

Nhat Nguyen and Masum Hossain, ISSCC 2021 Forum 6.7: 112Gb/s-and-Beyond Long-Reach and Short-Reach Electrical Interfaces

T. Chan Carusone, T. O. Dickson, S. Palermo, S. Shekhar and M. Mansuri, "Modern Wireline Transceivers," in *IEEE Journal of Solid-State Circuits*, vol. 61, no. 2, pp. 395-422, Feb. 2026 [[https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=11311714](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=11311714)] 

---

Akkaya, A. (2021). High-Speed ADC Design and Optimization for Wireline Links (Publication No. 8453) [PhD thesis, EPFL; Supervised by Y. Leblebici]. [[https://doi.org/10.5075/epfl-thesis-8453](https://doi.org/10.5075/epfl-thesis-8453)]

K. Zheng, “System-driven circuit design for ADC-based wireline data links,” Stanford Univ., Stanford, CA, USA, Tech. Rep., 2018 [[https://stacks.stanford.edu/file/hw458fp0168/thesis-augmented.pdf](https://stacks.stanford.edu/file/hw458fp0168/thesis-augmented.pdf)]

Kull, Lukas, Thomas Toifl, Martin L. Schmatz, Pier Andrea Francese, Christian Menolfi, Matthias Braendli, Marcel A. Kossel, Thomas Morf, Toke Meyer Andersen and Yusuf Leblebici. “22.1 A 90GS/s 8b 667mW 64× interleaved SAR ADC in 32nm digital SOI CMOS.” *2014 IEEE International Solid-State Circuits Conference Digest of Technical Papers (ISSCC)* (2014): 378-379. [[https://sci-hub.jp/10.1109/ISSCC.2014.6757477](https://sci-hub.jp/10.1109/ISSCC.2014.6757477)]

—. (2014). High-Speed CMOS ADC Design for 100Gb/s Communication Systems (Publication No. 6037) [PhD thesis, EPFL; Supervised by Y. Leblebici]. https://doi.org/10.5075/epfl-thesis-6037

—., "A 3.1mW 8b 1.2GS/s single-channel asynchronous SAR ADC with alternate comparators for enhanced speed in 32nm digital SOI CMOS," *2013 IEEE International Solid-State Circuits Conference Digest of Technical Papers*, San Francisco, CA, USA, 2013, pp. 468-469 [[https://sci-hub.jp/10.1109/ISSCC.2013.6487818](https://sci-hub.jp/10.1109/ISSCC.2013.6487818)]

—., "A 3.1 mW 8b 1.2 GS/s Single-Channel Asynchronous SAR ADC With Alternate Comparators for Enhanced Speed in 32 nm Digital SOI CMOS," in *IEEE Journal of Solid-State Circuits*, vol. 48, no. 12, pp. 3049-3058, Dec. 2013 [[https://sci-hub.jp/10.1109/JSSC.2013.2279571](https://sci-hub.jp/10.1109/JSSC.2013.2279571)]
