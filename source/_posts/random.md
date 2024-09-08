---
title: Random Process
date: 2023-11-10 13:26:31
tags:
categories:
- noise
mathjax: true
---



## Ergodicity & autocorrelation

The most important statistical properties of a random process $x(t)$ are obtained by applying the *expectation operator* to some functions of the process itself

- The **expectation** returns the probability-weighted average of the specific function at that specific time
  over all possible realizations of the process

> In many real practical cases, though, data from many realizations of the process are not available. On the contrary, often only data from one of them are known



***ensemble autocorrelation*** and ***temporal autocorrelation (time autocorrelation)*** 

![image-20240719230346944](random/image-20240719230346944.png)

> ![image-20240719210621021](random/image-20240719210621021.png)![image-20240720140527704](random/image-20240720140527704.png)





##  LTI Systems on WSS Processes

![image-20240827221945277](random/image-20240827221945277.png)

### output autocorrelation

**deterministic autocorrelation function**



![image-20240427170024123](random/image-20240427170024123.png)

![image-20240907211343832](random/image-20240907211343832.png)



> why $\overline{R}_{hh}(\tau)  \overset{\Delta}{=} h(\tau)*h(-\tau)$ is autocorrelation ?  the proof is as follows:
> 
> $$\begin{align}
>\overline{R}_{hh}(\tau) &= h(\tau)*h(-\tau) \\
> &= \int_{-\infty}^{\infty}h(x)h(-(\tau - x))dx \\
> &= \int_{-\infty}^{\infty}h(x)h(-\tau + x))dx \\
> &=\int_{-\infty}^{\infty}h(x+\tau)h(x))dx
> \end{align}$$

---



### output PSD

![image-20240827222224395](random/image-20240827222224395.png)

![image-20240827222235906](random/image-20240827222235906.png)





> Topic 6 Random Processes and Signals [[https://www.robots.ox.ac.uk/~dwm/Courses/2TF_2021/N6.pdf](https://www.robots.ox.ac.uk/~dwm/Courses/2TF_2021/N6.pdf)]
>
> Alan V. Oppenheim, Introduction To Communication, Control, And Signal Processing [[https://ocw.mit.edu/courses/6-011-introduction-to-communication-control-and-signal-processing-spring-2010/a6bddaee5966f6e73450e6fe79ab0566_MIT6_011S10_notes.pdf](https://ocw.mit.edu/courses/6-011-introduction-to-communication-control-and-signal-processing-spring-2010/a6bddaee5966f6e73450e6fe79ab0566_MIT6_011S10_notes.pdf)]
>



---

**Time Reversal**
$$
x(-t) \overset{FT}{\longrightarrow} X(-j\omega)
$$


 if $x(t)$ is *real*, then $X(j\omega)$​ has **conjugate symmetry**
$$
X(-j\omega) = X^*(j\omega)
$$



## Random Signals Sampling

> sampling autocorrelation sequence

![image-20240428162643394](random/image-20240428162643394.png)

![image-20240428162655969](random/image-20240428162655969.png)

![image-20240907220050543](random/image-20240907220050543.png)



> Alan V Oppenheim, Ronald W. Schafer. Discrete-Time Signal Processing, 3rd edition



---

> ![image-20240428161506523](random/image-20240428161506523.png)
>
> [[https://dsp.stackexchange.com/a/17348/59253](https://dsp.stackexchange.com/a/17348/59253)]



### Noise Aliasing

*apply aforegoing conclusion*



## The Periodogram

The periodogram is in fact the Fourier transform of the aperiodic correlation of the windowed data sequence

![image-20240907215822425](random/image-20240907215822425.png)

![image-20240907215957865](random/image-20240907215957865.png)

> ![image-20240907230715637](random/image-20240907230715637.png)
>
> ---
>
> Due to $\sum_{n=0}^{L-1}|w[n]|^2 = \frac{1}{L}\sum_{k=0}^{L-1}|W[k]|^2$​ 
> $$
> I(\omega) = \frac{|V(e^{j\omega})|^2}{LU} = \frac{L|V(e^{j\omega})|^2}{\sum_{k=0}^{L-1}|W[k]|^2}
> $$
> The unavoidable rectangular window sequence selects a *finite-length* segment ($L$ samples) for *infinite-length* sequence, that is $|X(\omega)|^2 L = I(\omega)$
> $$
> |X(\omega)|^2 = \frac{|V(e^{j\omega})|^2}{\sum_{k=0}^{L-1}|W[k]|^2}
> $$






## Wiener-Khinchin theorem

> Norbert Wiener proved this theorem for the case of a ***deterministic function*** in 1930; Aleksandr Khinchin later formulated an analogous result for ***stationary stochastic processes*** and published that probabilistic analogue in 1934. Albert Einstein explained, without proofs, the idea in a brief two-page memo in 1914

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

The *Wiener-Khinchin theorem* ensures that for well-behaved *wide-sense stationary processes* the **limit exists** and is equal to the *Fourier transform of the autocorrelation*
$$\begin{align}
S_x(f) &= \int_{-\infty}^{+\infty}R_x(\tau)e^{-j2\pi f \tau}d\tau \\
R_x(\tau) &= \int_{-\infty}^{+\infty}S_x(f)e^{j2\pi f \tau}df
\end{align}$$



> Note: $S_x(f)$ in *Hz*  and inverse Fourier Transform in *Hz* ($\frac{1}{2\pi}d\omega = df$)



---

**Example**

![image-20240904203802604](random/image-20240904203802604.png)




> Remember: impulse scaling
>
> ![image-20240718210137344](random/image-20240718210137344.png)
> $$
> \cos(2\pi f_0t) \overset{\mathcal{F}}{\longrightarrow} \frac{1}{2}[\delta(f -f_0)+\delta(f+f_0)]
> $$





## reference

L.W. Couch, Digital and Analog Communication Systems, 8th Edition, 2013

Alan V Oppenheim, George C. Verghese, Signals, Systems and Inference, 1st edition
