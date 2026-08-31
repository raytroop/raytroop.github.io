---
title: Digital Phase-Locked Loops
date: 2025-05-13 17:30:16
tags:
categories:
- link
mathjax: true
---



## Hunting Jitter

***Hunting jitter*** is often referred to as ***dithering jitter***, the *periodic* time error between *data clock* and input data, which exhibits a ***limit-cycle*** behavior

![image-20250819202727871](dpll/image-20250819202727871.png)

![image-20250819203806711](dpll/image-20250819203806711.png)

![image-20250819210031102](dpll/image-20250819210031102.png)



## BB PD

> Youngdon Choi, Deog-Kyoon Jeong and W. Kim, "Jitter transfer analysis of tracked oversampling techniques for multigigabit clock and data recovery," in IEEE Transactions on Circuits and Systems II: Analog and Digital Signal Processing, vol. 50, no. 11, pp. 775-783, Nov. 2003 [[https://sci-hub.st/10.1109/TCSII.2003.819070](https://sci-hub.st/10.1109/TCSII.2003.819070)]
>
> John T. Stonick, ISSCC 2011 TUTORIALS *T5: DPLL-Based Clock and Data Recovery*
>
> Walker, Richard. (2003). Designing Bang-Bang PLLs for Clock and Data Recovery in Serial Data Transmission Systems.  [[pdf](https://www.omnisterra.com/walker/pdfs.papers/BBPLL.pdf)]
>
> —, Clock and Data Recovery for Serial Data Communications, focusing on bang-bang CDR design methodology, ISSCC Short Course, February 2002. [[slides](https://www.omnisterra.com/walker/pdfs.talks/ISSCC2002.pdf)]

It's **ternary**, because *early*, *late* and *no transition*

notice the ***transition density = 1*** in digital PLL

### Linearization

The effective PD gain is a function of the **input jitter pdf**, it enables one to anticipate the effects of input jitter on loop characteristics


BB Gain is the slope of average BB output $\mu$, versus phase offset $\phi$, i.e. $\frac {\partial \mu}{\partial \phi}$,

BB only produces output for a transition and this de-rates the gain. ***Transition density = 0.5*** for ***random*** data

$$
K_{BB} = \frac{1}{2}\frac {\partial \mu}{\partial \phi}
$$

where $\mu = (1)\times \mathrm{P}(\text{late}|\phi) + (-1)\times \mathrm{P}(\text{early}|\phi)$

![bb-PDF.drawio](dpll/bb-PDF.drawio.svg)


> Both jitter and amplitude noise distribution are same, just scaled by slope


### Self-Noise Term

One price we pay for ***BB PD*** versus ***linear PD*** is the self-noise term. **For** **small phase errors** BB output noise is the **full magnitude** of the sliced data

> The PD output should be almost **0** for small phase errors. i.e. ideal PD output noise should be **0**

$$
\sigma_{BB}^2 = 1^2 \cdot \mathrm{P}(\text{trans}) + 0^2\cdot (1-\mathrm{P}(\text{trans})) = 0.5
$$

![image-20241127215947017](dpll/image-20241127215947017.png)

**Input referred jitter** from BB PD is **proportional to incoming jitter**

![image-20241127220933103](dpll/image-20241127220933103.png)



### gain simulation

> L. Avallone, M. Mercandelli, A. Santiccioli, M. P. Kennedy, S. Levantino and C. Samori, "A Comprehensive Phase Noise Analysis of Bang-Bang Digital PLLs," in IEEE Transactions on Circuits and Systems I: Regular Papers, vol. 68, no. 7, pp. 2775-2786, July 2021 [[https://sci-hub.st/10.1109/TCSI.2021.3072344](https://sci-hub.st/10.1109/TCSI.2021.3072344)]
>
> T. -K. Kuan and S. -I. Liu, "A Bang Bang Phase-Locked Loop Using Automatic Loop Gain Control and Loop Latency Reduction Techniques," in IEEE Journal of Solid-State Circuits, vol. 51, no. 4, pp. 821-831, April 2016 [[https://sci-hub.st/10.1109/JSSC.2016.2519391](https://sci-hub.st/10.1109/JSSC.2016.2519391)]

![image-20250902215541227](dpll/image-20250902215541227.png)

![image-20250913192552933](dpll/image-20250913192552933.png)

```python
import matplotlib.pyplot as plt
import numpy as np

N = 2**10
sigma = 0.1
dt = np.random.normal(0, sigma, size=N)
et = np.sign(dt)

# Eq-(2)
coef_form = np.mean(np.abs(dt)) / np.mean(np.power(dt, 2))
print(f'coef_form: {coef_form}')

# Eq-(9)
coef_gauss = (2/np.pi)**0.5/sigma
print(f'coef_gauss: {coef_gauss}')

# polyfit
coef_fit = np.polyfit(dt, et, 1)
print(f'coef_fit: {coef_fit}')

x = np.linspace(-3.5, 3.5, 1000)
y = coef_fit[0]*x + coef_fit[1]

plt.figure(figsize=(12,6))
plt.plot(dt, et, 'o')
plt.plot(x, y, linewidth=2, linestyle='--')

# Calculate histogram counts and bin edges
counts, bin_edges = np.histogram(dt, bins=100)
# Find the maximum count
max_count = counts.max()
# Create weights to normalize the maximum height to 1
weights = np.ones_like(dt) / max_count
plt.hist(dt, bins=100, weights=weights)

plt.xlabel(r'$\Delta t$')
plt.grid(True)
plt.legend([r'$\Delta t \sim \varepsilon $', r'$x_{fit} \sim y_{fit}$', r'$ \text{hist}_{\Delta t}$'])
plt.show()


# coef_form: 7.82197790742685
# coef_gauss: 7.978845608028654
# coef_fit: [7.82251511 0.01010586]
```



---

> Pavan, Shanthi, Richard Schreier, and Gabor Temes. (2016). Understanding Delta-Sigma Data Converters. 2nd ed. Wiley.  - *2.2.1 Quantizer Modeling*

![image-20250902212931083](dpll/image-20250902212931083.png)
$$
\frac{\mathrm{d}\sigma_e^2}{\mathrm{d}k} =0\space\space\Rightarrow\space\space k=\frac{\left\langle  v,y\right\rangle}{\left\langle y,y \right\rangle}
$$

![image-20250902231449843](dpll/image-20250902231449843.png)

## DCO Quantization Noise

*TODO* &#128197;





## TDC Quantization Noise

*TODO* &#128197;

![image-20250601122145164](dpll/image-20250601122145164.png)


## CDR Loop Latency

> Amir Amirkhany. ISSCC 2019 "Basics of Clock and Data Recovery Circuits"
>



![image-20250706121529451](dpll/image-20250706121529451.png)

---

![image-20241102235118149](dpll/image-20241102235118149.png)

![image-20241102235145417](dpll/image-20241102235145417.png)

loop latency is represented as $e^{-sD}$ in linear model

---

![image-20241102235736432](dpll/image-20241102235736432.png)

![image-20241103000223470](dpll/image-20241103000223470.png)

![image-20241103000653906](dpll/image-20241103000653906.png)



### Sensitivity to Loop Latency

![image-20241103142137640](dpll/image-20241103142137640.png)

---

![image-20241103142656134](dpll/image-20241103142656134.png)

![image-20241103142531277](dpll/image-20241103142531277.png)

![image-20241103142938907](dpll/image-20241103142938907.png)



### Loop Latency model

> CC Chen. Why A Low Loop Latency in A CDR Design? [[https://youtu.be/io9WZbhlahU](https://youtu.be/io9WZbhlahU)]
>
> —. Why Understanding and Optimizing Loop Latency for A CDR Design? [[https://youtu.be/Jyy18865jv8](https://youtu.be/Jyy18865jv8)]
>
> Walker, Richard. (2003). Designing Bang-Bang PLLs for Clock and Data Recovery in Serial Data Transmission Systems. [[paper](https://www.omnisterra.com/walker/pdfs.papers/BBPLL.pdf),[slides](https://www.omnisterra.com/walker/pdfs.talks/bctm2.maker.pdf)]

![image-20260831225928887](dpll/image-20260831225928887.png)

![image-20260831230613322](dpll/image-20260831230613322.png)



```python
"""
Behavioral model of the experiment on the slides
"Max dphi w/ SJ & Sweeping loop Latency" (pages 5 and 6):

    8 Gb/s, PRBS7, no input RJ
    SJ = 10 %UI p-p @ 100 MHz
    T_D (loop latency) = 2 / 5 / 10 UI  ->  dphi = 12 / 19 / 23 %UI p-p

Units: time step = 1 UI (125 ps @ 8 Gb/s), all phases in UI.

Loop (digital type-II, latency T_D inserted in the feedback path):

    e[n]       = sign(dphi[n]) on data transitions, 0 otherwise   (BBPD)
    acc[n+1]   = acc[n]   + Ki * e[n-TD]                          (integral / freq)
    ph_ck[n+1] = ph_ck[n] + acc[n+1] + Kp * e[n-TD]               (VCO phase)
    dphi[n]    = ph_din[n] - ph_ck[n]

Fitted gains that reproduce the three measured points:

    Kp = 0.60 %UI per decision,  Ki = Kp/1024
    -> dphi(p-p) = 12.8 / 19.3 / 23.4 %UI   (measured 12 / 19 / 23)

Key mechanism (confirmed by the page-6 zoom): the loop is SLEW-RATE LIMITED,
not bandwidth limited.  The CDR can move clock phase at most

    SR    = Kp * eta                    ~ 3.0 mUI/UI  (eta = PRBS7 edge density)

while the SJ demands

    SJ_SR = pi * A_pp * f_sj / f_b      ~ 3.9 mUI/UI

Since SR < SJ_SR, ph_ck ramps at constant slope, falls behind, and then keeps
ramping past the input after the sine turns around; T_D extends that turnaround.
The result is a coherent triangular oscillation at f_sj whose amplitude EXCEEDS
the input jitter.  The regime boundary is

    f_SL  = Kp * eta * f_b / (pi * A_pp) ~ 77 MHz
"""

def bbcdr(TD_UI=2, Kp=KP_FIT, zeta_div=ZD_FIT, ki_en=None,
          sj_pp=0.10, f_sj=100e6, f_b=F_B, ppm=0.0,
          n_ui=20000, n_settle=4000, seed=0x7F):
    """
    One CDR run.  Returns the waveforms plus p-p / peak / rms phase error
    measured after n_settle UI.

    dphi = ph_din - ph_ck   (>0 : data late -> clock must be delayed)

    ki_en : True -> type-II (Ki = Kp/zeta_div), False -> type-I (Ki = 0),
            None -> follow the module-level KI_EN.
    """
    use_ki = KI_EN if ki_en is None else ki_en
    Ki = Kp / zeta_div if use_ki else 0.0
    TD = int(round(TD_UI))

    n = np.arange(n_ui)
    ph_din = 0.5 * sj_pp * np.sin(2 * np.pi * (f_sj / f_b) * n) + ppm * 1e-6 * n

    bits = prbs7(n_ui + 1, seed)
    trans = (bits[1:] != bits[:-1]).astype(np.int8)   # BBPD updates on edges only

    ph_ck = np.empty(n_ui)
    dphi = np.empty(n_ui)
    e_buf = np.zeros(TD + 1)                          # latency pipeline
    acc = 0.0
    ck = 0.0

    for i in range(n_ui):
        d = ph_din[i] - ck
        dphi[i] = d
        ph_ck[i] = ck

        e_buf[1:] = e_buf[:-1]
        e_buf[0] = np.sign(d) * trans[i]              # BBPD decision
        e_del = e_buf[TD]                             # delayed by T_D UI

        acc += Ki * e_del
        ck += acc + Kp * e_del

    d = dphi[n_settle:]
    return dict(dphi=dphi, ph_ck=ph_ck, ph_din=ph_din, t=n,
                pp=d.max() - d.min(), peak=np.abs(d).max(), rms=d.std())
```











---

![image-20260831230916152](dpll/image-20260831230916152.png)

![image-20260831231004522](dpll/image-20260831231004522.png)





## DT & CT Spectral Density

> Sam Palermo, ECEN620: Network Theory Broadband Circuit Design Fall 2025 *Lecture 9: Digital PLLs* [[https://people.engr.tamu.edu/spalermo/ecen620/lecture09_ee620_digital_PLLs.pdf](https://people.engr.tamu.edu/spalermo/ecen620/lecture09_ee620_digital_PLLs.pdf)]
>
> Michael Perrott, August 14, 2008. Short Course On Phase-Locked Loops and Their Applications Day 4, AM Lecture *Digital Frequency Synthesizers* [[https://www.cppsim.com/PLL_Lectures/day4_am.pdf](https://www.cppsim.com/PLL_Lectures/day4_am.pdf)]
>
> —, "A modeling approach for Sigma Delta fractional-N frequency synthesizers allowing straightforward noise analysis," in *IEEE Journal of Solid-State Circuits*, vol. 37, no. 8, pp. 1028-1038, Aug. 2002 [[https://www.cppsim.com/Publications/JNL/perrott_jssc02.pdf](https://www.cppsim.com/Publications/JNL/perrott_jssc02.pdf)]
>
> —. "Techniques for high data rate modulation and low power operation of fractional-N frequency synthesizers." 1997. [[https://www.cppsim.com/Publications/Theses/perrott_phdthesis.pdf](https://www.cppsim.com/Publications/Theses/perrott_phdthesis.pdf)]
>
> Hsu, Chun-Ming, Ph. D. Massachusetts Institute of Technology. "Techniques for high-performance digital frequency synthesis and phase control." 2008. [[http://hdl.handle.net/1721.1/45870](http://hdl.handle.net/1721.1/45870)]
>
> J. R. Barry, E. A. Lee, and D. G. Messerschmitt, Digital Communication, 3rd ed., Boston, MA: Kluwer Academic Publishers, 2003.



![psd_ct_dt.drawio](dpll/psd_ct_dt.drawio.svg)

- $\color{red}\frac{1}{T}$ of CT-DT originates from CT to sampled sequence to impulse train Fourier transform, which is **explicit** in frequency-domain model
- $\color{red}\frac{1}{T}$ originates from DT **spectrum** to CT impulse **spectrum** is **implicit** in frequency-domain model
- $\color{red}T$ of DT-CT originates from **ZOH approximation** following impulse train, which is **explicit** in frequency-domain model

![image-20260628083804908](dpll/image-20260628083804908.png)

### Divider Sampling Operation & ITM

***Impulse Train Modulator (ITM)***

![image-20260626221809983](dpll/image-20260626221809983.png)

The **double outline of the box** in the figure is meant to serve as a reminder that a **sampling operation** is taking place

![image-20260626214746157](dpll/image-20260626214746157.png)



---

![image-20250913130708018](dpll/image-20250913130708018.png)

![image-20250913130847600](dpll/image-20250913130847600.png)





### DT -> CT

![image-20260625221638670](dpll/image-20260625221638670.png)

![image-20260625221753608](dpll/image-20260625221753608.png)

$\boxed{S_x(e^{j2\pi fT}) = S_d(f)\cdot \textcolor{blue}{\frac{1}{T}}=S_c(f)\cdot \textcolor{blue}{\frac{1}{T}}}$,   For example, the quantization noise spectrum is given by $S_x(e^{j2\pi fT}) = \frac{1}{12f_s}\cdot \frac{1}{T} = \frac{1}{12}$. To convert the sequence spectrum into a continuous impulse train spectrum, we multiply by $\color{blue}\frac{1}{T^2}$
$$
S_y(f) = S_x(e^{j2\pi fT}) \cdot \textcolor{blue}{T\cdot \frac{1}{T^2}\cdot |H(f)|^2 } = S_x(e^{j2\pi fT}) \cdot \textcolor{blue}{\frac{1}{T}|H(f)|^2}
$$


![image-20260625222247558](dpll/image-20260625222247558.png)

![image-20250512230604969](dpll/image-20250512230604969.png)

![image-20260626232513174](dpll/image-20260626232513174.png)

### CT -> DT -> CT

![image-20260625233049546](dpll/image-20260625233049546.png)





![image-20260625234115193](dpll/image-20260625234115193.png)

![image-20260625233852702](dpll/image-20260625233852702.png)

![image-20260625234008676](dpll/image-20260625234008676.png)


Assume that the lower $m$ bits of the digital filter output are discarded by truncation. The truncation error is therefore modeled as a uniformly distributed random variable,

$$
E_t \sim U[0,2^m\text{LSB}]
$$

Because the effective output resolution is reduced, the new least significant bit becomes

$$
\text{LSB}_t = 2^m\text{LSB}
$$

and the DAC quantization error is correspondingly modeled as

$$
Q_{DAC} \sim U[0,1] \space \text{in}\space \text{LSB}_t
$$



![image-20260625233243905](dpll/image-20260625233243905.png)

## Enhancing Resolution w/ DSM

> J. Stonick. ISSCC 2011 tutorials, T5: "DPLL-Based Clock and Data Recovery"
>
> Amir Amirkhany. ISSCC 2019 "Basics of Clock and Data Recovery Circuits"

![image-20260812233408446](dpll/image-20260812233408446.png)

$M+1$ bits ensure on overflow or underflow in the signed adder

![image-20260812233515238](dpll/image-20260812233515238.png)



![image-20260812232659641](dpll/image-20260812232659641.png)



## !! DPLL time-domain model

> L. Avallone, M. Mercandelli, A. Santiccioli, M. P. Kennedy, S. Levantino and C. Samori, "A Comprehensive Phase Noise Analysis of Bang-Bang Digital PLLs," in IEEE Transactions on Circuits and Systems I: Regular Papers, vol. 68, no. 7, pp. 2775-2786, July 2021 [[https://sci-hub.st/10.1109/TCSI.2021.3072344](https://sci-hub.st/10.1109/TCSI.2021.3072344)]
>
> —, “Contributions to the Theory and Development of Low-Jitter Bang-Bang Integrated Frequency Synthesizers.” University College Dublin. School of Electrical and Electronic Engineering, 2022. [[http://hdl.handle.net/10197/13372](http://hdl.handle.net/10197/13372)]
>
> N. Da Dalt, "Linearized Analysis of a Digital Bang-Bang PLL and Its Validity Limits Applied to Jitter Transfer and Jitter Generation," in IEEE Transactions on Circuits and Systems I: Regular Papers, vol. 55, no. 11, pp. 3663-3675, Dec. 2008 [[https://sci-hub.st/10.1109/TCSI.2008.925948](https://sci-hub.st/10.1109/TCSI.2008.925948)]



![ChatGPT Image Aug 31, 2026, 08_26_30 PM](dpll/ChatGPT%20Image%20Aug%2031,%202026,%2008_26_30%20PM.png)

The paper defines the BPD input as

$$
\boxed{\Delta t[k]=t_r[k]-t_d[k]}
$$

where $t_r[k]$ is the reference-edge timestamp and $t_d[k]$ is the divider-output timestamp.



The signal chain is essentially
$$
\epsilon[k] \rightarrow \underbrace{\beta\epsilon[k]+\psi[k]}_{u[k]} \rightarrow \underbrace{K_T u[k]}_{\text{DCO period change}} \rightarrow T_v.
$$

A useful distinction is that $K_T$ is **not the usual DCO frequency gain $K_{\mathrm{DCO}}$ in Hz/code**. This paper models the DCO in the **period domain**, so its gain is *period/code*. Around the nominal operating point, $f=\frac{1}{T}$

hence for a small period change,

$$
\Delta f \approx -\frac{\Delta T}{T_0^2}.
$$

Therefore the corresponding frequency gain would be approximately

$$
\boxed{ K_{\mathrm{DCO}} \approx -\frac{K_T}{T_0^2} = -K_T f_v^2 }
$$

in *Hz/code*. The minus sign means increasing the period lowers the frequency.

![image-20260831205554741](dpll/image-20260831205554741.png)

```matlab
%% DPLL parameters from the paper
fr    = 100e6;
N     = 24;
fv    = N*fr;

beta  = 70;
alpha = beta/2^8;

KT = 0.145e-15;          % [s/bit]

df = 1e6;                % DCO PN specified at 1 MHz

%% Table-I cases
%           Ref PN       DCO PN @ 1 MHz
cases = [   -155,        -Inf;
            -Inf,        -108;
            -155,        -108;
            -150,        -108;
            -155,        -103];

Nsim  = 1e6;
Nburn = 2e4;

rng(1);

sigma_sim = zeros(size(cases,1),1);

for icase = 1:size(cases,1)

    Lref = cases(icase,1);
    Ldco = cases(icase,2);

    %% ------------------------------------------------------------
    % Reference white phase noise -> absolute timestamp jitter
    %% ------------------------------------------------------------
    if isinf(Lref)
        sigma_ref = 0;
    else
        Sphi_ref = 10^(Lref/10);

        sigma_ref = sqrt( ...
            Sphi_ref/(4*pi^2*fr) );
    end

    %% ------------------------------------------------------------
    % DCO 1/f^2 phase noise -> DCO cycle jitter
    % Eq. (15)
    %% ------------------------------------------------------------
    if isinf(Ldco)
        sigma_Tv = 0;
    else
        Sphi_dco = 10^(Ldco/10);

        sigma_Tv = sqrt( ...
            Sphi_dco * df^2 / fv^3 );
    end

    fprintf('\nCase %d\n',icase);
    fprintf('sigma_ref = %.3f fs\n',sigma_ref/1e-15);
    fprintf('sigma_Tv  = %.3f fs\n',sigma_Tv/1e-15);

    %% Reference absolute jitter
    jr = sigma_ref * randn(Nsim+1,1);

    %% Sum of N independent DCO-period errors
    %
    % Wv[k] = sum of N cycle-jitter samples
    %
    Wv = sqrt(N)*sigma_Tv*randn(Nsim,1);

    %% ------------------------------------------------------------
    % Bang-bang DPLL
    %% ------------------------------------------------------------

    dt  = zeros(Nsim+1,1);
    psi = 0;

    % t_r[0] - t_d[0]
    dt(1) = jr(1);  % or w/ Zero-initialization

    for k = 1:Nsim

        %% Binary phase detector
        if dt(k) >= 0
            epsilon = +1;
        else
            epsilon = -1;
        end

        %% Integral path
        psi = psi + alpha*epsilon;

        %% PI loop-filter output
        u = beta*epsilon + psi;

        %% Time-error recursion
        dt(k+1) = dt(k) ...
                + (jr(k+1)-jr(k)) ...	% absolute jitter to period jitter
                - N*KT*u ...
                - Wv(k);

    end

    %% Remove startup transient
    dt_ss = dt(Nburn+1:end);

    sigma_sim(icase) = std(dt_ss);

end

%% Results
fprintf('\n------------------------------------------\n');
fprintf('Case       sigma_Dt [fs]\n');
fprintf('------------------------------------------\n');

for k = 1:length(sigma_sim)
    fprintf('(%c)        %8.2f\n', ...
        'a'+k-1, sigma_sim(k)/1e-15);
end
```

There are two different random sequences:

$$
\boxed{j_r[k] = \text{absolute reference edge jitter}}
$$

versus

$$
\boxed{\delta T_r[k]=j_r[k+1]-j_r[k] =\text{reference period jitter}}.
$$

Our simulation generates

```
jr = sigma_ref * randn(...);
```

because the paper assumes **white absolute reference jitter**. The paper explicitly calls $\sigma_{t_r}^2$ the *absolute jitter variance of the reference*. 

Then the model naturally converts that absolute jitter into reference-period variation using

```
jr(k+1) - jr(k)
```

There is also a subtle but important consequence. If $j_r[k]\sim\mathcal N(0,\sigma_{t_r}^2)$ is i.i.d., then $\operatorname{Var}\{j_r[k+1]-j_r[k]\} = 2\sigma_{t_r}^2.$

But consecutive period errors are **correlated**:

$$
\operatorname{Cov} \left( j_r[k+1]-j_r[k], j_r[k+2]-j_r[k+1] \right) = -\sigma_{t_r}^2.
$$

So you should **not** replace the code with independent samples such as

```
djr = sqrt(2)*sigma_ref*randn(...);
```

because that gets the variance right but loses the required correlation.

In short:

$$
\boxed{ \texttt{jr[k]}=\text{edge jitter} \quad\Rightarrow\quad \texttt{jr[k+1]-jr[k]}=\text{period jitter} }
$$

and the DPLL recursion evolves from **one edge interval to the next**, which is why the difference appears.







---

$\boxed{\sigma_{\Delta t}}$ at the **BPD input**, not directly the RMS DCO-output jitter. To obtain actual DCO-output jitter, we should also simulate/store $t_v[h]$, rather than only the reference-rate recursion for $\Delta t[k]$.





## reference

Topics in IC (Wireline Transceiver Design) [[https://ocw.snu.ac.kr/sites/default/files/NOTE/Lec%203%20-%20ADPLL.pdf](https://ocw.snu.ac.kr/sites/default/files/NOTE/Lec%203%20-%20ADPLL.pdf)]

Michael H. Perrott, ISSCC 2008 Tutorial on Digital Phase-Locked Loops 

—, CICC 2009 Tutorial on Digital Phase-Locked Loops [[https://www.cppsim.com/PLL_Lectures/digital_pll_cicc_tutorial_perrott.pdf](https://www.cppsim.com/PLL_Lectures/digital_pll_cicc_tutorial_perrott.pdf)]

Robert Bogdan Staszewski,  CICC 2020:  Beyond All-Digital PLL for RF and Millimeter-Wave Frequency Synthesis [[link](https://www.researchgate.net/profile/Yizhe-Hu/publication/342702810_Beyond_All-Digital_PLL_for_RF_and_Millimeter-Wave_Frequency_Synthesis/links/5f02305692851c52d619ce21/Beyond-All-Digital-PLL-for-RF-and-Millimeter-Wave-Frequency-Synthesis.pdf)]

Akihide Sai, ISSCC 2023 T5: All-digital PLLs From Fundamental Concepts to Future Trends 

Mike Shuo-Wei Chen, CICC 2020 ES2-3: Low-Spur PLL Architectures and Techniques [[https://youtu.be/sgPDchYhN-4](https://youtu.be/sgPDchYhN-4)]

S. Levantino, "Digital phase-locked loops," 2018 IEEE Custom Integrated Circuits Conference (CICC), San Diego, CA, USA, 2018

Saurabh Saxena, IIT Madras. Phase-Locked Loops: Noise Analysis in Digital PLL [[https://youtu.be/mddtxcqfiKU](https://youtu.be/mddtxcqfiKU)]

---

Y. Hu, T. Siriburanon and R. B. Staszewski, "Multirate Timestamp Modeling for Ultralow-Jitter Frequency Synthesis: A Tutorial," in *IEEE Transactions on Circuits and Systems II: Express Briefs*, vol. 69, no. 7, pp. 3030-3036, July 2022

---

Neil Robertson. Digital PLL's -- Part 1 [[https://www.dsprelated.com/showarticle/967.php](https://www.dsprelated.com/showarticle/967.php)]

—. Digital PLL's -- Part 2 [[https://www.dsprelated.com/showarticle/973.php](https://www.dsprelated.com/showarticle/973.php)]

—. Digital PLL's -- Part 3 [[https://www.dsprelated.com/showarticle/1177.php](https://www.dsprelated.com/showarticle/1177.php)]

Daniel Boschen. GRCon24 - Quick Start on Control Loops with Python Workshop [[video](https://youtu.be/RxQWk1PjJLQ), [slides](https://events.gnuradio.org/event/24/contributions/599/)]

---

M. Zanuso, D. Tasca, S. Levantino, A. Donadel, C. Samori and A. L. Lacaita, "Noise Analysis and Minimization in Bang-Bang Digital PLLs," in IEEE Transactions on Circuits and Systems II: Express Briefs, vol. 56, no. 11, pp. 835-839, Nov. 2009 [[https://sci-hub.st/10.1109/TCSII.2009.2032470](https://sci-hub.st/10.1109/TCSII.2009.2032470)]

N. Da Dalt, "Markov Chains-Based Derivation of the Phase Detector Gain in Bang-Bang PLLs," in IEEE Transactions on Circuits and Systems II: Express Briefs, vol. 53, no. 11, pp. 1195-1199, Nov. 2006 [[https://sci-hub.st/10.1109/TCSII.2006.883197](https://sci-hub.st/10.1109/TCSII.2006.883197)]

—, "A design-oriented study of the nonlinear dynamics of digital bang-bang PLLs," in *IEEE Transactions on Circuits and Systems I: Regular Papers*, vol. 52, no. 1, pp. 21-31, Jan. 2005 [[https://sci-hub.se/10.1109/TCSI.2004.840089](https://sci-hub.se/10.1109/TCSI.2004.840089)]

—, "Theory and Implementation of Digital Bang-Bang Frequency Synthesizers for High Speed Serial Data Communications", PhD Dissertation, RWTH Aachen University, Aachen, North Rhine-Westphalia, Germany, 2007 [[pdf](https://publications.rwth-aachen.de/record/62439/files/DaDalt_Nicola.pdf)]

---

***hunting jitter***

S. Jang, S. Kim, S. -H. Chu, G. -S. Jeong, Y. Kim and D. -K. Jeong, "An Optimum Loop Gain Tracking All-Digital PLL Using Autocorrelation of Bang–Bang Phase-Frequency Detection," in IEEE Transactions on Circuits and Systems II: Express Briefs, vol. 62, no. 9, pp. 836-840, Sept. 2015 [[https://sci-hub.st/10.1109/TCSII.2015.2435691](https://sci-hub.st/10.1109/TCSII.2015.2435691)] [[phd thesis](https://s-space.snu.ac.kr/bitstream/10371/119111/1/000000066677.pdf)]

Deog-Kyoon Jeong. Topics in IC (Wireline Transceiver Design). Lec 3 - All-Digital PLL [[https://ocw.snu.ac.kr/sites/default/files/NOTE/Lec%203%20-%20ADPLL.pdf](https://ocw.snu.ac.kr/sites/default/files/NOTE/Lec%203%20-%20ADPLL.pdf)]

—. Topics in IC (Wireline Transceiver Design). Lec 6 - Clock and Data Recovery [[https://ocw.snu.ac.kr/sites/default/files/NOTE/Lec%206%20-%20Clock%20and%20Data%20Recovery.pdf](https://ocw.snu.ac.kr/sites/default/files/NOTE/Lec%206%20-%20Clock%20and%20Data%20Recovery.pdf)]

Lee Hae-Chang.: ‘*An estimation approach to clock and data recovery*’, PhD Thesis, Stanford University, November 2006 [[pdf](https://www-vlsi.stanford.edu/people/alum/pdf/0611_HaechangLee_Phase_Estimation.pdf)]

J. Kim, Design of CMOS Adaptive-Supply Serial Links, Ph.D. Thesis, Stanford University, December 2002. [[pdf](https://vlsiweb.stanford.edu/people/alum/pdf/0212_Kim_______Design_Of_CMOS_AdaptiveSu.pdf)]

High-speed Serial Interface 2013. Lect. 16 – Clock and Data Recovery 3 [[http://tera.yonsei.ac.kr/class/2013_1_2/lecture/Lect16_CDR-3.pdf](http://tera.yonsei.ac.kr/class/2013_1_2/lecture/Lect16_CDR-3.pdf)]

CC Chen. Why Hunting Jitter Happens in CDR: The Role of Input Jitter and Latency? [[https://youtu.be/hPDielPsFgY](https://youtu.be/hPDielPsFgY)]
