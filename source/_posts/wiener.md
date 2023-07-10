---
title: Wiener-Khinchin theorem
date: 2024-07-18 20:29:38
tags:
categories:
- noise
mathjax: true
---



##  Energy signals vs Power signal

![image-20240427155046131](wiener/image-20240427155046131.png)

> ![image-20240719203550628](wiener/image-20240719203550628.png)



![image-20240427155100927](wiener/image-20240427155100927.png)

> ![image-20240719204148098](wiener/image-20240719204148098.png)



## Ergodicity & autocorrelation

The most important statistical properties of a random process $x(t)$ are obtained by applying the *expectation operator* to some functions of the process itself

- The **expectation** returns the probability-weighted average of the specific function at that specific time
  over all possible realizations of the process

> In many real practical cases, though, data from many realizations of the process are not available. On the contrary, often only data from one of them are known



***ensemble autocorrelation*** and ***temporal autocorrelation (time autocorrelation)*** 

![image-20240719230346944](wiener/image-20240719230346944.png)

> ![image-20240719210621021](wiener/image-20240719210621021.png)![image-20240720140527704](wiener/image-20240720140527704.png)







## Wiener-Khinchin theorem

> Norbert Wiener proved this theorem for the case of a *deterministic function* in 1930; Aleksandr Khinchin later formulated an analogous result for *stationary stochastic processes* and published that probabilistic analogue in 1934. Albert Einstein explained, without proofs, the idea in a brief two-page memo in 1914

$x(t)$, Fourier transform over a limited period of time $[-T/2, +T/2]$ , $X_T(f) = \int_{-T/2}^{T/2}x(t)e^{-j2\pi ft}dt$


With *Parseval's theorem*
$$
\int_{-T/2}^{T/2}|x(t)|^2dt = \int_{-\infty}^{\infty}|X_T(f)|^2df
$$
So that
$$
\frac{1}{T}\int_{-T/2}^{T/2}|x(t)|^2dt = \int_{-\infty}^{\infty}\frac{1}{T}|X_T(f)|^2df
$$

> where the quantity, $\frac{1}{T}|X_T(f)|^2$ can be interpreted as distribution of power in the frequency domain
>
> For each $f$ this quantity is a random variable, since it is a function of the random process $x(t)$



The power spectral density (PSD) $S_x(f )$ is defined as the limit of the expectation of the expression
above, for large $T$:
$$
S_x(f) = \lim _{T\to \infty}\mathrm{E}\left[ \frac{1}{T}|X_T(f)|^2 \right]
$$

The *Wiener-Khinchin theorem* ensures that for well-behaved *wide-sense stationary processes* the **limit exists** and is equal to the Fourier transform of the autocorrelation
$$\begin{align}
S_x(f) &= \int_{-\infty}^{+\infty}R_x(\tau)e^{-j2\pi f \tau}d\tau \\
R_x(\tau) &= \int_{-\infty}^{+\infty}S_x(f)e^{j2\pi f \tau}df
\end{align}$$



## Example

A pure sine wave is expressed as $y(t) = A_0 \sin(2\pi f_0 t +\phi _0)$, its autocorrelation function:

$$
\mathrm{R}(\tau) = \lim _{T\to \infty}\frac{1}{2T}\int_{-T}^{T} y(t)y(t+\tau)dt
$$

where $y(t)y(t+\tau)$ can be expressed as
$$\begin{align}
y(t)y(t+\tau) &= A_0\sin(2\pi f_0 t+\phi_0)\cdot A_0\sin(2\pi f_0 t+\phi_0+2\pi f_0\tau) \\
&= A_0^2\sin^2(2\pi f_0 t+\phi_0)\cdot \cos(2\pi f_0\tau) + A_0^2\sin(2\pi f_0 t+\phi_0)\cos(2\pi f_0 t+\phi_0)\cdot \cos(2\pi f_0\tau) \\
&= \frac{1}{2}A_0^2 (1 - \cos(2(2\pi f_0 t+\phi_0)))\cdot \cos(2\pi f_0\tau) + \frac{1}{2}A_0^2\sin(2(2\pi f_0 t+\phi_0))\cdot \cos(2\pi f_0\tau) \\
&= \frac{1}{2}A_0^2\cdot \cos(2\pi f_0\tau) - \frac{1}{2}A_0^2\cos(2(2\pi f_0 t+\phi_0))\cdot \cos(2\pi f_0\tau) + \frac{1}{2}A_0^2\sin(2(2\pi f_0 t+\phi_0))\cdot \cos(2\pi f_0\tau)
\end{align}$$

And substitute $y(t)y(t+\tau)$ in $\mathrm{R}(\tau)$

$$\begin{align}
\mathrm{R}(\tau) &= \lim _{T\to \infty}\frac{1}{2T}\int_{-T}^{T} y(t)y(t+\tau)dt \\
&= \lim _{T\to \infty}\int_{-T}^{T} \left[\frac{1}{2}A_0^2\cdot \cos(2\pi f_0\tau) - \frac{1}{2}A_0^2\cos(2(2\pi f_0 t+\phi_0))\cdot \cos(2\pi f_0\tau) + \frac{1}{2}A_0^2\sin(2(2\pi f_0 t+\phi_0))\cdot \cos(2\pi f_0\tau)\right]dt \\
& = \lim _{T\to \infty}\int_{-T}^{T} \frac{1}{2}A_0^2\cdot \cos(2\pi f_0\tau) dt \\
&= \frac{1}{2}A_0^2\cdot \cos(2\pi f_0\tau)
\end{align}$$

Taking Fourier transform of $\mathrm{R}(\tau)$, PSD is

$$
S_y(f) = \frac{1}{4}A_0^2 \delta(f-f_0) + \frac{1}{4}A_0^2 \delta(f+f_0)
$$

> Remeber
>
> ![image-20240718210137344](wiener/image-20240718210137344.png)
> $$
> \cos(2\pi f_0t) \overset{\mathcal{F}}{\longrightarrow} \frac{1}{2}[\delta(f -f_0)+\delta(f+f_0)]
> $$





## reference

Topic 5 Energy & Power Signals, Correlation & Spectral Density [[https://www.robots.ox.ac.uk/~dwm/Courses/2TF_2021/N5.pdf](https://www.robots.ox.ac.uk/~dwm/Courses/2TF_2021/N5.pdf)]

Topic 6 Random Processes and Signals [[https://www.robots.ox.ac.uk/~dwm/Courses/2TF_2021/N6.pdf](https://www.robots.ox.ac.uk/~dwm/Courses/2TF_2021/N6.pdf)]


Bae, Woorham; Jeong, Deog-Kyoon: 'Analysis and Design of CMOS Clocking Circuits for Low Phase Noise' (Materials, Circuits and Devices, 2020)
