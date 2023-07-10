---
title: Delta-Sigma Modulator
date: 2023-11-06 21:39:25
tags:
categories:
- analog
mathjax: true
---



## Oversampling

In the oversampling process, samples per second are more than what is required, according to Nyquist-Shannon criteria. Allowing more sample rates does not influence the signal power and total quantization noise power. Therefore, the SNR remains unchanged. 

The advantage of oversampling is that the quantization noises are spread over a larger frequency range. This reduces the quantization noise spectral density (the SNR over the frequency of interest is increased).

> Comparing normal sampling and oversampling, the quantization noise power is reduced by 3 dB for every doubling of oversampling ratio (OSR), where OSR is the ratio of sampling frequency to twice the frequency of the signal. 





## The Delta Modulator

(a) A delta modulator and (b) its simple implementation

![image-20230202224406667](delta-sigma/image-20230202224406667.png)

 The high loop gain ensures that $V_F \simeq V_{in}$

The principal difficulty with the delta modulator is that the output digital representation in fact contains only the **derivative of the input**, as can be seen by noting $V_F=\int D_{out}dt$, i.e.
$$
D_{out} = \frac{dV_F}{dt}
$$

- This differentiation alters the signal spectrum
- attenuates the low-frequency content of the signal
- and amplifies high-frequency noise

## Delta-Sigma modulators





##  Charge Balancing





## Decimation Filters

A simple time-domain analysis shows that a **sinc filter** is a suitable decimation filter for a first-order modulator. Such a filter has a rectangular impulse response, and can be implemented as a **counter**.





## reference

B. Razavi, "The Delta-Sigma Modulator [A Circuit for All Seasons]," IEEE Solid-State Circuits Magazine, Volume. 8, Issue. 20, pp. 10-15, Spring 2016.

Pavan, Shanthi, Richard Schreier, and Gabor Temes. (2016) 2016. Understanding Delta-Sigma Data Converters. 2nd ed. Wiley.

Richard Schreier (2022). Delta Sigma Toolbox (https://www.mathworks.com/matlabcentral/fileexchange/19-delta-sigma-toolbox), MATLAB Central File Exchange. Retrieved June 28, 2022.

Micheal, A., P., Pertijs., Johan, H., Huijsing., Pertijs., Johan, H., Huijsing. (2006). Precision Temperature Sensors in CMOS Technology.

Manolis Terrovitis and Ken Kundert. [Device noise simulation of delta-sigma modulators](https://designers-guide.org/analysis/delta-sigma.pdf) and associated Matlab scripts: [scripts.tar.gz](https://designers-guide.org/analysis/scripts.tar.gz), [scripts.zip](https://designers-guide.org/analysis/scripts.zip).

Oversampling and Noise Shaping in Delta-Sigma Modulation [[https://resources.system-analysis.cadence.com/blog/msa2021-oversampling-and-noise-shaping-in-delta-sigma-modulation](https://resources.system-analysis.cadence.com/blog/msa2021-oversampling-and-noise-shaping-in-delta-sigma-modulation)]

David A. Johns. ECE1371H - Advanced Analog Circuits - Spring 2014 [[https://www.eecg.toronto.edu/~johns/ece1371/ece1371.html](https://www.eecg.toronto.edu/~johns/ece1371/ece1371.html)]

R.S. Ashwin Kumar. EE698I: Mixed-signal IC design [[https://home.iitk.ac.in/~ashwinrs/2023_EE698I.html](https://home.iitk.ac.in/~ashwinrs/2023_EE698I.html)]

R.S. Ashwin Kumar. EE698W: Analog circuits for signal processing [[https://home.iitk.ac.in/~ashwinrs/2022_EE698W.html](https://home.iitk.ac.in/~ashwinrs/2022_EE698W.html)]

Vishal Saxena. ECE 697 Delta-Sigma Data Converter Design [[https://www.eecis.udel.edu/~vsaxena/courses/ece697A/s10/ECE697.htm](https://www.eecis.udel.edu/~vsaxena/courses/ece697A/s10/ECE697.htm)]

-, ECE 615 Mixed Signal IC Design Spring 2016, Boise State University [[https://www.eecis.udel.edu/~vsaxena/courses/ece615/s16/ECE615.htm](https://www.eecis.udel.edu/~vsaxena/courses/ece615/s16/ECE615.htm)]

Richard E. Schreier, ECE 1371 Advanced Analog Circuits Notes 2015 [[http://individual.utoronto.ca/schreier/ece1371-2015.html](http://individual.utoronto.ca/schreier/ece1371-2015.html)]

Dai, Getting Started With Delta-Sigma ADC Design [[https://everynanocounts.com/2022/06/02/getting-started-with-delta-sigma-adc-design/](https://everynanocounts.com/2022/06/02/getting-started-with-delta-sigma-adc-design/)]
