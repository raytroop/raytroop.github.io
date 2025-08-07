---
title: Clocking
date: 2024-05-11 09:36:14
tags:
categories:
- analog
mathjax: true
---

## excess phase around n-th harmonic

![image-20250523222041505](clocking/image-20250523222041505.png)


> $\Delta t$ is same for any n-th harmonic



## Spurious Tones

![image-20250523222846691](clocking/image-20250523222846691.png)



> Nicola Da Dalt, ISSCC 2012: Jitter Basic and Advanced Concepts, Statistics and Applications [[https://www.nishanchettri.com/isscc-slides/2012%20ISSCC/TUTORIALS/ISSCC2012Visuals-T5.pdf](https://www.nishanchettri.com/isscc-slides/2012%20ISSCC/TUTORIALS/ISSCC2012Visuals-T5.pdf)]

---

![image-20250529220609357](clocking/image-20250529220609357.png)



> P.E. Allen - 2003 ECE 6440 - Frequency Synthesizers: Lecture 150 – Phase Noise-I [[https://pallen.ece.gatech.edu/Academic/ECE_6440/Summer_2003/L150-PhaseNoise-I(2UP).pdf](https://pallen.ece.gatech.edu/Academic/ECE_6440/Summer_2003/L150-PhaseNoise-I(2UP).pdf)]



## Reference Spur

**spurs** are carrier or clock frequency spectral imperfections measured in the frequency domain just like phase noise. However, unlike phase noise they are *discrete* frequency components.

- Spurs are deterministic

- Spur power is independent of bandwidth

- Spurs contribute bounded peak jitter in the time domain



***Sources of Spurs:***

- External (coupling from other noisy block)
  Supply, substrate, bond wires, etc.
- Internal (int-N/fractional-N operation)
  - **Frac spur**: Fractional divider (multi-modulus and frequency accumulation)
  - **Ref. spur**: PFD/charge pump/analog loop filter non-idealities, clock coupling





## Fractional Spur

*TODO* &#128197;





## cycle slip

*TODO* &#128197;





##  frequency divider & phase margin

 **type-I PLLs**

![image-20241222152826102](clocking/image-20241222152826102.png)

![image-20241222152916367](clocking/image-20241222152916367.png)

 frequency divider weakens the feedback and ***increases** the phase margin*



---

**type-II PLLs**

![image-20241222153430163](clocking/image-20241222153430163.png)

 frequency divider weakens the feedback and ***decrease** the phase margin*



## multi-modulus divider

*TODO* &#128197;





##  Fractional-N

1. ***Dither Feedback Divider Ratio by a delta-sigma modulator***

![image-20241003105023092](clocking/image-20241003105023092.png)

2. ***Frequency Accumulation***

![image-20241003105059989](clocking/image-20241003105059989.png)



## Switched Capacitor Banks

Q: why $R_b$ ?

A:  *TODO* &#128197;



![image-20240901105919333](clocking/image-20240901105919333.png)



> Hu, Yizhe. "Flicker noise upconversion and reduction mechanisms in RF/millimeter-wave oscillators for 5G communications." PhD diss., 2019.
>
> S. D. Toso, A. Bevilacqua, A. Gerosa and A. Neviani, "A thorough analysis of the tank quality factor in LC oscillators with switched capacitor banks," *Proceedings of 2010 IEEE International Symposium on Circuits and Systems*, Paris, France, 2010, pp. 1903-1906



## SSC intuition

Due to $f= K_{vco}V_{ctrl}$, its derivate to $t$ is

$$
\frac{df}{dt} = K_{vco}\frac{dV_{ctrl}}{dt}
$$

For chargepump PLL, $dV_{ctrl} = \frac{\phi_e I_{cp}}{2\pi C}dt$, that is
$$
\frac{df}{dt} = K_{vco}  \frac{\phi_e I_{cp}}{2\pi C}
$$





## Phase Interpolator (PI)

!!! Clock Edges

And for a phase interpolator, you need those reference clocks to be completely the opposite. Ideally they would be **triangular** shaped

![image-20240821203756602](clocking/image-20240821203756602.png)

> *four input clocks given by the cyan, black, magenta, red* 




> John T. Stonick, ISSCC 2011 tutorial. "DPLL Based Clock and Data Recovery" [[https://www.nishanchettri.com/isscc-slides/2011%20ISSCC/TUTORIALS/ISSCC2011Visuals-T5.pdf](https://www.nishanchettri.com/isscc-slides/2011%20ISSCC/TUTORIALS/ISSCC2011Visuals-T5.pdf)]



***kink problem***

![image-20240919223032380](clocking/image-20240919223032380.png)

> B. Razavi, **"The Design of a Phase Interpolator [The Analog Mind],"** IEEE Solid-State Circuits Magazine, Volume. 15, Issue. 4, pp. 6-10, Fall 2023.([https://www.seas.ucla.edu/brweb/papers/Journals/BR_SSCM_4_2023.pdf](https://www.seas.ucla.edu/brweb/papers/Journals/BR_SSCM_4_2023.pdf))





## DIV 1.5

*TODO* &#128197;

> Xu, Haojie & Luo, Bao & Jin, Gaofeng & Feng, Fei & Guo, Huanan & Gao, Xiang & Deo, Anupama. (2022). A Flexible 0.73-15.5 GHz Single LC VCO Clock Generator in 12 nm CMOS. IEEE Transactions on Circuits and Systems II: Express Briefs. 69. 4238 - 4242. [[https://www.researchgate.net/publication/382240520_A_Flexible_073-155_GHz_Single_LC_VCO_Clock_Generator_in_12_nm_CMOS](https://www.researchgate.net/publication/382240520_A_Flexible_073-155_GHz_Single_LC_VCO_Clock_Generator_in_12_nm_CMOS)]





## False locking

*TODO* &#128197;

- divider failure
- even-stage ring oscillator ( multipath ring oscillators)
- DLL: harmonic locking,  stuck locking






## clock edge impact

![clock2clock.drawio](clocking/clock2clock.drawio.svg)

> ck1 is div2 of ck0

- edge of ck0 is affected differently by ck1

- edge of ck1 is affected equally by ck0





## Feedback Dividers

![image-20240803225130324](clocking/image-20240803225130324.png)

- Large values of N lowers the loop BW which is bad for jitter





> Gunnman, Kiran, and Mohammad Vahidfar. *Selected Topics in RF, Analog and Mixed Signal Circuits and Systems*. Aalborg: River Publishers, 2017.





## clock gating

![clk_mux.drawio](clocking/clk_mux.drawio.svg)





## Why Type 2 PLL ?

> **Type**: # of integrators within the loop
>
> **Order**: # of poles in the *closed-loop* transfer function 
>
> *Type $\leq$ Order*



1. That is, to have a wide bandwidth, a high loop gain is required
2. More importantly, the type 1 PLL has the problem of a ***static phase error*** for the change of an input frequency

---

*Type 1 PLL with input phase step* $\Delta \phi \cdot u(t)$
$$\begin{align}
\Delta \phi\cdot u(t) - K\int_0^{t}\phi _e (\tau)d\tau &= \phi _e (t) \\
\phi _e (0) &= \Delta \phi
\end{align}$$

we obtain $\phi _e (t) = \Delta \phi \cdot e^{-Kt}\cdot u(t)$

and $\phi _e(\infty) = 0$

---





## Divider phase noise & jitter

![image-20241013212542173](clocking/image-20241013212542173.png)

- Multiplying the frequency of a signal by a factor of N using an **ideal** frequency multiplier increases the phase noise of the multiplied signal by $20\log(N)$ dB. 
- Similarly dividing a signal frequency by N reduces the phase noise of the output signal by $20\log(N)$  dB

> The sideband offset from the carrier in the frequency multiplied/divided signal is the same as for the original signal.



### The 20log(N) Rule

If the carrier frequency of a clock is divided down by a factor of $N$ then we expect the phase noise to decrease by $20\log(N)$.The primary assumption here is a *noiseless* conventional digital divider.

> The $20\log(N)$ rule only applies to *phase noise* and *not integrated phase noise or phase jitter*. Phase jitter should generally measure about the **same**.



![20log(N).png](clocking/rtaImage-1720945161770-5.png)

### What About Phase Jitter?

We integrate *SSB* phase noise *L*(f) [dBc/Hz] to obtain rms phase jitter in seconds as follows for “brick wall” integration from f1 to f2 offset frequencies in Hz and where f0 is the carrier or clock frequency.

![phase jitter.png](clocking/rtaImage.png)

Note that the rms phase jitter in seconds is inversely proportional to f0. When frequency is divided down, the phase noise, *L*(f), goes down by a factor of 20log(N). However, since the frequency goes down by N also, the phase jitter expressed in units of time is constant. 

Therefore, phase noise curves, related by 20log(N), with the same phase noise shape over the *jitter bandwidth*, are expected to yield the same phase jitter in seconds.



> [[Timing 101: The Case of the Jitterier Divided-Down Clock, Silicon Labs]](https://community.silabs.com/s/share/a5U1M000000knweUAA/timing-101-the-case-of-the-jitterier-divideddown-clock?language=en_US)
>
> [[How division impacts spurs, phase noise, and phase]](https://www.planetanalog.com/how-division-impacts-spurs-phase-noise-and-phase/)
>
> [[Phase Noise Theory: Ideal Frequency Multipliers and Dividers]](http://www.ko4bb.com/~bruce/IdealFreqMultDiv.html)



## PLL bandwidth test

A *step response test* is an easy way to determine the bandwidth.

*Sum a small step into the control voltage* of your oscillator (VCO or NCO), and measure the *90% to 10%* fall time of the corrected response at the output of the loop filter as shown in this block diagram

![PLL Step Response Test](clocking/loVQR.png)

a first order loop 
$$
BW = \frac{0.35}{t} \space\space\space\space \text{(first order system)}
$$
Where $BW$ is the 3 dB bandwidth in Hz and $𝑡$​ is the 10%/90% rise or fall time.



For second order loops with a typical damping factor of *0.7* this relationship is closer to:
$$
BW = \frac{0.33}{t}\space\space\space\space \text{(second order system, damping factor = 0.7)}
$$

> [How can I experimentally find the bandwidth of my PLL?, [https://dsp.stackexchange.com/a/73654/59253](https://dsp.stackexchange.com/a/73654/59253)]





## reference

Dennis Fischette, Frequently Asked PLL Questions [[https://www.delroy.com/PLL_dir/FAQ/FAQ.htm](https://www.delroy.com/PLL_dir/FAQ/FAQ.htm)]

Ian Galton, ISSCC 2010 SC3: Fractional-N PLLs [[https://www.nishanchettri.com/isscc-slides/2010%20ISSCC/Short%20Course/SC3.pdf](https://www.nishanchettri.com/isscc-slides/2010%20ISSCC/Short%20Course/SC3.pdf)]

Mike Shuo-Wei Chen, ISSCC 2020 T6: Digital Fractional-N Phase Locked Loop Design [[https://www.nishanchettri.com/isscc-slides/2020%20ISSCC/TUTORIALS/T6Visuals.pdf](https://www.nishanchettri.com/isscc-slides/2020%20ISSCC/TUTORIALS/T6Visuals.pdf)]
