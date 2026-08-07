---
title: Jitter
date: 2023-09-16 23:48:05
tags:
categories:
- noise
mathjax: true
---

![image-20250816004521416](jitter/image-20250816004521416.png)



![image-20250816003816639](jitter/image-20250816003816639.png)

## Voltage to Excess Phase Transformations

### Excess phase as Random Noise

![image-20260609230802209](jitter/image-20260609230802209.png)

***excess phase around $n$-th harmonic***

![image-20260609222319329](jitter/image-20260609222319329.png)

![image-20250523222041505](jitter/image-20250523222041505.png)


> $\Delta t$ is same for any n-th harmonic

![image-20260609224913582](jitter/image-20260609224913582.png)

### Excess phase as deterministic periodic signal

> Nicola Da Dalt, ISSCC 2012: Jitter Basic and Advanced Concepts, Statistics and Applications
>
> C. Samori, "Tutorial: Understanding Phase Noise in LC VCOs," *2016 IEEE International Solid-State Circuits Conference (ISSCC)*, San Francisco, CA, USA, 2016

![image-20260621101558719](jitter/image-20260621101558719.png)

FM $\Delta \omega_0 \cos\omega_m t$ to PM $\frac{\Delta \omega_0}{\omega_m} \sin\omega_m t$ depend on FM modulation frequency $\omega_m$


![image-20260609231247931](jitter/image-20260609231247931.png)

![image-20260609231317481](jitter/image-20260609231317481.png)

> ***Jacobi-Anger expansions with Bessel functions***
>
> ![image-20260609233706065](jitter/image-20260609233706065.png)
>
> ***Bessel function***
>
> ![image-20260609233914850](jitter/image-20260609233914850.png)

---

Spurious Tones in Spectrum & ***S**pur-to-**C**arrier **R**atio* (**SCR**)



![image-20250523222846691](jitter/image-20250523222846691.png)


single tone PM $A\sin\omega_m t$ to DJ don't depend on PM modulation frequency $\omega_m$


---

![image-20250529220609357](jitter/image-20250529220609357.png)



> P.E. Allen - 2003 ECE 6440 - Frequency Synthesizers: Lecture 150 – Phase Noise-I [[https://pallen.ece.gatech.edu/Academic/ECE_6440/Summer_2003/L150-PhaseNoise-I(2UP).pdf](https://pallen.ece.gatech.edu/Academic/ECE_6440/Summer_2003/L150-PhaseNoise-I(2UP).pdf)]

---



![image-20251213182452985](jitter/image-20251213182452985.png)
$$
f = \frac{\mathrm{d}(\omega_0 t + A\sin\omega_mt)}{2\pi \mathrm{d}t}=\frac{\omega_0 + A\cdot 2\pi f_m \cos\omega_m t}{2\pi}
$$
therefore
$$
\Delta f_{pk} = Af_m
$$
and
$$
P_{spur} = 10\log\left(\frac{\Delta f_{pk}}{2f_m}\right)^2= 10\log\left(\frac{A}{2}\right)^2
$$





## Phase Noise to Jitter

> Note that $L(f )$ is defined over positive frequencies only $(f \ge 0)$

![image-20250902231037546](jitter/image-20250902231037546.png)



---

![image-20250901224816795](jitter/image-20250901224816795.png)
$$\begin{align}
S_{jACC(N)}(f) &= |1-z^{-N}|^2\cdot S_{jABS}(f) \\
&= |1-\cos\theta +j\sin\theta|^2\cdot S_{jABS}(f) = ((1-\cos\theta)^2 + \sin^2\theta)\cdot S_{jABS}(f) \\
&= 2(1-\cos\theta)\cdot S_{jABS}(f) = 4\sin^2(\theta/2)\cdot S_{jABS}(f)
\end{align}$$

where $\theta = 2\pi f N/f_0$

![image-20250901233055582](jitter/image-20250901233055582.png)


As EQ(3.44), EQ(3.45)

the autocorrelation is the inverse Fourier transform of the PSD

$$
R_{\varphi}(t) = \int_{-\infty}^{+\infty} S_{\varphi} (f) e^{j2\pi f t}df
$$

Then,
$$
R_{\varphi}(0) = \int_{-\infty}^{+\infty} S_{\varphi} (f)  df \qquad R_{\varphi}(NT_0) = \int_{-\infty}^{+\infty} S_{\varphi} (f)   e^{j2\pi f NT_0} df
$$
Thus, yield EQ(3.48)

![image-20250903184827248](jitter/image-20250903184827248.png)



---

***Simplified PLL Phase Noise Profile***



***Absolute Jitter***

*TODO* &#128197;



 ***Period Jitter***

![image-20251218232426501](jitter/image-20251218232426501.png)

---

Given Simple PLL $\frac{\mathcal{L}_0}{1 + (f / f_{3dB})^2}$ and $\sigma_{p(N)}^2=\frac{\mathcal{L}_0 f_{3dB}}{2\pi f_0^2} \left(1 - \exp\left(-2\pi f_{3dB} N / f_0\right)\right)$

|           | $1 - \exp\left(-2\pi f_{3dB} N / f_0\right)$ | $\sigma_{\mathbf{p}(N)}^2$                     |
| --------- | -------------------------------------------- | ---------------------------------------------- |
| small $N$ | $\frac{2\pi f_{3dB} N} {f_0}$                | $\sigma_{PER}^2\cdot N$                        |
| large $N$ | $1$                                          | $\sigma_{PER}^2\cdot \frac{f_0}{2\pi f_{3dB}}$ |

where $\sigma_{\mathbf{p}}^2 = \frac{\mathcal{L}_0 f_{3dB}^2}{f_0^3}$



![image-20250901233626772](jitter/image-20250901233626772.png)

![image-20250901233756765](jitter/image-20250901233756765.png)

---

**a random-walk DCO - $1/f^2$ Phase Noise Profile**

> L. Avallone, M. Mercandelli, A. Santiccioli, M. P. Kennedy, S. Levantino and C. Samori, "A Comprehensive Phase Noise Analysis of Bang-Bang Digital PLLs," in IEEE Transactions on Circuits and Systems I: Regular Papers, vol. 68, no. 7, pp. 2775-2786, July 2021 [[https://sci-hub.st/10.1109/TCSI.2021.3072344](https://sci-hub.st/10.1109/TCSI.2021.3072344)]

![image-20250902232230515](jitter/image-20250902232230515.png)

> ![image-20250902231843251](jitter/image-20250902231843251.png)

---

> Mozhgan Mansuri “Low-Power Low-Jitter On-Chip Clock Generation” thesis UCLA [[https://people.engr.tamu.edu/spalermo/ecen689/pll_thesis_mansuri_ucla_2003.pdf](https://people.engr.tamu.edu/spalermo/ecen689/pll_thesis_mansuri_ucla_2003.pdf)]
>
> [[https://people.engr.tamu.edu/spalermo/ecen689/PRBS_&_PLL_model.pdf](https://people.engr.tamu.edu/spalermo/ecen689/PRBS_&_PLL_model.pdf)]

![image-20251218222327126](jitter/image-20251218222327126.png)

## Intersymbol interference (ISI)

![image-20260208094957058](jitter/image-20260208094957058.png)



![image-20260208095030679](jitter/image-20260208095030679.png)

![image-20260208095050799](jitter/image-20260208095050799.png)

> ![image-20260208095210726](jitter/image-20260208095210726.png)

$$
\color{red}\phi = 2\pi D \cdot f
$$



![image-20260208100834849](jitter/image-20260208100834849.png)





## Even-odd Jitter (EOJ)

| Jitter measurement | Description                                                  |
| :----------------- | :----------------------------------------------------------- |
| F/2                | F/2 is the peak-to-peak amplitude of the periodic jitter occurring at 1/2 of the data rate. |

**Even-odd jitter**, also known as **F/2 jitter**, arises from a clock signal's duty cycle not being perfectly 50%

![image-20250816130508935](jitter/image-20250816130508935.png)

> ***Even-odd jitter*** has been referred to as ***duty cycle distortion*** by other Physical Layer specifications for operation over electrical backplane or twinaxial copper cable assemblies



![image-20250816130650378](jitter/image-20250816130650378.png)

---

![image-20250816181004878](jitter/image-20250816181004878.png)

> Comparing DCD and F/2 Jitter Using a BERTScope® Bit Error Rate Testing Application Note [[https://download.tek.com/document/65W_26040_0_Letter.pdf](https://download.tek.com/document/65W_26040_0_Letter.pdf)]

## Pulse Width Jitter (PWJ)

![image-20250816125512147](jitter/image-20250816125512147.png)

![image-20250816125533070](jitter/image-20250816125533070.png)

> Jeff Morriss Updated 10/25/07. Analysis of 8G PCIe Pulse Width Jitter (*UI to UI Jitter_10_25.ppt*)



---

![image-20250816132730999](jitter/image-20250816132730999.png)



## Duty Cycle Distortion – DCD

![dcd.drawio](jitter/dcd.drawio.svg)
$$
\boxed{DJ_{DCD,pp} = 2 \times UI \times \left| DCD\% - 50\% \right|}
$$


| Jitter measurement | Description                                                  |
| :----------------- | :----------------------------------------------------------- |
| DCD                | Duty Cycle Distortion is the peak-to-peak amplitude of the component of the deterministic jitter correlated with the signal polarity. |

![image-20250816081711834](jitter/image-20250816081711834.png)

![image-20250816081808897](jitter/image-20250816081808897.png)

---

> Jitter fundamental & How Isolating Root Causes of Jitter [[https://picture.iczhiku.com/resource/eetop/ShKgzTEiUfdFOcvn.pdf](https://picture.iczhiku.com/resource/eetop/ShKgzTEiUfdFOcvn.pdf)]

There are two primary causes of DCD jitter which are usually generated within a transmitter

-  If the data input to a transmitter is theoretically perfect, but if the ***transmitter sampling threshold*** is offset from its ideal level, then the output of transmitter will have duty cycle distortion as ***a function of the slew rate of the data signal*** 
- Another cause of duty cycle distortion can be a ***mismatch/asymmetry in rising and falling edge speeds***

![image-20250816085315710](jitter/image-20250816085315710.png)

---

Unfortunately, other sources such as ISI almost always exist making it sometimes difficult to isolate the DCD component. One technique to test for DCD is to stimulate your system/components with ***a repeating `1-0-1-0…` data pattern.*** This technique will eliminate inter-symbol interference (ISI) jitter and make viewing the DCD within the spectrum display much easier

> Why clock pattern? That's because all symbols experience ***same*** inter-symbol interference, which are canceled out

---

![image-20250816103444976](jitter/image-20250816103444976.png)

---

![image-20250816180338475](jitter/image-20250816180338475.png)

> [[https://scdn.rohde-schwarz.com/ur/pws/dl_downloads/dl_application/application_notes/1td03/1TD03_2e_RTO_Jitter_Analysis.pdf](https://scdn.rohde-schwarz.com/ur/pws/dl_downloads/dl_application/application_notes/1td03/1TD03_2e_RTO_Jitter_Analysis.pdf)]

## Correlated  vs. Uncorrelated

If the PDF of one jitter source changes when the PDF of another source is changed, then those two sources are ***dependent*** or ***correlated***

![image-20250816080432083](jitter/image-20250816080432083.png)





## Inter-Symbol Interference  (ISI)

The primary cause of Data Dependent Jitter

![image-20250816090326309](jitter/image-20250816090326309.png)

![image-20250816090430513](jitter/image-20250816090430513.png)

---



Jitter measurements can be classified into three categories: *cycle-to-cycle jitter*, *period jitter*, and *long-term jitter*

Jitter is a key performance parameter. Need to know what matters in each case: 

- *PJ* for digital timing
- *LTJ* for data converters and serial data
- *Phase noise* for communications (not all bandwidths matter)



![image-20240714095712249](jitter/image-20240714095712249.png)

> The above Cycle-Cycle Jitter equation is **wrong**,  $\tau_1$ and $\tau_2$ are not independent




##  Short Term Jitter

![image-20230916235240675](jitter/image-20230916235240675.png)

![image-20230916235314423](jitter/image-20230916235314423.png)

> **Period jitter**, *Jper* is the short term variation in clock period compared to the average (mean) clock period.
>
>  **Cycle-to-Cycle**, *Jcc* is the time difference of two adjacent clock periods





## Long Term Jitter (LTJ)

> [[https://people.engr.tamu.edu/spalermo/ecen689/PRBS_&_PLL_model.pdf](https://people.engr.tamu.edu/spalermo/ecen689/PRBS_&_PLL_model.pdf)]
>
> ***absolute jitter*** is also known as ***long-term jitter***
>
> ![image-20251218214812202](jitter/image-20251218214812202.png)

![image-20230916235647723](jitter/image-20230916235647723.png)

![image-20230916235709504](jitter/image-20230916235709504.png)

---

***measuring LTJ***

![image-20230916235033464](jitter/image-20230916235033464.png)

## Jitter Calculation Examples

![image-20230917003028143](jitter/image-20230917003028143.png)

## Jcc vs Jper

> Estimating the RMS cycle-to-cycle jitter if all you have available is the RMS period jitter.

- **Cycle-to-cycle jitter** - The *short-term* variation in clock period between *adjacent* clock cycles. This jitter measure, abbreviated here as $J_{CC}$, may be specified as either an RMS or peak-to-peak quantity.
- **Period jitter** - The *short-term* variation in clock period over *all* measured clock cycles, compared to the average clock period. This jitter measure, abbreviated here as $J_{PER}$, may be specified as either an RMS or peak-to-peak quantity.

Let the variable below represent the variance of a single edge's timing jitter, i.e. the difference in time of a jittery edge versus an ideal edge, $\sigma^2_j$

If each edge's jitter is *independent* then the variance of the period jitter can be written as
$$\begin{align}
\sigma^2_\text{jper} &= (\sigma_\text{j(n+1)}-\sigma_\text{j(n)})^2 \\
&= \sigma_\text{j(n+1)}^2-2\sigma_\text{j(n+1)}\sigma_\text{j(n)})+\sigma_\text{j(n)})^2\\
&= \sigma_\text{j(n+1)}^2+\sigma_\text{j(n)})^2 \\
&=2\sigma^2_j
\end{align}$$

In every cycle-to-cycle measurement we use one "**interior**" clock edge *twice* and therefore we must account for this

$$\begin{align}
\sigma^2_\text{jcc} &= (\sigma_\text{jper(n+1)}-\sigma_\text{jper(n)})^2 \\
&=(\sigma_\text{j(n+2)}-2\sigma_\text{j(n+1)}+\sigma_\text{j(n)})^2
\end{align}$$

Since each edge's jitter is assumed to be *independent* and have the same statistical properties we can drop the cross correlation terms and write:

$$\begin{align}
\sigma^2_\text{jcc} &=(\sigma_\text{j(n+2)}-2\sigma_\text{j(n+1)}+\sigma_\text{j(n)})^2 \\
&=\sigma_\text{j(n+2)}^2+4\sigma_\text{j(n+1)}^2+\sigma_\text{j(n)}^2 \\
&=6\sigma_\text{j}^2
\end{align}$$

The ratio of the variances is therefore
$$
\frac{\sigma^2_\text{jcc}}{\sigma^2_\text{jper}} = \frac{6\sigma_\text{j}^2} {2\sigma_\text{j}^2}=3
$$
Then
$$
\sigma_\text{jcc} = \sqrt{3}\sigma_\text{per}
$$

> [[Timing 101 #8: The Case of the Cycle-to-Cycle Jitter Rule of Thumb, Silicon Labs](https://community.silabs.com/s/share/a5U1M000000knzoUAA/timing-101-8-the-case-of-the-cycletocycle-jitter-rule-of-thumb?language=en_US)]







## Phase Noise Modeling

### w/ noisefile

> Tawna, "Modeling Oscillators with Arbitrary Phase Noise Profiles"[[https://community.cadence.com/cadence_blogs_8/b/rf/posts/modeling-oscillators-with-arbitrary-phase-noise-profiles](https://community.cadence.com/cadence_blogs_8/b/rf/posts/modeling-oscillators-with-arbitrary-phase-noise-profiles)]
>
> —, "How to Specify Phase Noise as an Instance Parameter in Spectre Sources (e.g. vsource, isource, Port)" [[https://community.cadence.com/cadence_blogs_8/b/rf/posts/how-to-specify-phase-noise-as-an-instance-parameter-in-spectre-sources-e-g-vsource-isource-port](https://community.cadence.com/cadence_blogs_8/b/rf/posts/how-to-specify-phase-noise-as-an-instance-parameter-in-spectre-sources-e-g-vsource-isource-port)]



![image-20260719013301709](jitter/image-20260719013301709.png)

![image-20260719012251065](jitter/image-20260719012251065.png)

driving an otherwise ideal oscillator with direct phase modulation makes its noise purely PM — a good model of near-carrier oscillator noise 

![image-20260719020826827](jitter/image-20260719020826827.png)

![image-20260719015605522](jitter/image-20260719015605522.png)

In verilog-A model `oscwphnoise.va`, ***Norton-equivalent circuit***
$$
\boxed{v(t) = A\cos(\omega_0 t + \phi(t))\approx A[\cos\omega_0 t - \sin\omega_0 t \cdot \varphi(t)]}
$$
![image-20260719105917024](jitter/image-20260719105917024.png)

```verilog
`define db10_real(x) pow(10, (x)/10)
`define dbm2pow(x) `db10_real(((x)-30))
`define pow2v(x,r) sqrt(8*(r)*(x))
```

The first two macros convert the available power from dBm to watts:
$$
P_{\mathrm{W}}
=
10^{(P_{\mathrm{dBm}}-30)/10}.
$$
The third macro calculates the **open-circuit peak voltage**
$$
V_{\text{oc,pk}}=\sqrt{8R_{\text{out}}P_{\mathrm{W}}}.
$$
The factor $8$ follows from a matched source:
$$
V_{\text{load,pk}}=\frac{V_{\text{oc,pk}}}{2},
$$
and therefore
$$
P_{\mathrm{avail}}
=
\frac{V_{\text{load,rms}}^2}{R_{\text{out}}}
=
\frac{\left(V_{\text{oc,pk}}/2\sqrt{2}\right)^2}{R_{\text{out}}}
=
\frac{V_{\text{oc,pk}}^2}{8R_{\text{out}}}.
$$
For the defaults,
$$
P=10\ \mathrm{dBm}=10\ \mathrm{mW},
\qquad
R_{\text{out}}=50\ \Omega,
$$
so
$$
V_{\text{oc,pk}}
=
\sqrt{8(50)(0.01)}
=
2\ \mathrm{V}.
$$
With a matched $50\ \Omega$ load, the load voltage is $1\ \mathrm{V_{pk}}$, corresponding to $10\ \mathrm{dBm}$. 





```verilog
`include "constants.vams"
`include "disciplines.vams"

// Behavioral oscillator with an arbitrary phase noise profile.

// fundname: the name of the fundamentail frequency default: ""
// power: available power (dBm) 	default: 10 dBm
// freq: output frequency (Hz)          default: 1 GHz
// rout: output impedance (Ohm)        	default: 50 Ohm

`define db10_real(x) pow(10, (x)/10)
`define dbm2pow(x) `db10_real( ((x)-30) )
`define pow2v(x,r) sqrt(8*(r)*(x))  // open-circuit peak voltage

module oscwphnoise(out, ph);
inout out;
input ph;
electrical out;
electrical ph;
electrical gnd;
ground gnd;
electrical int;

parameter real power = 10 ;
parameter real rout = 50 ;
parameter real freq = 1e+09 ;
  
isource #(.type("sine"), .ampl(`pow2v(`dbm2pow(power),rout)/rout), .freq(freq) ) is1(gnd,out);
vsource #(.type("sine"), .ampl(`pow2v(`dbm2pow(power),rout)/rout), .sinephase(-90), .freq(freq) ) vs1(gnd,int);
 
analog begin
    I(out) <+ -V(int)*V(ph); // - \sin\omega_c t \cdot \phi(t)
    I(out) <+ V(out)/rout;
end

endmodule
```

Note that `int` is purely internal — no current flows there, and it never appears at the output; `vs1` exists only to be sampled by the multiplier



---

 `isource` and `vsource` are **not built-in Verilog-A language constructs**. They are Cadence-provided behavioral source modules
$$
\boxed{
\texttt{isource},\ \texttt{vsource}
\text{ are instantiated source models supplied by Cadence}
}
$$

1. **vsource (p, n)** forces V(p) − V(n) = w(t), where for `type="sine"` the waveform is w(t) = ampl·sin(2πf(t − delay) + sinephase·π/180), with `sinephase` in degrees. 

​		So in the model, `vs1(gnd, int)` means V(gnd) − V(int) = w(t), i.e. **V(int) = −w(t)** — the polarity flips because ground was listed first.



2. **isource (p, n)**: positive current flows *from p, through the source, to n* — it is pulled out of node p and **injected into node n**. 

​		So `is1(gnd, out)` pumps ampl·sin(ωt) into node `out`, which is exactly why the blog wired it as (gnd, out): to drive the output. Writing `is1(out, gnd)` with the same amplitude would sink that current from `out` instead



3. **`I(a,b) <+ expr`** adds a current `expr` flowing a → b through that branch. 

​	So **`I(out) <+ V(out)/rout`** is a resistor from `out` to ground, 

​	and `**I(out) <+ -X**` *injects* X into `out` (positive contribution = current leaving the node)



---

---

![image-20260719010706918](jitter/image-20260719010706918.png)

For modern spectreRF, PORTs and other sources with **noisefiles** or **instance parameter** are easier and correct methods

Starting in **MMSIM 13.1**, you can specify the phase noise as an instance parameter in Spectre sources, including port, vsource and isource

![image-20260719005818616](jitter/image-20260719005818616.png)

The `Generate noise?` button (corresponds to `isnoisy` parameter on the port) is **by default set to "yes"**





### w/ periodic jitter inject

> 我想流tsmc28nm, 振荡器噪声建模：从Phase Noise 到Jitter [[xiaohongshu](https://www.xiaohongshu.com/explore/6a70334c000000000502bd25?xsec_token=CBgayytWezHD3rQO6rVJU8hNnyvEQrepUC7c_s163Abiw=&xsec_source=app_share)]
>
> Claude Fable5 [[Github gist](https://gist.github.com/raytroop/d206c428bf3ac2e07f13a34c32246943)]
>
> Matthew Schubert. Colouring Noise - Generating coloured noise to simulate physical processes [[https://blog.ioces.com/matt/posts/colouring-noise/](https://blog.ioces.com/matt/posts/colouring-noise/)] [[https://gist.github.com/m-schubert/45c562146c6607b8990f1e8f34ff87b0](https://gist.github.com/m-schubert/45c562146c6607b8990f1e8f34ff87b0)]

The same jitter standard deviation $\sigma_a^2$ can correspond to completely different phase noise shapes. A single $\sigma_a^2$ **cannot** define the PN shape, because σ is an *integral* of the spectrum, and integration throws away shape information. 

The shape lives in the **correlation structure** of the jitter sequence — equivalently, in *how* $\sigma^2_{p(N)}$ grows with $N$ — and in your simulation it is set by *how you generate and inject* the samples, not by the $\sigma_a^2$ value itself

![image-20260803174915707](jitter/image-20260803174915707.png)



***Flat: $\mathcal{L}(f)=\mathcal{L}_0$***

**statistically independent edges**, the generator therefore perturbs each ideal edge directly, with **no accumulation**
$$
t_n \;=\; nT_0 + a_n,
\qquad
a_n \stackrel{\text{iid}}{\sim} \mathcal{N}\!\left(0,\;\sigma_a^2\right),
\qquad
\sigma_a^2 = \frac{\mathcal{L}_0}{4\pi^2 f_0}
$$

---



***$1/f^2$: $\mathcal{L}(f)=\mathcal{L}_1 f_1^2/f^2$ (white FM)***

$\sigma_p^2(N)\;=\;\frac{\mathcal{L}_1 f_1^2}{f_0^3}\,N$ — **Linear growth** in $N$ is the signature of **independent increments**, the generator injects an iid error into every period and **accumulates edges**:
$$
t_n \;=\; t_{n-1} + T_0 + d_n,
\qquad
d_n \stackrel{\text{iid}}{\sim} \mathcal{N}\!\left(0,\;\sigma_\Delta^2\right),
\qquad
\sigma_\Delta^2 \;=\; \sigma_p^2(N{=}1) \;=\; \frac{\mathcal{L}_1 f_1^2}{f_0^3}
$$

---



***$1/f^3$: $\mathcal{L}(f)=\mathcal{L}_1 f_1^3/f^3$ (flicker FM)***

> shaping noise in the frequency domain
>
> `fft` and `ifft` are just tool to transform between time domain and frequency domain — we only care about input PSD (**uniformly sampled discrete white noise**) and final output PSD

```python
W = np.fft.rfft(rng.standard_normal(M))
```

This generates white Gaussian noise and transforms it to the frequency domain, i.e. Unit-variance sampled white noise has one-sided PSD
$$
S_W = \frac{2}{f_s}
$$

```python
H[1:] = 1.0 / np.sqrt(f[1:])
```

Filtering amplitudes by $1/\sqrt f$ filters power by
$$
|H(f)|^2=\frac{1}{f}
$$


```python
return x * np.sqrt(c * fs / 2.0)
```

Therefore, the resulting sequence has a $1/f$ PSD. DC is set to zero because ideal $1/f$ noise diverges at $f=0$.

Unit-variance sampled white noise has one-sided PSD $2/f_s$. Thus the output PSD is
$$
S_o(f) = \frac{2}{f_s}\frac{1}{f} \left(\frac{c f_s}{2}\right) = \frac{c}{f}
$$

```python
c_fl  = 2 * L3 * f1 ** 3 / f0 ** 4      # 1/f^3: period-error PSD S_d(f)=c/f [s^2/Hz]
```

$$
c_{fl} = \frac{2L_3f_1^3}{f_0^4}
$$



```python
J["1_f3_only"] = np.cumsum(d3)
```

**Accumulation is discrete-time integration**. Its exact transfer function is
$$
|H_{\mathrm{acc}}(f)|^2 = \frac{1}{4\sin^2(\pi f/f_0)} \approx \frac{f_0^2}{4\pi^2f^2}, \qquad f\ll f_0
$$
Consequently, the accumulated time-error PSD is

$$
S_J(f) \approx \frac{c}{f}\frac{f_0^2}{4\pi^2f^2} = \frac{c f_0^2}{4\pi^2f^3}
$$


Timing error is converted to phase using $\phi=2\pi f_0J$

Therefore,

$$
S_\phi(f) =(2\pi f_0)^2S_J(f) \approx \frac{c f_0^4}{f^3}
$$
Since the code uses the usual phase-noise definition $L(f)=S_\phi(f)/2$

$$
L(f)=\frac{c f_0^4}{2f^3}
$$
The coefficient is selected as $c_{fl} = \frac{2L_3f_1^3}{f_0^4}$. Substitution gives exactly the desired target:

$$
\boxed{L(f)=L_3\left(\frac{f_1}{f}\right)^3}
$$
In short:

$$
\underbrace{\frac1f}_{\text{flicker period noise}} \times \underbrace{\frac1{f^2}}_{\text{accumulation}} = \underbrace{\frac1{f^3}}_{\text{phase noise}}
$$

![pn_closedloop](jitter/pn_closedloop.png)

![sigma_pN](jitter/sigma_pN.png)




```python
EULER_GAMMA = 0.5772156649015329

# ----------------------------------------------------------------- targets ----
f0 = 5.015e9                # DCO frequency [Hz]
T0 = 1.0 / f0
f1 = 1e6                    # reference offset for the sloped lines [Hz]
L0_dB = -155.0              # flat floor            [dBc/Hz]
L2_dB = -128.0              # 1/f^2 line @ 1 MHz    [dBc/Hz]
L3_dB = -130.0              # 1/f^3 line @ 1 MHz    [dBc/Hz]
L0, L2, L3 = (10 ** (x / 10) for x in (L0_dB, L2_dB, L3_dB))

M    = 2 ** 22              # number of simulated periods (~0.84 ms)
fmin = f0 / M               # low-frequency cutoff set by record length
rng  = np.random.default_rng(7)

# ----------------------------- sigma_p^2(N)  ->  generator parameters ---------
var_a = L0 / (4 * np.pi ** 2 * f0)      # flat : edge-jitter variance   [s^2]
var_d = L2 * f1 ** 2 / f0 ** 3          # 1/f^2: per-period variance = sigma_p^2(1)
c_fl  = 2 * L3 * f1 ** 3 / f0 ** 4      # 1/f^3: period-error PSD S_d(f)=c/f [s^2/Hz]

print(f"sigma_a  (flat, per edge)    = {np.sqrt(var_a)*1e15:8.3f} fs")
print(f"sigma_d  (1/f^2, per period) = {np.sqrt(var_d)*1e15:8.3f} fs")
print(f"flicker coefficient c        = {c_fl:.3e}  s^2  (S_d = c/f)")

def flicker(M, fs, c, rng):
    """Zero-mean Gaussian sequence with one-sided PSD c/f, sampled at fs."""
    W = np.fft.rfft(rng.standard_normal(M)) # Unit-variance sampled white noise has one-sided PSD 2/fs
    f = np.fft.rfftfreq(M, d=1.0 / fs)
    H = np.zeros_like(f)
    H[1:] = 1.0 / np.sqrt(f[1:])            # |H|^2 = 1/f, DC removed
    x = np.fft.irfft(W * H, n=M)
    return x * np.sqrt(c * fs / 2.0)        # c/f

# --------------------------------------------- generate the three sequences ---
a  = rng.standard_normal(M) * np.sqrt(var_a)    # flat : direct edge displacement
d2 = rng.standard_normal(M) * np.sqrt(var_d)    # white period errors
d3 = flicker(M, f0, c_fl, rng)                  # flicker period errors

# --------------------- per-period injection  +  edge accumulation -------------
#   t_n = n*T0 + J(n).  Only the deviation J is accumulated -> no precision loss.
J = {
    "flat_only": a,                              # no accumulation (white PM)
    "1_f2_only": np.cumsum(d2),                  # random walk     (white FM)
    "1_f3_only": np.cumsum(d3),                  # flicker walk    (flicker FM)
}
J["all_noise"] = J["1_f2_only"] + J["1_f3_only"] + a

def Lref_dB(name, f):
    if name == "flat_only":
        return np.full_like(f, L0_dB)
    if name == "1_f2_only":
        return L2_dB - 20 * np.log10(f / f1)
    if name == "1_f3_only":
        return L3_dB - 30 * np.log10(f / f1)
    return 10 * np.log10(L0 + L2 * f1 ** 2 / f ** 2 + L3 * f1 ** 3 / f ** 3)
```



---

Let the input period error be \(d[n]\), and let the accumulated timing error be $J[n]=J[n-1]+d[n]$

This is exactly what `np.cumsum(d)` implements, assuming $J[-1]=0$

Taking the \(z\)-transform: $J(z)=z^{-1}J(z)+D(z)$

Rearranging $J(z)(1-z^{-1})=D(z)$

so the accumulator transfer function is
$$
H_{\mathrm{acc}}(z) =\frac{J(z)}{D(z)} =\frac{1}{1-z^{-1}}
$$


To obtain its frequency response, evaluate it on the unit circle: $z=e^{j\omega}$

Therefore,
$$
H_{\mathrm{acc}}(e^{j\omega}) = \frac{1}{1-e^{-j\omega}}
$$
Its power gain is the squared magnitude:
$$
|H_{\mathrm{acc}}(e^{j\omega})|^2 = \frac{1}{|1-e^{-j\omega}|^2}
$$
The denominator can be simplified as

$$\begin{aligned} 
|1-e^{-j\omega}|^2 &=(1-e^{-j\omega})(1-e^{j\omega})\\ 
&=2-e^{j\omega}-e^{-j\omega}\\ 
&=2-2\cos\omega\\ 
&=4\sin^2\left(\frac{\omega}{2}\right)
\end{aligned}$$

Thus the exact discrete-time power gain is

$$
\boxed{ |H_{\mathrm{acc}}(e^{j\omega})|^2 = \frac{1}{4\sin^2(\omega/2)} }
$$


## references

AN10007 Clock Jitter Definitions and Measurement Methods, SiTime [[pdf](https://www.sitime.com/sites/default/files/hiddenresources/AN10007-Jitter-and-measurement-methods_SIT.pdf)]

SERDES Design and Simulation Using the Analog FastSPICE Platform, Silicon Creations [[pdf](https://www.siliconcr.com/sc-cms/uploads/u2u_presentation_sc_april25.pdf)]

Flexible clocking solutions in advanced processes from 180nm to 5nm, Silicon Creations [[pdf](https://www.siliconcr.com/sc-cms/uploads/siliconcreations_iccad_2019_v2_191020.pdf)]

One-size-fits-all PLLs for Advanced Samsung Foundry Processes, Silicon Creations [[pdf](https://www.siliconcr.com/sc-cms/uploads/siliconcreations_dac_2022_v2_22-07-12.pdf)]

Circuit Design and Verification of 7nm LowPower, Low-Jitter PLLs, Silicon Creations, [[pdf](https://www.siliconcr.com/sc-cms/uploads/u2u-2018-sicr-plls-v3-180509.pdf)]

Lecture 10: Jitter, ECEN720: High-Speed Links Circuits and Systems Spring 2023 [[pdf](https://people.engr.tamu.edu/spalermo/ecen689/lecture10_ee720_jitter.pdf)]

Jitter 360° Knowledge Series  [[pdf](https://ransomsnotes.com/index_htm_files/RansomStephensAndTektronixJitter360.pdf), [slides](https://picture.iczhiku.com/resource/eetop/WyiGPhKZaiWfoXxM.pdf)]

N. Da Dalt, "Tutorial: Jitter: Basic and Advanced Concepts, Statistics, and Applications," *2012 IEEE International Solid-State Circuits Conference*, San Francisco, CA, USA, 2012 [[slides](https://picture.iczhiku.com/resource/eetop/WhiryqaaRpqYeCxx.pdf), [transcript](https://picture.iczhiku.com/resource/eetop/WYifhqAAZphyFNcn.pdf) ]

