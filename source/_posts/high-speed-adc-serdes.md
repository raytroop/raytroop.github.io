---
title: High-Speed ADC for SerDes
date: 2025-09-05 11:04:47
tags:
categories:
- link
mathjax: true
---



Time-interleaved SAR ADCs are an optimal choice for high-speed ADCs with moderate resolution



## BER with Quantization Noise

![image-20240804110522955](high-speed-adc-serdes/image-20240804110522955.png)




> $$
> \text{Var}(X) = E[X^2] - E[X]^2
> $$
>
> ![image-20240804110235178](high-speed-adc-serdes/image-20240804110235178.png)



## reference

Akkaya, A. (2021). High-Speed ADC Design and Optimization for Wireline Links (Publication No. 8453) [PhD thesis, EPFL; Supervised by Y. Leblebici]. [[https://doi.org/10.5075/epfl-thesis-8453](https://doi.org/10.5075/epfl-thesis-8453)]

K. Zheng, “System-driven circuit design for ADC-based wireline data links,” Stanford Univ., Stanford, CA, USA, Tech. Rep., 2018 [[https://stacks.stanford.edu/file/hw458fp0168/thesis-augmented.pdf](https://stacks.stanford.edu/file/hw458fp0168/thesis-augmented.pdf)]

T. Chan Carusone, T. O. Dickson, S. Palermo, S. Shekhar and M. Mansuri, "Modern Wireline Transceivers," in *IEEE Journal of Solid-State Circuits*, vol. 61, no. 2, pp. 395-422, Feb. 2026 [[https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=11311714](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=11311714)]

Kull, Lukas, Thomas Toifl, Martin L. Schmatz, Pier Andrea Francese, Christian Menolfi, Matthias Braendli, Marcel A. Kossel, Thomas Morf, Toke Meyer Andersen and Yusuf Leblebici. “22.1 A 90GS/s 8b 667mW 64× interleaved SAR ADC in 32nm digital SOI CMOS.” *2014 IEEE International Solid-State Circuits Conference Digest of Technical Papers (ISSCC)* (2014): 378-379. [[https://sci-hub.jp/10.1109/ISSCC.2014.6757477](https://sci-hub.jp/10.1109/ISSCC.2014.6757477)]

—. (2014). High-Speed CMOS ADC Design for 100Gb/s Communication Systems (Publication No. 6037) [PhD thesis, EPFL; Supervised by Y. Leblebici]. https://doi.org/10.5075/epfl-thesis-6037
