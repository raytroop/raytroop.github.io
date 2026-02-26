---
title: VLSI Digital Signal Processing 
date: 2025-11-11 07:29:09
tags:
categories:
- link
mathjax: true
---



## Number Systems

> Harris, David Money, and Sarah L. Harris. *Digital Design and Computer Architecture*. 2nd ed. Morgan Kaufmann, 2013. [[pdf](https://github.com/last-genius/comp_arch_list/blob/master/books/Digital%20Design%20and%20Computer%20Architecture.%20ARM%20Edition%20by%20Sarah%20Harris%2C%20David%20Harris.pdf)]

***integers***

![image-20260207093700537](vlsi-dsp/image-20260207093700537.png)

***rational number***

![image-20260207094834081](vlsi-dsp/image-20260207094834081.png)

![image-20260206230528138](vlsi-dsp/image-20260206230528138.png)


### 2's Complement

> [[https://bpb-us-w2.wpmucdn.com/sites.coecis.cornell.edu/dist/4/81/files/2019/06/4740_lecture23ALU-circuits.pdf](https://bpb-us-w2.wpmucdn.com/sites.coecis.cornell.edu/dist/4/81/files/2019/06/4740_lecture23ALU-circuits.pdf)]

![image-20260207085804825](vlsi-dsp/image-20260207085804825.png)

> Google AI Mode [[https://share.google/aimode/KsxxgDF0vAdhAIgm0](https://share.google/aimode/KsxxgDF0vAdhAIgm0)]

![image-20260207094125000](vlsi-dsp/image-20260207094125000.png)

### Fixed Point Number

![image-20260207095601437](vlsi-dsp/image-20260207095601437.png)




### Floating Point Number

> Dennis Forbes. Understanding Floating-Point Numbers [[https://dennisforbes.ca/blog/features/floating_point/understanding-floating-point-numbers/](https://dennisforbes.ca/blog/features/floating_point/understanding-floating-point-numbers/)]
>
> IEEE Standard for Floating-Point Arithmetic [[https://www-users.cse.umn.edu/~vinals/tspot_files/phys4041/2020/IEEE%20Standard%20754-2019.pdf](https://www-users.cse.umn.edu/~vinals/tspot_files/phys4041/2020/IEEE%20Standard%20754-2019.pdf)]

![image-20260207101850895](vlsi-dsp/image-20260207101850895.png)

![image-20260207104005414](vlsi-dsp/image-20260207104005414.png)

|                                      |                                |                                                              |
| ------------------------------------ | ------------------------------ | ------------------------------------------------------------ |
| **32-bit floating-point version 1**  | store *implicit leading one*   | ![image-20260207102121844](vlsi-dsp/image-20260207102121844.png) |
| **32-bit floating-point version 2**  | discard *implicit leading one* | ![image-20260207102147689](vlsi-dsp/image-20260207102147689.png) |
| **IEEE 754 floating point notation** | *biased exponent*              | ![image-20260207102210468](vlsi-dsp/image-20260207102210468.png) |

> [[https://share.google/aimode/yY2R2EQCTsP9BlMNx](https://share.google/aimode/yY2R2EQCTsP9BlMNx)]

| Format                        | Exponent Bits | Bias (Decimal) | Representable Range |
| ----------------------------- | ------------- | -------------- | ------------------- |
| **Single Precision (32-bit)** | 8             | **127**        | -126 to +127        |
| **Double Precision (64-bit)** | 11            | **1023**       | -1022 to +1023      |

![image-20260207103557952](vlsi-dsp/image-20260207103557952.png)





## VLSI Arithmetic

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

![image-20250907163030510](vlsi-dsp/image-20250907163030510.png)

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




## Discrete-Time Integrators

> Qasim Chaudhari. Discrete-Time Integrators [[https://wirelesspi.com/discrete-time-integrators/](https://wirelesspi.com/discrete-time-integrators/)]
>
> David Johns (University of Toronto) "Oversampled Data Converters" Course (2019) [[https://youtu.be/qIJ2LORYmyA](https://youtu.be/qIJ2LORYmyA)]

Delaying Integrator

Delay-free Integrator

![image-20250615124417691](vlsi-dsp/image-20250615124417691.png)

## Discrete-Time Differentiator

> Qasim Chaudhari. Design of a Discrete-Time Differentiator [[https://wirelesspi.com/design-of-a-discrete-time-differentiator/](https://wirelesspi.com/design-of-a-discrete-time-differentiator/)]

*TODO* &#128197;



## Accumulate-and-dump (AAD) decimator

accumulating the input for $N$ cycles and then latching the result and resetting the integrator

![image-20241015222205883](vlsi-dsp/image-20241015222205883.png)

> It adds up $N$ succeeding input samples at rate $1/T$ and delivers their sum in a *single* sample at the output. Therefore, the process comprises a **filter (in the accumulation)** and a **down-sampler (in the dump)**



## Moving Average and CIC Filters

> An Intuitive Look at Moving Average and CIC Filters [[web](https://tomverbeure.github.io/2020/09/30/Moving-Average-and-CIC-Filters.html), [code](https://github.com/tomverbeure/pdm/tree/master/modeling/cic_filters)]
>
> A Beginner's Guide To Cascaded Integrator-Comb (CIC) Filters [[https://www.dsprelated.com/showarticle/1337.php](https://www.dsprelated.com/showarticle/1337.php)]



*TODO* &#128197;



## Cascaded Integrator-Comb (CIC) filter

Let’s focus on decimation: if we decimate by a factor 4, we simply retain one output sample out of every 4 input samples.

In the example below, the downsampler at the right drops those 3 samples out of 4, and the output rate, $y^\prime(n)$, is one fourth of the input rate $x(n)$:

![moving_average_filters-decimation_trivial](vlsi-dsp/moving_average_filters-decimation_trivial.svg)
$$\begin{align}
Y(z) &= X(z)\frac{1-z^{-4}}{1-z^{-1}} \\
Y^\prime(\xi) &= \frac{1}{4}Y(\xi^{1/4}) = \frac{1}{4}X(\xi^{1/4})\frac{1-\xi^{-1}}{1-\xi^{-1/4}}
\end{align}$$

with $z=e^{j\Omega/f_s}$ and $\xi =z^4$, we have
$$
Y^\prime(z) = \frac{1}{4}X(z)\frac{1-z^{-4}}{1-z^{-1}}
$$

But if we're going to be throwing away 75% of the calculated values, can't we just move the downsampler from the end of the pipeline to somewhere in the middle? Right between the integrator stage and the comb stage? That answer is yes, but to keep the math working, ***we also need to divide the number of delay elements in the comb stage by the decimation rate***:

![moving_average_filters-decimation_smart](vlsi-dsp/moving_average_filters-decimation_smart.svg)

$$\begin{align}
A(z) &= X(z)\frac{1}{1-z^{-1}} \\
A^\prime(\xi) &= \frac{1}{4}A(\xi^{1/4}) = \frac{1}{4}X(\xi^{1/4})\frac{1}{1-\xi^{-1/4}} \\
Y^\prime(\xi) &= A^\prime(\xi) (1-\xi^{-1}) =  \frac{1}{4}X(\xi^{1/4})\frac{1-\xi^{-1}}{1-\xi^{-1/4}}
\end{align}$$

with $z=e^{j\Omega/f_s}$ and $\xi =z^4$, we have
$$
Y^\prime(z) = \frac{1}{4}X(z)\frac{1-z^{-4}}{1-z^{-1}}
$$

---

And we can do this just the same with cascaded sections (*without downsampler or updampler*) where *integrators and combs have been grouped*

- for **decimation**, the *integrators come first* and the *combs second* with the downsampler in between
- For **interpolation**, the reverse is true
  - the incoming sample rate is fraction of the outgoing sample rate, the combs must come first and the interpolators second

![moving_average_filters-integrator_comb_decimated](vlsi-dsp/moving_average_filters-integrator_comb_decimated.svg)





![moving_average_filters-comb_integrator_interpolated](vlsi-dsp/moving_average_filters-comb_integrator_interpolated.svg)







> Tom Verbeure. An Intuitive Look at Moving Average and CIC Filters [[https://tomverbeure.github.io/2020/09/30/Moving-Average-and-CIC-Filters.html](https://tomverbeure.github.io/2020/09/30/Moving-Average-and-CIC-Filters.html)]
>
> —. Half-Band Filters, a Workhorse of Decimation Filters [[https://tomverbeure.github.io/2020/12/15/Half-Band-Filters-A-Workhorse-of-Decimation-Filters.html](https://tomverbeure.github.io/2020/12/15/Half-Band-Filters-A-Workhorse-of-Decimation-Filters.html)]
>
> —. Design of a Multi-Stage PDM to PCM Decimation Pipeline [[https://tomverbeure.github.io/2020/12/20/Design-of-a-Multi-Stage-PDM-to-PCM-Decimation-Pipeline.html](https://tomverbeure.github.io/2020/12/20/Design-of-a-Multi-Stage-PDM-to-PCM-Decimation-Pipeline.html)]
>
> Arash Loloee, Ph.D. Exploring Decimation Filters [[https://www.highfrequencyelectronics.com/Archives/Nov13/1311_HFE_decimationFilters.pdf](https://www.highfrequencyelectronics.com/Archives/Nov13/1311_HFE_decimationFilters.pdf)]
>
> Rick Lyons. A Beginner's Guide To Cascaded Integrator-Comb (CIC) Filters [[https://www.dsprelated.com/showarticle/1337.php](https://www.dsprelated.com/showarticle/1337.php)]





## reference

Jabbour, Chadi, etc.. "Digitally enhanced mixed signal systems." *IEEE International Symposium on Circuits and Systems (ISCAS)*. 2019.

Sen M. Kuo. Real-Time Digital Signal Processing: Fundamentals, Implementations and Applications, 3rd Edition. John Wiley & Sons 2013

Taylor, Fred. *Digital filters: principles and applications with MATLAB*. John Wiley & Sons, 2011

Kuo, Sen-Maw. (2013) Real-Time Digital Signal Processing: Implementations and Applications 3rd [[pdf](http://dl.icdst.org/pdfs/files/e51100ce301ad56951e4511a9a1c66aa.pdf)]

D. Markovic and R. W. Brodersen, DSP Architecture Design Essentials, Springer, 2012.

---

Bevan Baas, EEC281 VLSI Digital Signal Processing,  [[https://www.ece.ucdavis.edu/~bbaas/281/](https://www.ece.ucdavis.edu/~bbaas/281/)]

Mark Horowitz. EE371: Advanced VLSI Circuit Design Spring 2006-2007 [[https://web.stanford.edu/class/archive/ee/ee371/ee371.1066/](https://web.stanford.edu/class/archive/ee/ee371/ee371.1066/)]

謝秉璇. 2019 積體電路設計導論 [[link](https://nthuee.org/archive//%E7%A9%8D%E9%AB%94%E9%9B%BB%E8%B7%AF%E8%A8%AD%E8%A8%88%E5%B0%8E%E8%AB%96/2019%E8%AC%9D%E7%A7%89%E7%92%87/)]

Tinoosh Mohsenin. CMPE 691: Digital Signal Processing Hardware Implementation [[https://userpages.cs.umbc.edu/tinoosh/cmpe691/](https://userpages.cs.umbc.edu/tinoosh/cmpe691/)]

Keshab K. Parhi [[http://www.ece.umn.edu/users/parhi/](http://www.ece.umn.edu/users/parhi/)]

---

Qasim Chaudhari. FIR vs IIR Filters – A Practical Comparison [[https://wirelesspi.com/fir-vs-iir-filters-a-practical-comparison/](https://wirelesspi.com/fir-vs-iir-filters-a-practical-comparison/)]

—. Finite Impulse Response (FIR) Filters [[https://wirelesspi.com/finite-impulse-response-fir-filters/](https://wirelesspi.com/finite-impulse-response-fir-filters/)]

—. Why FIR Filters have Linear Phase [[https://wirelesspi.com/why-fir-filters-have-linear-phase/](https://wirelesspi.com/why-fir-filters-have-linear-phase/)]

—. Moving Average Filter [[https://wirelesspi.com/moving-average-filter/](https://wirelesspi.com/moving-average-filter/)]

—. Cascaded Integrator Comb (CIC) Filters – A Staircase of DSP. [[https://wirelesspi.com/cascaded-integrator-comb-cic-filters-a-staircase-of-dsp/](https://wirelesspi.com/cascaded-integrator-comb-cic-filters-a-staircase-of-dsp/)]

---

Jason Sachs. Understanding and Preventing Overflow (I Had Too Much to Add Last Night) [[https://www.embeddedrelated.com/showarticle/532.php](https://www.embeddedrelated.com/showarticle/532.php)]

—. Round Round Get Around: Why Fixed-Point Right-Shifts Are Just Fine [[https://www.embeddedrelated.com/showarticle/1015.php](https://www.embeddedrelated.com/showarticle/1015.php)]

—. How to Build a Fixed-Point PI Controller That Just Works: Part I [[https://www.embeddedrelated.com/showarticle/121.php](https://www.embeddedrelated.com/showarticle/121.php)]

—. How to Build a Fixed-Point PI Controller That Just Works: Part II [[https://www.embeddedrelated.com/showarticle/123.php](https://www.embeddedrelated.com/showarticle/123.php)]

