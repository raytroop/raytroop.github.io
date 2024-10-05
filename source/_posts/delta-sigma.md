---
title: Delta-Sigma Data Converters
date: 2024-09-08 16:48:32
tags:
categories:
- analog
mathjax: true
---



The average output of DSM tracks the input signal

---



## Delta Modulator

![image-20240908173930949](delta-sigma/image-20240908173930949.png)

$$\begin{align}
(V_{in} - V_F) &= D_{out} \\
D_{out} &= s V_F
\end{align}$$

Therefore $V_{in} - \frac{D_{out}}{s} = D_{out}$
$$
D_{out} = \frac{s}{s+1} V_{in}
$$


> attenuates the low-frequency content of the signal, and amplifies high-frequency noise.



## MOD1

![image-20241005120659945](delta-sigma/image-20241005120659945.png)

- A binary DAC (and hence a binary modulator) is inherently linear
- With a CT loop filter, MOD1 has inherent anti-alising



## MOD2

![image-20241005160203074](delta-sigma/image-20241005160203074.png)







## Delta-Sigma Modulator

*TODO* &#128197;



## integrator

*TODO* &#128197;



### opamp bandwidth & slewing

*TODO* &#128197;



## decimation filter

The combination of the the *digital post-filter* and *downsampler* is called the **decimation filter** or **decimator**

![image-20241005190053391](delta-sigma/image-20241005190053391.png)

![image-20241005190126691](delta-sigma/image-20241005190126691.png)

> [https://classes.engr.oregonstate.edu/eecs/spring2017/ece627/Lecture%20Notes/First-Order%20D-S%20ADC.pdf](https://classes.engr.oregonstate.edu/eecs/spring2017/ece627/Lecture%20Notes/First-Order%20D-S%20ADC.pdf)






## reference

R. Schreier, ISSCC2006 tutorial: Understanding Delta-Sigma Data Converters

Bruce A. Wooley , 2012, "The Evolution of Oversampling Analog-to-Digital Converters" [[https://r6.ieee.org/scv-sscs/wp-content/uploads/sites/80/2012/06/Oversampling-Wooley_SCV-ver2.pdf](https://r6.ieee.org/scv-sscs/wp-content/uploads/sites/80/2012/06/Oversampling-Wooley_SCV-ver2.pdf)]

B. Razavi, "The Delta-Sigma Modulator [A Circuit for All Seasons]," IEEE Solid-State Circuits Magazine, Volume. 8, Issue. 20, pp. 10-15, Spring 2016. [[http://www.seas.ucla.edu/brweb/papers/Journals/BRSpring16DeltaSigma.pdf](http://www.seas.ucla.edu/brweb/papers/Journals/BRSpring16DeltaSigma.pdf)]

Pavan, Shanthi, Richard Schreier, and Gabor Temes. (2016) 2016. Understanding Delta-Sigma Data Converters. 2nd ed. Wiley.

---

Richard E. Schreier, ECE 1371 Advanced Analog Circuits - 2015 [[http://individual.utoronto.ca/schreier/ece1371-2015.html](http://individual.utoronto.ca/schreier/ece1371-2015.html)]

Gabor C. Temes. ECE 627-Oversampled Delta-Sigma Data Converters [[https://classes.engr.oregonstate.edu/eecs/spring2017/ece627/lecturenotes.html](https://classes.engr.oregonstate.edu/eecs/spring2017/ece627/lecturenotes.html)]

