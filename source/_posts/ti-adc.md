---
title: Time-Interleaved ADC (TI-ADC)
date: 2025-06-07 23:17:25
tags:
categories:
- adc-dac
mathjax: true
---

![image-20260914193314752](ti-adc/image-20260914193314752.png)



## Frequency Domain Model

![f-mdl.drawio](ti-adc/f-mdl.drawio.svg)

![image-20260913094812184](ti-adc/image-20260913094812184.png)



<span style="color:white; background-color:black">Why (8.14) means "sampled at $T_s$"</span>
$$
X_s(f) = \frac{1}{T_s}\sum_{k=-\infty}^{\infty} X(f - kf_s)
$$

This spectrum is periodic with period $f_s$: copies of $X(f)$ sit at every multiple of $f_s$, with weight $1/T_s$. That is exactly the spectrum of uniform sampling at $T_s$



## Interleaver Architectures

![image-20260914194340521](ti-adc/image-20260914194340521.png)



<span style="color:white; background-color:black">Direct Interleaver</span>

![image-20260914194944454](ti-adc/image-20260914194944454.png)

> similar to increase the resolution of the flash ADC with *more* parallel comparators





<span style="color:white; background-color:black">De-multiplexing Interleaver</span>

![image-20260914200548166](ti-adc/image-20260914200548166.png)

it is the *front-end samplers* that determine *timing/bandwidth mismatch errors*

only one front-end channel $L=1$ eliminate any timing/bandwidth mismatch errors to the first order



<span style="color:white; background-color:black">Re-sampling Interleaver</span>

 ![image-20260914195228805](ti-adc/image-20260914195228805.png)



> back-end re-sampling occur after the front-end,  two $\frac{KT}{C}$ contribution in total noise (De-multiplexing Interleaver only one $\frac{KT}{C}$)
>
> without buffer, charging distribution reduce signal and reduce SNR, but buffers give excess noise



---



![image-20260906160455591](ti-adc/image-20260906160455591.png)



<span style="color:white; background-color:black">Interleaver Model</span>

![image-20260914195326519](ti-adc/image-20260914195326519.png)











## Interleaving Errors

![image-20260914202358169](ti-adc/image-20260914202358169.png)

![image-20260915213004819](ti-adc/image-20260915213004819.png)



<span style="color:white; background-color:black">Offset Mismatch Errors</span>

![image-20260914202446007](ti-adc/image-20260914202446007.png)



<span style="color:white; background-color:black">Gain Mismatch Errors</span>

![image-20260914202550362](ti-adc/image-20260914202550362.png)

![image-20250621072944516](ti-adc/image-20250621072944516.png)

![image-20260914210022880](ti-adc/image-20260914210022880.png)



<span style="color:white; background-color:black">Timing Mismatch Errors</span>

![image-20260914204512858](ti-adc/image-20260914204512858.png)


In the frequency domain,

$$
\mathcal{L}\left\{ \frac{dV(t)}{dt} \right\}
\;\longrightarrow\;
sV(s)
\quad\text{and, for }s=j\omega,\quad
j\omega V(j\omega).
$$

The factor

$$
j=e^{j\pi/2}
$$

introduces a **$+\pi/2$ (90°) phase shift**, while $\omega$ scales the magnitude proportionally to frequency.

In the time domain,

$$
\frac{d}{dt}\sin(\omega t)
=\omega\cos(\omega t)
=\omega\sin\left(\omega t+\frac{\pi}{2}\right).
$$

Thus, differentiation produces two effects: **magnitude scaling by $\omega$** and a **$90^\circ$ phase advance**.


**Frequency-dependent**: the *higher* frequency input signal $f_\text{in}$, the *larger* error becomes

![image-20250621091024424](ti-adc/image-20250621091024424.png)

![image-20260914210257078](ti-adc/image-20260914210257078.png)

![image-20250621091047339](ti-adc/image-20250621091047339.png)





<span style="color:white; background-color:black">Bandwidth Mismatch Errors</span>

![image-20260914202752033](ti-adc/image-20260914202752033.png)

> ![image-20250621093321623](ti-adc/image-20250621093321623.png)



## ADC Clocking

<span style="background-color:yellow">**Track-and-Hold (TAH)**</span>, <span style="background-color:yellow">**Sample-and-Holds (SAH)**</span>

![image-20261017111944790](ti-adc/image-20261017111944790.png)

Note that the falling edge of $\phi_1$ is **determined by the rising edge of CK** and is thus **free from jitter and mismatch in $X_1$**, which accumulates jitter and phase mismatch

![image-20260920233403464](ti-adc/image-20260920233403464.png)

<span style="background-color:yellow">**reset mechanism** to the latches for nominal order</span>

![image-20261017112345989](ti-adc/image-20261017112345989.png)



---



<span style="color:white; background-color:black">a clock generator for an eight-channel ADC</span>

![image-20260920235134383](ti-adc/image-20260920235134383.png)

| NORed    |                        | $\div 2$         | $\div 2 \div 2$  |
| -------- | ---------------------- | ---------------- | ---------------- |
| $\phi_1$ | $\text{CK}$            | $I_1$            | $I_2$            |
| $\phi_2$ | $\overline{\text{CK}}$ | $Q_1$            | $I_3$            |
| $\phi_3$ | $\text{CK}$            | $\overline{I_1}$ | $Q_2$            |
| $\phi_4$ | $\overline{\text{CK}}$ | $\overline{Q_1}$ | $Q_3$            |
| $\phi_5$ | $\text{CK}$            | $I_1$            | $\overline{I_2}$ |
| $\phi_6$ | $\overline{\text{CK}}$ | $Q_1$            | $\overline{I_3}$ |
| $\phi_7$ | $\text{CK}$            | $\overline{I_1}$ | $\overline{Q_2}$ |
| $\phi_8$ | $\overline{\text{CK}}$ | $\overline{Q_1}$ | $\overline{Q_3}$ |

$\text{CK}$, $I/Q_1$ and $I/Q_{2,3}$ shift by **1UI**



### Interchannel Crosstalk

> D. Xu *et al*., "8.5 A Scalable Adaptive ADC/DSP-Based 1.25-to-56Gbps/112Gbps High-Speed Transceiver Architecture Using Decision-Directed MMSE CDR in 16nm and 7nm," *2021 IEEE International Solid-State Circuits Conference (ISSCC)*, San Francisco, CA, USA, 2021, pp. 134-136 [[https://sci-hub.ru/10.1109/ISSCC42613.2021.9366063](https://sci-hub.ru/10.1109/ISSCC42613.2021.9366063)]

![image-20260920232810972](ti-adc/image-20260920232810972.png)

![image-20261018192820211](ti-adc/image-20261018192820211.png)



### 64Gb/s Clock Generation

> D. Xu *et al*., "8.5 A Scalable Adaptive ADC/DSP-Based 1.25-to-56Gbps/112Gbps High-Speed Transceiver Architecture Using Decision-Directed MMSE CDR in 16nm and 7nm," *2021 IEEE International Solid-State Circuits Conference (ISSCC)*, San Francisco, CA, USA, 2021, pp. 134-136 [[https://sci-hub.ru/10.1109/ISSCC42613.2021.9366063](https://sci-hub.ru/10.1109/ISSCC42613.2021.9366063)]

![image-20261018193058479](ti-adc/image-20261018193058479.png)

![image-20261018192820211](ti-adc/image-20261018192820211.png)

---

<span style="color:white; background-color:black">**4x8 Time Interleaving w/ 25% duty cycle for input tracking**</span>



![adc_clocking_TH](ti-adc/adc_clocking_TH.svg)

![4way-clocking-TH.drawio](ti-adc/4way-clocking-TH.drawio.svg)



<span style="background-color:yellow">Ensure nominal order by **masking some edges**</span>

![adc_clocking_reset](ti-adc/adc_clocking_reset.svg)

![4way-clocking-reset-mask.drawio](ti-adc/4way-clocking-reset-mask.drawio.svg)



### 128Gb/s Clock Generation


> Z. Guo et al., "A 112.5Gb/s ADC-DSP-Based PAM-4 Long-Reach Transceiver with >50dB Channel Loss in 5nm FinFET," 2022 IEEE International Solid-State Circuits Conference (ISSCC), San Francisco, CA, USA, 2022 [[https://sci-hub.st/10.1109/ISSCC42614.2022.9731650](https://sci-hub.st/10.1109/ISSCC42614.2022.9731650)]
>
> P. Liu et al., "A 128Gb/s ADC/DAC Based PAM-4 Transceiver with >45dB Reach in 3nm FinFET," 2025 Symposium on VLSI Technology and Circuits (VLSI Technology and Circuits), Kyoto, Japan, 2025

![adc-clk_4to32way_8to64way.drawio](ti-adc/adc-clk_4to32way_8to64way.drawio.svg)

![image-20250806224145281](ti-adc/image-20250806224145281.png)

![8way-interleaving-Marvell-ISSCC2022.drawio](ti-adc/8way-interleaving-Marvell-ISSCC2022.drawio.svg)





![image-20250808220954208](ti-adc/image-20250808220954208.png)

![image-20250808221134749](ti-adc/image-20250808221134749.png)

![RX-Clocking-Marvell-VLSI2025.drawio](ti-adc/RX-Clocking-Marvell-VLSI2025.drawio.svg)











### 224Gb/s Clock Generation

> M. Gambhir *et al*., "A 2.05pJ/bit, 212.5Gbps DSP Based Transceiver with 55dB Reach in 3nm FinFET," *2026 IEEE/JSAP Symposium on VLSI Technology and Circuits (VLSI Technology and Circuits)*, Honolulu, HI, USA, 2026, pp. 1-3, doi: 10.1109/VLSITechnologyandCir65830.2026.11577411.



![image-20261018203306919](ti-adc/image-20261018203306919.png)

![image-20261018203332571](ti-adc/image-20261018203332571.png)

4UI track, 12UI hold in TAH



## shift register-based clock divider for TH<sub>2</sub> clocks

> J. Im *et al*., "6.1 A 112Gb/s PAM-4 Long-Reach Wireline Transceiver Using a 36-Way Time-Interleaved SAR-ADC and Inverter-Based RX Analog Front-End in 7nm FinFET," *2020 IEEE International Solid-State Circuits Conference - (ISSCC)*, San Francisco, CA, USA, 2020, pp. 116-118 [[https://sci-hub.ru/10.1109/ISSCC19947.2020.9063081](https://sci-hub.ru/10.1109/ISSCC19947.2020.9063081)]
>
> —, "A 112-Gb/s PAM-4 Long-Reach Wireline Transceiver Using a 36-Way Time-Interleaved SAR ADC and Inverter-Based RX Analog Front-End in 7-nm FinFET," in IEEE Journal of Solid-State Circuits, vol. 56, no. 1, pp. 7-18, Jan. 2021 [[https://sci-hub.ru/10.1109/JSSC.2020.3024261](https://sci-hub.ru/10.1109/JSSC.2020.3024261)]

![image-20261025125422783](ti-adc/image-20261025125422783.png)

![image-20261031123020616](ti-adc/image-20261031123020616.png)

![thck_6ui_2p4ui.drawio](ti-adc/thck_6ui_2p4ui.drawio.svg)



![image-20261025130744430](ti-adc/image-20261025130744430.png)

![image-20261025135125595](ti-adc/image-20261025135125595.png)

![th2ck_36ui_4ui.drawio](ti-adc/th2ck_36ui_4ui.drawio.svg)

> ![image-20261031123046608](ti-adc/image-20261031123046608.png)
>
> ![image-20261025143050494](ti-adc/image-20261025143050494.png)





---

a.k.a. <span style="background-color:yellow">**ring counter**</span>, generating **SAH** clock

![image-20261018235719799](ti-adc/image-20261018235719799.png)

![adc_clocking_ring](ti-adc/adc_clocking_ring.svg)

all FFs initialized to 0



## Rank<sub>1</sub> & Rank<sub>2</sub> Clock relationship

> J. Im *et al*., "6.1 A 112Gb/s PAM-4 Long-Reach Wireline Transceiver Using a 36-Way Time-Interleaved SAR-ADC and Inverter-Based RX Analog Front-End in 7nm FinFET," *2020 IEEE International Solid-State Circuits Conference - (ISSCC)*, San Francisco, CA, USA, 2020, pp. 116-118 [[https://sci-hub.ru/10.1109/ISSCC19947.2020.9063081](https://sci-hub.ru/10.1109/ISSCC19947.2020.9063081)]
>
> —, "A 112-Gb/s PAM-4 Long-Reach Wireline Transceiver Using a 36-Way Time-Interleaved SAR ADC and Inverter-Based RX Analog Front-End in 7-nm FinFET," in IEEE Journal of Solid-State Circuits, vol. 56, no. 1, pp. 7-18, Jan. 2021 [[https://sci-hub.ru/10.1109/JSSC.2020.3024261](https://sci-hub.ru/10.1109/JSSC.2020.3024261)]
>
> M. -A. LaCroix *et al*., "8.4 A 116Gb/s DSP-Based Wireline Transceiver in 7nm CMOS Achieving 6pJ/b at 45dB Loss in PAM-4/Duo-PAM-4 and 52dB in PAM-2," *2021 IEEE International Solid-State Circuits Conference (ISSCC)*, San Francisco, CA, USA, 2021, pp. 132-134 [[https://sci-hub.ru/10.1109/ISSCC42613.2021.9366030](https://sci-hub.ru/10.1109/ISSCC42613.2021.9366030)]
>
> G. Li *et al*., "18.1 A 600Gb/s DP-QAM64 Coherent Optical Transceiver Frontend with 4x105GS/s 8b ADC/DAC in 16nm CMOS," *2024 IEEE International Solid-State Circuits Conference (ISSCC)*, San Francisco, CA, USA, 2024, pp. 338-340 [[https://sci-net.xyz/10.1109/ISSCC49657.2024.10454499](https://sci-net.xyz/10.1109/ISSCC49657.2024.10454499)]

![image-20261031125216446](ti-adc/image-20261031125216446.png)

There are overlap between clk6UI_ph0UI and clk36UI_ph0UI, clk36UI_ph12UI, clk36UI_ph24UI, clk36UI_ph6UI, clk36UI_ph18UI, clk36UI_ph30UI

<span style="color:white; background-color:black">J. Im: TH2 track overlaps TH1 track</span>

| 56GS/s, 1UI = 17.9ps                         | window                       |
| -------------------------------------------- | ---------------------------- |
| TH1 track (40% DCC)                          | $0 \to 2.4\text{UI}$         |
| TH1 hold                                     | $2.4 \to 6\text{UI}$ (3.6UI) |
| TH2 track (ring counter by ph0, trim by ph4) | $0 \to 4\text{UI}$           |

- overlap with TH1 **current** track: 2.4UI
- TH2 settling after TH1 hold: $4-2.4 = 1.6\text{UI}$ (~29ps)
- margin before TH1 **next** track: $6-4 = 2\text{UI}$ (~36ps)

<span style="background-color:yellow">what matters is where $\Phi_2$ falling edge lands</span>: after $\Phi_1$ falling edge + settling, before $\Phi_1$ next rising edge with margin for PVT drift between fast Rank1 path & slow Rank2 path → LaCroix's **aligner**

![image-20261031125418057](ti-adc/image-20261031125418057.png)

![image-20261031125520312](ti-adc/image-20261031125520312.png)






## ADC Data Alignment

> Gain Kim, 2023. Equalization, Architecture, and Circuit Design for High-Speed Serial Link Receiver [[www.theise.org/...](https://www.theise.org/wp-content/uploads/2023/10/Analog_1_%EA%B9%80%EA%B0%80%EC%9D%B8%EA%B5%90%EC%88%98%EB%8B%98_DGIST_LectureNote-Min-Jae-Seo.pdf)]

![image-20261009070618262](ti-adc/image-20261009070618262.png)





## Skew Calibration Techniques

Timing-skew calibration has two separate tasks: **detect the relative sampling-time errors**, then **correct the sampling instants or the resulting digital errors**. Foreground/background describes when estimation runs; analog/digital describes where correction occurs. A digital detector driving a variable delay line is a mixed-signal calibration loop.

For an $M$-channel TI-ADC, let $f_s=1/T_s$ be the **aggregate** sampling rate and $\tau_i$ the skew of channel $i$:

$$
t_{i,k}=(kM+i)T_s,\qquad
y_i[k]=x(t_{i,k}+\tau_i)
\approx x(t_{i,k})+\tau_i\dot{x}(t_{i,k}).
$$

This first-order model assumes small skew and omits other errors. It explains why timing error increases with input slope. Calibration removes **relative skew**: adding the same delay to every channel shifts the time origin without producing interleaving mismatch. Random aperture jitter and frequency-dependent bandwidth mismatch are separate limitations. See [S1](#skew-ref-1) and [S2](#skew-ref-2).

### Method Comparison

The main background families are **input-statistics-based**, **reference-channel-based**, and **reference-signal-based** [S1]. The rows below separate useful implementations within these families; digital correction is discussed separately because it can accompany several detectors.

| Method | Timing-error observable | Main advantage | Main limitation / cost | Read |
| --- | --- | --- | --- | --- |
| Foreground training | Channel phase or sample error for a known sine, ramp, or reference edge | Simple identification and startup calibration | Interrupts normal conversion; stored trims do not track later drift | [S1](#skew-ref-1), [S2](#skew-ref-2) |
| Autocorrelation / MAD | Unequal statistics of nominally equal sample intervals | No extra analog reference channel | Input statistics, coherent patterns, and detector slope affect convergence | [S3](#skew-ref-3), [S4](#skew-ref-4) |
| Digital mixing | Products of channel outputs and an estimate of the autocorrelation slope | Can estimate skew magnitude for digital correction | Derivative estimation and correction bandwidth; some implementations add auxiliary samplers | [S5](#skew-ref-5), [S6](#skew-ref-6) |
| Zero-crossing statistics | Unequal crossing counts between adjacent sampling instants | Simple sign/count logic | Requires crossing activity and appropriate sample-sequence control | [S7](#skew-ref-7) |
| Reference-ADC correlation / variance | Correlation or difference between nominally coincident main/reference samples | Provides a common timing reference for all channels | Extra input loading, reference-clock quality, averaging, and possible reference spurs | [S8](#skew-ref-8), [S9](#skew-ref-9) |
| Reference-ADC derivative / LMS | Main/reference sample error multiplied by input slope | Direct early/late information | Must obtain a useful slope estimate; weak input activity slows adaptation | [S10](#skew-ref-10) |
| Injected reference / dither | Response to a known timing-sensitive signal correlated with its modulation sequence | Supplies excitation independently of the unknown input | Injection-path mismatch, headroom, kickback, and residual dither | [S11](#skew-ref-11), [S12](#skew-ref-12) |

### Foreground Calibration with a Known Input

Apply a known calibration waveform, estimate each channel's relative timing, and store clock-trim codes or digital correction coefficients. For a sinusoid, an unwrapped phase difference gives $\Delta\tau=\Delta\phi/(2\pi f_{\mathrm{cal}})$ after accounting for the nominal interleaving phase. A ramp converts timing error into a voltage error through its known slope.

This is useful for initial characterization and coarse startup alignment. Offset, gain, and analog-path phase must be separated from timing error; otherwise the trim can absorb another mismatch. Recalibration is needed if the relative delays drift. Foreground coefficients may be applied continuously during operation, but that alone does not make their **estimation** a background process [S1], [S2].

### Autocorrelation-Based Skew Calibration

Assume the input is wide-sense stationary over the averaging interval, with

$$
R_x(\tau)=E[x(t)x(t+\tau)].
$$

After offset/gain equalization, the correlation between adjacent channel samples is approximately

$$
C_i=R_x(T_s+\tau_{i+1}-\tau_i)
\approx R_x(T_s)+R_x'(T_s)(\tau_{i+1}-\tau_i).
$$

For the last channel, use channel 0's sample from the **next** interleaving frame and set $\tau_M=\tau_0$. Equal nominal intervals should give equal correlations; deviations reveal relative skew when $R_x'(T_s)$ is observable.

#### Hierarchical Calibration and Its Bandwidth Limit

A hierarchical scheme first aligns widely separated channels, then fills in the intermediate phases. Its detector can therefore depend on $R_x'(L T_s)$ with $L>1$, whose sign is harder to guarantee over a wide input band. In the power-of-two hierarchy discussed in [S3], the first step uses a lag of $M T_s/2$; its usual input-bandwidth guarantee is limited to $f_s/M$ [S1].

**Channel grouping and trim-code search are different choices.** Binary search over delay codes still needs a reliable, monotonic error indication; it does not remove a detector's input-bandwidth restriction.

![image-20260328225656118](ti-adc/image-20260328225656118.png)

#### Adjacent-Channel Calibration

Gu et al. [S4] use adjacent-channel statistics to extract all channel skews without the long-lag first step. The first-order relationship can be written as

$$
\overline{C}=\frac{1}{M}\sum_{i=0}^{M-1}C_i\approx R_x(T_s),
\qquad
\sum_{i=0}^{m-1}(C_i-\overline{C})
\approx R_x'(T_s)(\tau_m-\tau_0).
$$

The sum telescopes, giving the skew of channel $m$ relative to channel 0. This illustrates why adjacent correlations can support simultaneous estimation and extend the applicable bandwidth toward $f_s/2$.

![image-20260330204902627](ti-adc/image-20260330204902627.png)

![image-20260330205119231](ti-adc/image-20260330205119231.png)

**Nyquist-band coverage is not input independence.** The ensemble model and finite per-channel averages can differ for coherent inputs. The review [S1] explicitly identifies a sinusoid at $f_s/M$ as a problematic case for [S4]. Low signal activity also reduces detector gain.

For a random-phase sinusoid of amplitude $A$,

$$
R_x(\tau)=\frac{A^2}{2}\cos(2\pi f_{\mathrm{in}}\tau),
\qquad
R_x'(T_s)=-\pi A^2 f_{\mathrm{in}}\sin(2\pi f_{\mathrm{in}}T_s).
$$

Thus the ideal adjacent-correlation detector loses first-order sensitivity at DC and at an exact Nyquist tone. A result measured near Nyquist does not establish convergence for every coherent pattern.

![image-20260324183003185](ti-adc/image-20260324183003185.png)

---

<span style="background-color:yellow">**Why the Wei–Razavi method has a bandwidth restriction**</span>

Using the correlation model discussed above, a detector comparing intervals $L+\Delta t$ and $L-\Delta t$ produces

$$
e=R_x(L+\Delta t)-R_x(L-\Delta t) \approx 2\Delta t\,R_x'(L)
$$

Therefore, **the sign of $e$ indicates the sign of skew only if the sign of $R_x'(L)$ is known**.

For a real WSS input with two-sided PSD $S_x(f)$ confined to $|f|\le B$,

$$
R_x'(L) =-4\pi\int_0^B fS_x(f)\sin(2\pi fL)\,df
$$

A sufficient condition for a negative slope, assuming nonzero signal energy inside the band, is

$$
\boxed{B<\frac{1}{2L}}
$$

Above that range, positive and negative contributions can cancel or reverse the slope.

In the hierarchical multichannel extension, the first calibration step uses $L=MT_s/2$, giving the familiar guarantee

$$
\boxed{B<\frac{f_s}{M}}
$$

The Gu's 2025 review explicitly identifies this limitation. It is a **detector-polarity guarantee**, rather than a claim that every higher-frequency input necessarily fails

<span style="background-color:yellow">**Gu: shorten the correlation lag to address the restriction**</span>

| Approach                                                     | What changes                                                 | Remaining limitation                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Adjacent-channel correlations — Gu et al., JSSC 2025 [S4]** | Uses only lag $T_s$, extending the correlation-slope bandwidth condition toward $f_s/2$ | Still depends on input statistics; certain coherent tones remain problematic |


The method measures all adjacent-channel correlations, uses their average to estimate the ideal adjacent correlation, and combines the deviations to recover each channel’s relative skew. It avoids the widely separated channel pairs in the first hierarchical step:

$$
\boxed{ L:\frac{MT_s}{2}\rightarrow T_s \quad\Longrightarrow\quad B_{\mathrm{guarantee}}:\frac{f_s}{M}\rightarrow\frac{f_s}{2} }
$$

However, the review still identifies a coherent sinusoid at $f_s/M$ as a failure case. Extending the bandwidth does not eliminate sampling-pattern dependence.



#### MAD (Mean Absolute Difference) vs. Correlation

Wei et al. [S3] compare the mean absolute differences on the two sides of a sample, avoiding general-purpose multipliers. To understand the relationship, define

$$
D(\tau)=E[|x(t+\tau)-x(t)|],\qquad
Q(\tau)=E[(x(t+\tau)-x(t))^2].
$$

For a real WSS signal, the squared-difference identity is exact:

$$
Q(\tau)=2[R_x(0)-R_x(\tau)].
$$

MAD does **not** equal the squared difference. Replacing the absolute value by a square in [S3] is an analytical surrogate. If the increment is zero-mean Gaussian, then $D(\tau)=\sqrt{2Q(\tau)/\pi}$, so the two metrics are monotonic functions of one another. WSS alone does not guarantee that relation for arbitrary input distributions.

![image-20260328212413965](ti-adc/image-20260328212413965.png)

### Digital-Mixing-Based Calibration

Here, digital mixing forms products of channel samples to measure correlation imbalance. It belongs to the statistical family above. To estimate skew **magnitude**, rather than only an update direction, the imbalance must be normalized by an estimate of the relevant correlation slope.

Lin et al. [S5] obtain the required information with auxiliary delta-sampling SAR ADCs. Guo et al. [S6] estimate the autocorrelation derivative digitally and correct the timing error without those extra analog channels. Their first-order approximation and derivative bandwidth deserve attention, especially for direct sampling above the first Nyquist zone. The reported 29 mW in [S6] is **ADC-core power with mismatch calibration implemented off-chip**, not the power of a complete on-chip calibration system.

The existing notes from [S6] are retained here:

![image-20260324180833001](ti-adc/image-20260324180833001.png)

### Zero-Crossing-Based Calibration

Wang and Wu [S7] detect skew by counting input zero crossings between adjacent channels while randomly alternating their sampling order. The count imbalance drives digitally controlled delays. This uses sign decisions and counters instead of full-resolution products.

The input must provide sufficient crossings, and the sampling-order scheme is part of the detector. A generic crossing counter cannot be assumed to recover skew for every waveform or sampling rate. Study the paper's convergence and residual-jitter analysis together with its switching sequence.

### Reference-Channel-Based Calibration

An extra ADC samples the same input at nominally coincident instants with each main channel. For an already gain/offset-matched pair, a local model is

$$
e_i=y_i-y_{\mathrm{ref}}
\approx (\tau_i-\tau_{\mathrm{ref}})\dot{x}.
$$

The reference may run slowly while visiting all channel phases. In [S8], choosing $f_{\mathrm{CAL}}=f_s/K$ with $\gcd(K,M)=1$ provides that coverage. **Coprime division guarantees phase-slot coverage, not automatic physical edge alignment**; the clock origin and correction range still need to be designed.

#### Correlation Maximization / Difference-Variance Minimization

El-Chammas and Murmann [S8] maximize the cross-correlation between the reference and each main channel. With matched scaling and delay-independent signal power, maximizing correlation is equivalent to minimizing mean-squared sample difference. Song et al. [S9] provide a variance-based implementation to study alongside it.

These metrics have an extremum at alignment, so a search or perturbation is needed to determine which direction to move. Reference-path bandwidth mismatch can move the optimum; extra sampling loads can also disturb the main input.

#### Derivative-Based LMS

Multiplying the error by an input-slope estimate gives a signed timing observable:

$$
E[e_i\dot{x}]
\approx (\tau_i-\tau_{\mathrm{ref}})E[\dot{x}^{\,2}].
$$

A negative-feedback update can therefore drive the relative skew toward zero. Its actual code-update sign depends on whether increasing the delay code advances or retards the sampling edge.

Stepanović and Nikolić [S10] estimate the derivative using two calibration paths with different analog bandwidths. Read this for the implementation of the slope detector and LMS loop. Unlike purely statistical correlation search, the slope provides direct directional information, but adds circuitry and still needs input activity.

### Reference-Signal / Dither-Injection Calibration

Inject a known waveform with a timing-sensitive slope into the input path. In foreground operation it can replace the normal input. For background operation, modulate the reference with a known pseudo-random sequence and correlate the ADC outputs with that sequence to extract its contribution [S11], [S12].

This supplies calibration excitation even when the external input is quiet or unfavorable for a statistical detector. The main design issue is **which path the injected signal measures**. Injection after a mismatched input-buffer stage can miss that stage's delay; separate injection paths can introduce their own mismatch. Tao et al. [S11] and Cao et al. [S12] are useful comparisons of shared/global injection arrangements.

Check the residual injected component, input headroom, reference-edge quality, and disturbance of the wanted signal. These determine the cost of improved input independence.

### Clock Trimming vs. Digital Error Correction

| Correction | Implementation | What to check |
| --- | --- | --- |
| Analog sampling-time correction | Digital detector adjusts a variable delay line, phase interpolator, or clock-buffer trim | Delay range, resolution, monotonicity, added jitter, and whether the adjusted edge controls the actual sampling aperture |
| Digital reconstruction | Derivative cancellation or fractional-delay / reconstruction filters correct the output samples | Accurate skew magnitude, filter bandwidth, higher-order residuals, word length, throughput, and power |

For small skew, the first-order digital correction is

$$
\widehat{x}[n]=y[n]-\widehat{\tau}_{i(n)}\,\widehat{\dot{x}}[n],
\qquad i(n)=n\bmod M,
$$

where $\widehat{\dot{x}}$ estimates the derivative with respect to **physical time**. A derivative per sample instead requires the normalized coefficient $\widehat{\tau}_i/T_s$. Align the derivative-filter latency with the data and channel index. The remaining error depends on derivative accuracy and higher-order Taylor terms; a digital detector alone does not guarantee an all-digital solution. Read [S13](#skew-ref-13), [S6](#skew-ref-6), and the earlier adaptive approach in [S14](#skew-ref-14).

A common front-end track-and-hold can reduce downstream aperture-mismatch sensitivity, while channel randomization can spread mismatch spurs. These are architectural mitigation techniques, not estimates of the skew itself; spur spreading does not by itself remove total error power [S1].

For an ADC-based SerDes, a useful design check is to identify which front-end sampling rank sets the input aperture, then evaluate the detector with the actual equalized data statistics and repeating patterns. Common sampling-phase recovery and relative interleaver-skew calibration control different degrees of freedom.

### Papers to Read

Suggested first pass: **[S1] → [S2] → [S3] → [S4]** for statistical detection, then **[S8] → [S10] → [S11]** to compare reference-assisted approaches. Read **[S13] → [S6]** for digital correction. The remaining papers deepen particular branches.

<span id="skew-ref-1"></span>
**[S1] Overview.** M. Gu, Y. Tao, Y. Zhong, L. Jie, and N. Sun, “Timing-Skew Calibration Techniques in Time-Interleaved ADCs,” *IEEE Open Journal of the Solid-State Circuits Society*, vol. 5, pp. 1–10, 2025. [DOI / open-access paper](https://doi.org/10.1109/OJSSCS.2024.3519486). Read first for the taxonomy and input-dependence tradeoffs. Note that this review's author list differs from [S4].

<span id="skew-ref-2"></span>
**[S2] Fundamentals.** B. Razavi, “Problem of Timing Mismatch in Interleaved ADCs,” *IEEE CICC*, 2012. [Author PDF](https://www.seas.ucla.edu/brweb/papers/Conferences/BRCICC12.pdf). Read for the error model, sources of skew, and detection/correction alternatives.

<span id="skew-ref-3"></span>
**[S3] MAD detector and delay correction.** H. Wei, P. Zhang, B. D. Sahoo, and B. Razavi, “An 8 Bit 4 GS/s 120 mW CMOS ADC,” *IEEE JSSC*, vol. 49, no. 8, pp. 1751–1761, Aug. 2014. [DOI](https://doi.org/10.1109/JSSC.2014.2313571), [author PDF](https://www.seas.ucla.edu/brweb/papers/Journals/Hegong_JSSC14.pdf). The earlier CICC 2013 paper 16.3 is [here](https://www.seas.ucla.edu/brweb/papers/Conferences/HegongCICC13.pdf). Focus on the multiplier-free detector, channel hierarchy, and fine delay line.

<span id="skew-ref-4"></span>
**[S4] Adjacent-channel statistics.** M. Gu, Y. Tao, X. He, Y. Zhong, L. Jie, and N. Sun, “A 1-GS/s 11-b Time-Interleaved SAR ADC With Robust, Fast, and Accurate Autocorrelation-Based Background Timing-Skew Calibration,” *IEEE JSSC*, vol. 60, no. 2, pp. 421–431, Feb. 2025. [DOI](https://doi.org/10.1109/JSSC.2024.3421363). Compare its simultaneous extraction and bandwidth with [S3], and examine the remaining input restrictions.

<span id="skew-ref-5"></span>
**[S5] Digital mixing with auxiliary sampling.** C.-Y. Lin, Y.-H. Wei, and T.-C. Lee, “A 10-bit 2.6-GS/s Time-Interleaved SAR ADC With a Digital-Mixing Timing-Skew Calibration Technique,” *IEEE JSSC*, vol. 53, no. 5, pp. 1508–1517, May 2018. [DOI](https://doi.org/10.1109/JSSC.2018.2793535). Focus on the delta-sampling auxiliary ADCs and how skew magnitude is obtained.

<span id="skew-ref-6"></span>
**[S6] Fully digital mixing-based calibration.** M. Guo, J. Mao, S.-W. Sin, H. Wei, and R. P. Martins, “A 5 GS/s 29 mW Interleaved SAR ADC With 48.5 dB SNDR Using Digital-Mixing Background Timing-Skew Calibration for Direct Sampling Applications,” *IEEE Access*, vol. 8, pp. 138944–138954, 2020. [DOI / open-access paper](https://doi.org/10.1109/ACCESS.2020.3012699). Focus on the autocorrelation-derivative approximation and off-chip digital correction.

<span id="skew-ref-7"></span>
**[S7] Zero-crossing statistics.** C.-Y. Wang and J.-T. Wu, “A Background Timing-Skew Calibration Technique for Time-Interleaved Analog-to-Digital Converters,” *IEEE TCAS-II: Express Briefs*, vol. 53, no. 4, pp. 299–303, Apr. 2006. [DOI](https://doi.org/10.1109/TCSII.2005.861887), [institutional PDF](https://ir.lib.nycu.edu.tw/bitstream/11536/12403/1/000236891400012.pdf). Read for sampling-sequence randomization, crossing counts, and loop convergence.

<span id="skew-ref-8"></span>
**[S8] Reference-ADC correlation.** M. El-Chammas and B. Murmann, “A 12-GS/s 81-mW 5-bit Time-Interleaved Flash ADC With Background Timing Skew Calibration,” *IEEE JSSC*, vol. 46, no. 4, pp. 838–847, Apr. 2011. [DOI](https://doi.org/10.1109/JSSC.2011.2108125). Read together with B. Murmann and M. El-Chammas, “Background Calibration of Timing Skew in Time-Interleaved A/D Converters,” *SampTA*, 2011 ([author PDF](https://www.el-chammas.com/papers/sampTA2011.pdf)), which explains the coprime reference-clock schedule and correlation objective.

<span id="skew-ref-9"></span>
**[S9] Variance-based reference calibration.** J. Song, K. Ragab, X. Tang, and N. Sun, “A 10-b 800-MS/s Time-Interleaved SAR ADC With Fast Variance-Based Timing-Skew Calibration,” *IEEE JSSC*, vol. 52, no. 10, pp. 2563–2575, Oct. 2017. [DOI](https://doi.org/10.1109/JSSC.2017.2713523), [author page](https://sunlab.ee.tsinghua.edu.cn/zh/publication/jssc_201707_jeonggoo-song_7983356/). Focus on its single-comparator window detector and faster variance estimation; compare the objective with [S8].

<span id="skew-ref-10"></span>
**[S10] Analog derivative and LMS.** D. Stepanović and B. Nikolić, “A 2.8 GS/s 44.6 mW Time-Interleaved ADC Achieving 50.9 dB SNDR and 3 dB Effective Resolution Bandwidth of 1.5 GHz in 65 nm CMOS,” *IEEE JSSC*, vol. 48, no. 4, pp. 971–982, Apr. 2013. [DOI](https://doi.org/10.1109/JSSC.2013.2239005), [author PDF](https://people.eecs.berkeley.edu/~bora/Journals/2013/JSSC2013.pdf). Focus on the two calibration paths, derivative estimate, and timing-control loop.

<span id="skew-ref-11"></span>
**[S11] Background reference injection.** Y. Tao, M. Gu, B. Chi, Y. Zhong, L. Jie, and N. Sun, “22.4 A 4.8GS/s 7-ENoB Time-Interleaved SAR ADC with Dither-Based Background Timing-Skew Calibration and Bit-Distribution-Based Background Ping-Pong Comparator Offset Calibration,” *IEEE ISSCC*, pp. 394–396, 2024. [DOI](https://doi.org/10.1109/ISSCC49657.2024.10454299). Focus on reference modulation, injection location, and cancellation of the injected component.

<span id="skew-ref-12"></span>
**[S12] Global dither injection.** Y. Cao, M. Zhang, Y. Zhu, R. P. Martins, and C.-H. Chan, “A 12-GS/s 12-b 4× Time-Interleaved ADC Using Input-Independent Timing Skew Calibration With Global Dither Injection and Linearized Input Buffer,” *IEEE JSSC*, vol. 59, no. 12, pp. 4211–4224, Dec. 2024. [DOI](https://doi.org/10.1109/JSSC.2024.3482567). Read for the difference between local and global injection and the timing errors each can observe.

<span id="skew-ref-13"></span>
**[S13] All-digital estimation and correction.** S. Chen, L. Wang, H. Zhang, R. Murugesu, D. Dunwell, and A. Chan Carusone, “All-Digital Calibration of Timing Mismatch Error in Time-Interleaved Analog-to-Digital Converters,” *IEEE Transactions on VLSI Systems*, vol. 25, no. 9, pp. 2552–2560, Sept. 2017. [DOI](https://doi.org/10.1109/TVLSI.2017.2703141), [author PDF](https://www.eecg.utoronto.ca/~tcc/Chen_TVLSI17.pdf), [slides](https://www.eecg.utoronto.ca/~tcc/Wang_ISCAS_SLIDES_2018.pdf). Focus on difference-based estimation, derivative-filter correction, and residual SNDR limits.

<span id="skew-ref-14"></span>
**[S14] Early adaptive digital calibration.** S. M. Jamal, D. Fu, N. C.-J. Chang, P. J. Hurst, and S. H. Lewis, “A 10-b 120-Msample/s Time-Interleaved Analog-to-Digital Converter With Digital Background Calibration,” *IEEE JSSC*, vol. 37, no. 12, pp. 1618–1627, Dec. 2002. [DOI](https://doi.org/10.1109/JSSC.2002.804327). Read for correlation-driven adaptive correction of gain and sample-time errors.






## Overlapping versus Non-overlapping track time

![image-20250611224418950](ti-adc/image-20250611224418950.png)



tracking accuracy stay same, Cin (2Cs) counteract the longer tracking



## Summing Interleaved Alias

![image-20240929215841300](ti-adc/image-20240929215841300.png)

The sampling function - impulse train is
$$
s(t) = \sum_{n=-\infty}^{\infty}\left[ \delta(t-n4T_s) + \delta(t-n4T_s-T_s) + \delta(t-n4T_s-2T_s) + \delta(t-n4T_s-3T_s)\right]
$$

Its Fourier transform is
$$\begin{align}
S(f) &= \frac{2\pi}{4T}\sum_{k=-\infty}^{\infty}\left[\delta(f-k\frac{f_s}{4}) + e^{-j2\pi f\cdot T_s}\delta(f-k\frac{f_s}{4}) + e^{-j2\pi f\cdot 2T_s}\delta(f-k\frac{f_s}{4}) + e^{-j2\pi f\cdot 3T_s}\delta(f-k\frac{f_s}{4})  \right] \\
&= \frac{2\pi}{4T}\sum_{k=-\infty}^{\infty}\left(1+e^{-j2\pi\frac{f}{f_s}} + e^{-j4\pi\frac{f}{f_s}} + e^{-j6\pi\frac{f}{f_s}}  \right) \delta(f-k\frac{f_s}{4}) \\
&= \frac{2\pi}{4T}\sum_{k=-\infty}^{\infty}\left(1+e^{-jk\frac{\pi}{2}} + e^{-jk\pi} + e^{-jk\frac{3\pi}{2}}  \right) \delta(f-k\frac{f_s}{4})
\end{align}$$

We define $M[k] = 1+e^{-jk\frac{\pi}{2}} + e^{-jk\pi} + e^{-jk\frac{3\pi}{2}}$, which is periodic, i.e. $M[k]=M[k+4]$
$$
M[k]=\left\{ \begin{array}{cl}
4 & : \ k = 4m \\
0 & : \ k=4m+1 \\
0 & : \ k=4m+2 \\
0 & : \ k=4m+3 \\
\end{array} \right.
$$

That is
$$
S(f) = \frac{2\pi}{T}\sum_{k=-\infty}^{\infty} \delta(f-kf_s)
$$

Alias has same frequency for each slice but **different phase**: Alias terms sum to **zero** if all slices match exactly


## Random Chopping in TI-ADC

![image-20240929215927957](ti-adc/image-20240929215927957.png)



$$
D_n(kT) = (G_n R(kT) V(kT) + O_n)R(kT)= C_n V(kT) + R(kT)O_n
$$





## DNL/INL Benefit

Each sub-ADC has its **own physical capacitor array**, so each slice has its own independent, zero-mean mismatch error

Because the sub-ADC are sampled round-robin, *a busy input signal* visits all $N$ sub-ADC with equal probability over the whole input range. The transfer curve that the *composite* output presents is therefore the **ensemble average**
$$
e_{\mathrm{eff}}(k)
=
\frac{1}{N}\sum_{i=1}^{N} e_i(k)
\quad\Rightarrow\quad
\sigma\!\left\{e_{\mathrm{eff}}(k)\right\}
=
\frac{\sigma\{e_i(k)\}}{\textcolor{red}{\sqrt{N}}}
$$
the measured static DNL/INL genuinely improves by $\sqrt{N}$ at **code-density (histogram)** test

The composite result
$$
\boxed{\sigma_{DNL,\max}^{TI}
=
\frac{\sigma_{\text{sub},DNL}}{\sqrt{N}},
\qquad
\sigma_{INL,\max}^{TI}
=
\frac{\sigma_{\text{sub},INL}}{\sqrt{N}}}
$$
where $N$ is channel number



<span style="color:white; background-color:black">Conventional binary array  sub-SARADC</span>
$$
\sigma_{DNL,\max}=\sqrt{2^n-1}\,\frac{\sigma_u}{C_u}\,[\mathrm{LSB}],
\qquad
\sigma_{INL,\max}=\frac{\sqrt{2^n}}{2}\,\frac{\sigma_u}{C_u}\,[\mathrm{LSB}]
$$
<span style="color:white; background-color:black">VCM-based ($n-1$ bit array)  sub-SARADC</span>

In a VCM-based (top-plate-sampled, tri-level) SAR, the MSB decision needs **no capacitor switching at all** — it's a direct comparison against $V_{CM}$
$$
\sigma^{VCM}_{DNL,\max}
=
\sqrt{2^{n-1}-1}\,\frac{\sigma_u}{C_u},
\qquad
\sigma^{VCM}_{INL,\max}
=
\frac{\sqrt{2^{n-1}}}{2}\,\frac{\sigma_u}{C_u}
\qquad
\text{at } k=2^{n-2},\,3\cdot 2^{n-2}
$$


---

![image-20260913173227688](ti-adc/image-20260913173227688.png)







## reference

Poulton, Ken. ISSCC2009  "Time-Interleaved ADCs, Past and Future" [(slides)](http://poulton.net/papers.public/2009_isscc_se0604_interleaving.pdf)

—. CICC2010 "GHz ADCs: From Exotic to Mainstream", tutorial session, [(slides)](http://poulton.net/papers.public/2010_cicc_GHz_ADCs.pdf)

—. ISSCC2015 "Interleaved ADCs Through the Ages", [(slides)](http://poulton.net/papers.public/2015isscc_interleaved.forum.pdf)

ISSCC2015 F1: High-Speed Interleaved ADCs

Ron Kapusta, Analog Devices, CICC2015 ED007: SAR ADCs in parallel [time-interleaved] converter arrays

Samuel Palermo, ISSCC 2018 T10: ADC-Based Serial Links: Design and Analysis

Ewout Martens. ESSCIRC 2019 Tutorials: Advanced Techniques for ADCs for 5G Massive MIMO [[https://youtu.be/7hYichGGU6k](https://youtu.be/7hYichGGU6k)]

Yohan Frans, CICC2019 ES3-3- "ADC-based Wireline Transceivers" [[pdf](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=8780306)]

John P. Keane, ISSCC2020 T5: "Fundamentals of Time-Interleaved ADCs"

Heng Zhang, Broadcom, ISSCC 2025 Forum *F4.2: High-speed ADCs for 100Gbps+ Wireline Transceivers*

Athanasios Ramkaj. January 26, 2022, IEEE SSCS Santa Clara Valley Section Technical Talk: Design Considerations Towards Optimal High-Resolution Wide-Bandwidth Time-Interleaved ADCs [[video](https://youtu.be/k3jY9NtfYlY)] [[slides](https://r6.ieee.org/scv-sscs/wp-content/uploads/sites/80/2022/02/Thanos-Ramkaj-SCV-Talk-01-26-22.pdf)]

V. Chen, "Tutorial: High-Speed Analog-to-Digital Converters," *2025 IEEE International Solid-State Circuits Conference (ISSCC)*, San Francisco, CA, USA, 2025, pp. 1-1, doi: 10.1109/ISSCC49661.2025.11076112.

---

Ahmed M. A. Ali 2016, "High Speed Data Converters"

Razavi, B. (2025). *Analysis and design of data converters*. Cambridge University Press.

S. Jang, J. Lee, Y. Choi, D. Kim, and G. Kim, "[Recent advances in ultra-high-speed wireline receivers with ADC-DSP-based equalizers](https://ieeexplore.ieee.org/document/10767763)," *IEEE* *Open Journal of the Solid-State Circuits Society* (OJ-SSCS), vol. 4, pp. 290-304, Nov. 2024.

Yida Duan. Design Techniques for Ultra-High-Speed Time-Interleaved Analog-to-Digital Converters (ADCs) [[http://www2.eecs.berkeley.edu/Pubs/TechRpts/2017/EECS-2017-10.pdf](http://www2.eecs.berkeley.edu/Pubs/TechRpts/2017/EECS-2017-10.pdf)]

Preview Lecture #1 - "Extreme SAR ADCs" Online Course (2024) - Prof. Chi-Hang Chan (U. of Macau) [[https://youtu.be/rgMRL4QZ-wA](https://youtu.be/rgMRL4QZ-wA)]

---

oscarmattia. Data Converter Toolbox [[https://github.com/oscarmattia/data_converter_toolbox](https://github.com/oscarmattia/data_converter_toolbox)]
