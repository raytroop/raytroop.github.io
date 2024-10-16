---
title: DPLL Based Clock and Data Recovery
date: 2024-09-23 21:04:41
tags:
categories:
- analog
mathjax: true
---

## Decimation

- Decimation is commonly employed to alleviate the high-speed requirement. However, decimation increases loop-latency which causes excessive dither jitter.
- Decimation is basically, widen the data and slowing it down
- Decimating by $L$ means frequency register only added once every $L$ UI, thus *integral path gain* reduced by $L$ in linear model
- *proportional path gain* is unchanged

![intg_path_decim.drawio](dpll-cdr/intg_path_decim.drawio.svg)


### Decimation by Summing

> In DSP this is called *boxcar filter*
>
> $\sum d_n$, where $d_n \in \{-1, 0, 1\}$

- Decimation via boxcar filter produces a DC gain, $K_b$, corresponding to the *decimation factor*. 



### Decimation by Voting

> equivalent $\sum d_n \lt 0 \to -1$, $\sum d_n = 0 \to 0$ and $\sum d_n\gt 0 \to 1$
>
> Compared to the boxcar filter, voting is able to reduce the loop delay and lower the output noise of the MMPD

- Decimation via voting has a reduced gain, $K_V$, which can be determined through simulation


---

![image-20240813223338067](dpll-cdr/image-20240813223338067.png)



## Digital to Phase Converter (DPC) 

Converts *digital code* from the phase integrator into an edge location with respect to the local
reference clock

- Phase Interpolator (PI), phase rotator, DLL, etc

> Phase interpolators realize digital-to-phase conversion (DPC)





> P. Palestri *et al*., "Analytical Modeling of Jitter in Bang-Bang CDR Circuits Featuring Phase Interpolation," in *IEEE Transactions on Very Large Scale Integration (VLSI) Systems*, vol. 29, no. 7, pp. 1392-1401, July 2021 [[https://sci-hub.se/10.1109/TVLSI.2021.3068450](https://sci-hub.se/10.1109/TVLSI.2021.3068450)]





## reference

J. L. Sonntag and J. Stonick, "A Digital Clock and Data Recovery Architecture for Multi-Gigabit/s Binary Links," in *IEEE Journal of Solid-State Circuits*, vol. 41, no. 8, pp. 1867-1875, Aug. 2006

John T. Stonick, ISSCC 2011 tutorial. "DPLL Based Clock and Data Recovery" [[https://www.nishanchettri.com/isscc-slides/2011%20ISSCC/TUTORIALS/ISSCC2011Visuals-T5.pdf](https://www.nishanchettri.com/isscc-slides/2011%20ISSCC/TUTORIALS/ISSCC2011Visuals-T5.pdf)]

P. K. Hanumolu, M. G. Kim, G. -y. Wei and U. -k. Moon, "A 1.6Gbps Digital Clock and Data Recovery Circuit," *IEEE Custom Integrated Circuits Conference 2006*, San Jose, CA, USA, 2006, pp. 603-606

Pavan Hanumolu, ISSCC 2015 tutorial. "Clock and Data Recovery Architectures & Circuits" 

Liu, Tao, Tiejun Li, Fangxu Lv, Bin Liang, Xuqiang Zheng, Heming Wang, Miaomiao Wu, Dechao Lu, and Feng Zhao. 2021. "Analysis and Modeling of Mueller-Muller Clock and Data Recovery Circuits" *Electronics* 10, no. 16: 1888. https://doi.org/10.3390/electronics10161888

Gu, Youzhi & Feng, Xinjie & Chi, Runze & Chen, Yongzhen & Wu, Jiangfeng. (2022). Analysis of Mueller-Muller Clock and Data Recovery Circuits with a Linearized Model. 10.21203/rs.3.rs-1817774/v1. [[https://assets-eu.researchsquare.com/files/rs-1817774/v1_covered.pdf?c=1664188179](https://assets-eu.researchsquare.com/files/rs-1817774/v1_covered.pdf?c=1664188179)]

H. Kang et al., "A 42.7Gb/s Optical Receiver With Digital Clock and Data Recovery in 28nm CMOS," in IEEE Access, vol. 12, pp. 109900-109911, 2024 [[https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=10630516](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=10630516)]

Marinaci, Stefano. "Study of a Phase Locked Loop based Clock and Data Recovery Circuit for 2.5 Gbps data-rate" [[https://cds.cern.ch/record/2870334/files/CERN-THESIS-2023-147.pdf](https://cds.cern.ch/record/2870334/files/CERN-THESIS-2023-147.pdf)]

