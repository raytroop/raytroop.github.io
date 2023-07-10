---
title: Multirate Filter 
date: 2024-09-22 14:23:43
tags:
categories:
- dsp
mathjax: true
---

![image-20241019142915175](multirate/image-20241019142915175.png)



## Multirate Signal Processing

alternative view of sampling, assuming DC value is $A$

![sampling-c2d-d2d.drawio](multirate/sampling-c2d-d2d.drawio.svg)

- $x_c(t)$ and $x_s(t)$

  $\overline{x_c} = A$; $\overline{x_s}=\frac{A}{T}$: therefore $X_s(j0) = \frac{1}{T}X_c(j0)$



- $x[n]$ and $x_d[n]$

  $\overline{x} = A$; $\overline{x_d}=\frac{A}{2}$: therefore $X_d(e^{j0}) = \frac{1}{2}X(e^{j0})$



***expander***

![sampling-expander.drawio](multirate/sampling-expander.drawio.svg)



- $x[n]$ and $x_e[n]$

  $\overline{x} = A$; $\overline{x_e}=A$: therefore $X_e(e^{j0}) = X(e^{j0})$

  > Fourier transform of the output of the expander is a frequency-scaled version of the Fourier transform of the input





---



### downsampling

![image-20241004151215993](multirate/image-20241004151215993.png)

![image-20241004151308422](multirate/image-20241004151308422.png)

![image-20241004151434477](multirate/image-20241004151434477.png)

- Eqs. (4.72)

  the superposition of an infinite set of amplitude-scaled copies of $X_c(j\Omega)$, frequency scaled through $\omega = \Omega T_d$ and shifted by integer multiples of $2\pi$

- Eq. (4.77)

  the superposition of $M$ amplitude-scaled copies of the periodic Fourier transform $X (e^{j\omega})$, frequency scaled by $M$ and shifted by integer multiples of $2\pi$ 





---

downsampled by a factor of $M = 2$

![image-20241004161805974](multirate/image-20241004161805974.png)



---

![image-20241005073349726](multirate/image-20241005073349726.png)

![image-20241005073534041](multirate/image-20241005073534041.png)



---



### upsampling

![image-20241006074604512](multirate/image-20241006074604512.png)

![image-20241006072426572](multirate/image-20241006072426572.png)


![image-20241006074425704](multirate/image-20241006074425704.png)

![image-20241006075854246](multirate/image-20241006075854246.png)



> Balu Santhanam, Probability Theory & Stochastic Process 2020: Random Signals & Multirate Systems [[https://ece-research.unm.edu/bsanthan/ece541/rand.pdf](https://ece-research.unm.edu/bsanthan/ece541/rand.pdf)]



### sampling identities

![sampling-ID.drawio](multirate/sampling-ID.drawio.svg)



---



#### downsampling identity 

![image-20241007085509889](multirate/image-20241007085509889.png)






![image-20241007090624888](multirate/image-20241007090624888.png)



---



#### upsampling identity

![image-20241007085527233](multirate/image-20241007085527233.png)




![image-20241007090939701](multirate/image-20241007090939701.png)



### Polyphase Decomposition

![image-20241020122709610](multirate/image-20241020122709610.png)

![image-20241020122726153](multirate/image-20241020122726153.png)

where $e_k[n]=h[nM+k]$

---

***Polyphase Implementation of Decimation Filters & Interpolation Filters***

|                       | Decimation system                                            | Interpolation system                                         |
| --------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
|                       | ![image-20241020123035001](multirate/image-20241020123035001.png) | ![image-20241020123043829](multirate/image-20241020123043829.png) |
|                       | ![image-20241020123027067](multirate/image-20241020123027067.png) | ![image-20241020123101780](multirate/image-20241020123101780.png) |
| **sampling identity** | ![image-20241020123345371](multirate/image-20241020123345371.png) | ![image-20241020123355113](multirate/image-20241020123355113.png) |



### LPTV Implementation

*TODO* &#128197;

The **interpolation filter** following an up-sampler generally is **time varying** and cannot be represented
by a simple transfer function. The equivalent filter in a **zero-order hold** is an exception, perhaps unique, that can be represented with a time-invariant transfer function



> Dr. Deepa Kundur, Multirate Digital Signal Processing: Part I [[pdf](https://www.comm.utoronto.ca/dkundur/course_info/discrete-time-systems/notes/Kundur_DTS_Chap11a.pdf), [https://www.comm.utoronto.ca/dkundur/course/discrete-time-systems/](https://www.comm.utoronto.ca/dkundur/course/discrete-time-systems/)]

## Decimation

![image-20241020140430663](multirate/image-20241020140430663.png)

DLF's input bit-width can be reduced by *decimating* BBPD's output. Decimation is typically performed by realizing either **majority voting (MV)** or **boxcar filtering**.

> Note that **deserialization** is inherent to both **MV** and **boxcar** filtering

![image-20241019225016868](multirate/image-20241019225016868.png)

- Decimation is commonly employed to alleviate the high-speed requirement. However, decimation increases loop-latency which causes excessive dither jitter.
- Decimation is basically, widen the data and slowing it down
- Decimating by $L$ means frequency register only added once every $L$ UI, thus *integral path gain* reduced by $L$ in linear model
- *proportional path gain* is unchanged

![intg_path_decim.drawio](multirate/intg_path_decim.drawio.svg)


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



## Zero-Order Hold (ZOH) interpolator

![zoh.drawio](multirate/zoh.drawio.svg)
$$
F_1(z) = X(z^{LM})\frac{1-z^{-LM}}{1-z^{-1}}
$$


Split the $1:LM$ hold process into a $1 : L$ hold followed by a $1 : M$ hold
$$
Y(\eta)=X(\eta^{L})\frac{1-\eta^{-L}}{1-\eta^{-1}}
$$
then
$$\begin{align}
F_2(z) &= Y(z^M)\cdot\frac{1-z^{-M}}{1-z^{-1}} \\
&=X(z^{LM})\frac{1-z^{-LM}}{1-z^{-M}}\cdot \frac{1-z^{-M}}{1-z^{-1}} \\
&= X(z^{LM})\frac{1-z^{-LM}}{1-z^{-1}}
\end{align}$$

That is $F_1(z)=F_2(z)$, i.e. they are equivalent




## reference

Alan V Oppenheim, Ronald W. Schafer. 2010. Discrete-Time Signal Processing, 3rd edition

R. E. Crochiere and L. R. Rabiner, "Multirate Digital Signal Processing", Prentice Hall, 1983.

John G. Proakis and Dimitris G. Manolakis, Digital Signal Processing: Principles, Algorithms, and Applications, 4th edition, 2007.

D. Sundararajan. 2024. Digital Signal Processing: An Introduction 2nd Edition

F. M. Gardner, "Phaselock Techniques", 3rd Edition, Wiley Interscience, Hoboken, NJ, 2005 [[https://picture.iczhiku.com/resource/eetop/WyIgwGtkDSWGSxnm.pdf](https://picture.iczhiku.com/resource/eetop/WyIgwGtkDSWGSxnm.pdf)]

Rhee, W. (2020). *Phase-locked frequency generation and clocking : architectures and circuits for modern wireless and wireline systems*. The Institution of Engineering and Technology
