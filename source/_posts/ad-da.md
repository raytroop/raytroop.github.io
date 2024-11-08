---
title: Data Converter
date: 2024-08-18 14:50:27
tags:
categories:
- analog
mathjax: true
---



## kick-back

kick-back increases CDAC settling time

> *add pre-amp (more power)*







> Lei, Ka Meng & Mak, Pui-In & Martins, R.P.. (2013). Systematic analysis and cancellation of kickback noise in a dynamic latched comparator. Analog Integrated Circuits and Signal Processing. 77. 277-284. 10.1007/s10470-013-0156-1. [[https://rto.um.edu.mo/wp-content/uploads/docs/ruimartins_cv/publications/journalpapers/57.pdf](https://rto.um.edu.mo/wp-content/uploads/docs/ruimartins_cv/publications/journalpapers/57.pdf)]
>
> Figueiredo, Pedro & Vital, João. (2006). Kickback noise reduction techniques for CMOS latched comparators. Circuits and Systems II: Express Briefs, IEEE Transactions on. 53. 541 - 545. 10.1109/TCSII.2006.875308. [[https://sci-hub.se/10.1109/TCSII.2006.875308](https://sci-hub.se/10.1109/TCSII.2006.875308)]
>
> P. M. Figueiredo and J. C. Vital, "Low kickback noise techniques for CMOS latched comparators," 2004 IEEE International Symposium on Circuits and Systems (ISCAS), Vancouver, BC, Canada, 2004, pp. I-537 [[https://sci-hub.se/10.1109/ISCAS.2004.1328250](https://sci-hub.se/10.1109/ISCAS.2004.1328250)]





## bootstrap T/H Switch
![image-20240825222432796](ad-da/image-20240825222432796.png)



> A. Abo et al., "A 1.5-V, 10-bit, 14.3-MS/s CMOS Pipeline Analog-to Digital Converter," IEEE J. Solid-State Circuits, pp. 599, May 1999 [[https://sci-hub.se/10.1109/4.760369](https://sci-hub.se/10.1109/4.760369)]
>
> Dessouky and Kaiser, "Input switch configuration suitable for rail-to-rail operation of switched opamp circuits," Electronics Letters, Jan. 1999. [[https://sci-hub.se/10.1049/EL:19990028](https://sci-hub.se/10.1049/EL:19990028)]

![image-20241108210222043](ad-da/image-20241108210222043.png)



## Quantization Noise

![image-20240825221754959](ad-da/image-20240825221754959.png)

> Quantization noise is less with higher resolution as the input range is divided into a greater number of smaller ranges
>
> This error can be considered a quantization noise with **RMS**

![image-20240925235213137](ad-da/image-20240925235213137.png)

## Quantization is NOT Noise

![image-20241006152621688](ad-da/image-20241006152621688.png)





## ADC INL Testing

![image-20241006211529077](ad-da/image-20241006211529077.png)

![image-20241006195931838](ad-da/image-20241006195931838.png)





## ADC DNL Testing







## DAC DNL Testing

One difference between ADC and DAC is that DAC DNL can be less than -1 LSB

> In a DAC, **DNL < -1LSB** implies **non-monotinicity**

![image-20241006215420568](ad-da/image-20241006215420568.png)



## Bottom plate sampling

> Sample signal at the *"grounded"* side of the capacitor to achieve ***signal independent sampling***

![image-20240825231816582](ad-da/image-20240825231816582.png)

![image-20240825232007848](ad-da/image-20240825232007848.png)

![image-20240825232717342](ad-da/image-20240825232717342.png)

![image-20240825233801855](ad-da/image-20240825233801855.png)

![image-20240825233821389](ad-da/image-20240825233821389.png)

---

![image-20240825233859540](ad-da/image-20240825233859540.png)

> [[https://indico.cern.ch/event/1064521/contributions/4475393/attachments/2355793/4078773/esi_sampling_and_converters2022.pdf](https://indico.cern.ch/event/1064521/contributions/4475393/attachments/2355793/4078773/esi_sampling_and_converters2022.pdf)]



> EE 435 Spring 2024 Analog VLSI Circuit Design - Switched-Capacitor Amplifiers Other Integrated Filters, [https://class.ece.iastate.edu/ee435/lectures/EE%20435%20Lect%2044%20Spring%202008.pdf](https://class.ece.iastate.edu/ee435/lectures/EE%20435%20Lect%2044%20Spring%202008.pdf)



## Hold Mode Feedthrough
![image-20240820204720277](ad-da/image-20240820204720277.png)

![image-20240820204959977](ad-da/image-20240820204959977.png)



> P. Schvan et al., "A 24GS/s 6b ADC in 90nm CMOS," 2008 IEEE International Solid-State Circuits Conference - Digest of Technical Papers, San Francisco, CA, USA, 2008, pp. 544-634
>
> B. Sedighi, A. T. Huynh and E. Skafidas, "A CMOS track-and-hold circuit with beyond 30 GHz input bandwidth," 2012 19th IEEE International Conference on Electronics, Circuits, and Systems (ICECS 2012), Seville, Spain, 2012, pp. 113-116
>
> Tania Khanna, ESE 568: Mixed Signal Circuit Design and Modeling [[https://www.seas.upenn.edu/~ese5680/fall2019/handouts/lec11.pdf](https://www.seas.upenn.edu/~ese5680/fall2019/handouts/lec11.pdf)]




## CDAC intuition

The *charge redistribution capacitor network* is used to sample the input signal and serves as a
digital-to-analog converter (DAC) for creating and subtracting reference voltages

sampling charge
$$
Q = V_{in} C_{tot}
$$
conversion charge
$$
Q = -C_{tot}V_c + V_{ref}C_\Delta
$$
That is
$$
V_c = \frac{C_\Delta}{C_{tot}}V_{ref} - V_{in}
$$

---

CDAC is actually working as a **capacitive divider** during *conversion phase*, the charge of internal node retain (*charge conservation law*)

assuming $\Delta V_i$ is applied to series capacitor $C_1$ and $C_2$

![cap_divider.drawio](ad-da/cap_divider.drawio.svg)
$$
(\Delta V_i - \Delta V_x) C_1 = \Delta V_x \cdot C_2
$$
Then
$$
\Delta V_x = \frac{C_1}{C_1+C_2}\Delta V_i
$$

> $V_x= V_{x,0} + \Delta V_x$



## CDAC settling time

![cdac-tau.drawio](ad-da/cdac-tau.drawio.svg)
$$\begin{align}
V_x(s) &= \frac{C_1+C_2}{RC_1C_2}\cdot \frac{1}{s+\frac{C_1+C_2}{RC_1C_2}}\cdot V_i(s) \\
&= \frac{1}{\tau}\cdot \frac{1}{s+\frac{1}{\tau}}\cdot \frac{1}{s}\\
&=  \frac{1}{\tau}\cdot \tau(\frac{1}{s} - \frac{1}{s+\frac{1}{\tau}})=\frac{1}{s} - \frac{1}{s+\frac{1}{\tau}}
\end{align}$$

inverse Laplace Transform is $V_x(t) = 1 - e^{-t/\tau}$

$$\begin{align}
V_y(s) &= V_x\frac{C_1}{C_1+C_2} \\
&= \frac{C_1}{C_1+C_2} \left(\frac{1}{s} - \frac{1}{s+\frac{1}{\tau}}\right)\\
\end{align}$$

inverse Laplace Transform is $V_y(t) = \frac{C_1}{C_1+C_2}\left(1 - e^{-t/\tau}\right)$

$V_x(t)$ and $V_y(t)$ prove that the settling time is *same*


> $\tau = R\frac{C_1C_2}{C_1+C_2}$, which means usually worst for MSB capacitor (largest)



## CDAC Energy Consumption


$$
E_{Vref} = \int P(t)dt = \int V_{ref} I(t) dt = V_{ref}\int I(t)dt = V_{ref}\cdot \Delta Q
$$


![image-20240922093524720](ad-da/image-20240922093524720.png)

Given $V_{c,0}=\frac{1}{2}V_{ref}-V_{in}$ and $V_{c,1}=\frac{3}{4}V_{ref}-V_{in}$
$$\begin{align}
Q_{b0,0} &= \left(V_{ref} - V_{c,0} \right)\cdot 2C = \left(\frac{1}{2}V_{ref}+V_{in} \right)\cdot 2C \\
Q_{b1,0} &= (0 - V_{c,0})\cdot C = \left(-\frac{1}{2}V_{ref}+V_{in} \right)\cdot C \\
Q_{b0,1} &= \left(V_{ref} - V_{c,1} \right)\cdot 2C = \left(\frac{1}{4}V_{ref}+V_{in} \right)\cdot 2C \\
Q_{b1,1} &= \left(V_{ref} - V_{c,1} \right)\cdot C = \left(\frac{1}{4}V_{ref}+V_{in} \right)\cdot C
\end{align}$$

Therefore
$$
E_{Vref} = V_{ref}\cdot (Q_{b0,1}+Q_{b1,1} - Q_{b0,0}-Q_{b1,0}) = \frac{1}{4}C V_{ref}^2
$$


---

CDAC total energy change
$$\begin{align}
\Delta E_{tot} &= \frac{1}{2}\cdot 2C \cdot (U_{2c,1}^2  - U_{2c,0}^2) + \frac{1}{2}\cdot C \cdot (U_{c,1}^2  - U_{c,0}^2) + \frac{1}{2}\cdot C \cdot (U_{c1,1}^2  - U_{c1,0}^2) \\
&= \left(-\frac{3}{16}V_{ref}^2 - \frac{1}{2}V_{ref}V_{in} - \frac{3}{32}V_{ref}^2+\frac{3}{4}V_{ref}V_{vin} + \frac{5}{32}V_{ref}^2-\frac{1}{4}V_{ref}V_{in}\right)C \\
&= -\frac{1}{8}CV_{ref}^2
\end{align}$$



***alternative method***

![CapEnergy.drawio](ad-da/CapEnergy.drawio.svg)
$$
\Delta E_{tot} = \frac{1}{2}\cdot\frac{3}{4}C\cdot V_{ref}^2  -  \frac{1}{2}\cdot C\cdot V_{ref}^2 = -\frac{1}{8}CV_{ref}^2
$$


> The total energy decreases by $-\frac{1}{8}CV_{ref}^2$, though $V_{ref}$ provides $\frac{1}{4}C V_{ref}^2$



---

The charge redistribution change the CDAC energy

![cap_redis_energy.drawio](ad-da/cap_redis_energy.drawio.svg)


$$
E_{c,0} = \frac{1}{2}CV^2
$$
After charge redistribution
$$
E_{c,1} = \frac{1}{2}\cdot 2C\cdot \left(\frac{1}{2}V\right)^2 = \frac{1}{4}CV^2
$$

> That make sense, **charge redistribution consume energy**





## Comparator input cap impact

![image-20240907194621524](ad-da/image-20240907194621524.png)
$$
-V_{in}\cdot 2^N C = V_c (2^N C + C_p)
$$
Then $V_c = -\frac{2^N C}{2^N C + C_p}V_{in}$, i.e. this capacitance reduce the voltage amplitude by the factor

During conversion
$$\begin{align}
V_c &= -\frac{2^N C}{2^N C + C_p}V_{in} +V_{ref}\sum_{n=0}^{N-1} \frac{b_n\cdot2^n C}{2^N C + C_p} \\
&= \frac{2^N C}{2^N C + C_p}\left(-V_{in} + V_{ref}\sum_{n=0}^{N-1}\frac{b_n }{2^{N-n}}  \right)
\end{align}$$

That is, it does not change the sign



## Summing Interleaved Alias

![image-20240929215841300](ad-da/image-20240929215841300.png)

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


> John P. Keane, ISSCC2020, T5: "Fundamentals of Time-Interleaved ADCs"



## Random Chopping in TI-ADC

![image-20240929215927957](ad-da/image-20240929215927957.png)



$$
D_n(kT) = (G_n R(kT) V(kT) + O_n)R(kT)= C_n V(kT) + R(kT)O_n
$$




## SNR of an ADC Due to Clock Jitter

*TODO* &#128197;





> K. Tyagi and B. Razavi, "Performance Bounds of ADC-Based Receivers Due to Clock Jitter," in *IEEE Transactions on Circuits and Systems II: Express Briefs*, vol. 70, no. 5, pp. 1749-1753, May 2023 [[https://www.seas.ucla.edu/brweb/papers/Journals/KT_TCAS_2023.pdf](https://www.seas.ucla.edu/brweb/papers/Journals/KT_TCAS_2023.pdf)]
>
> N. Da Dalt, M. Harteneck, C. Sandner and A. Wiesbauer, "On the jitter requirements of the sampling clock for analog-to-digital converters," in *IEEE Transactions on Circuits and Systems I: Fundamental Theory and Applications*, vol. 49, no. 9, pp. 1354-1360, Sept. 2002 [[https://sci-hub.se/10.1109/TCSI.2002.802353](https://sci-hub.se/10.1109/TCSI.2002.802353)]





## reference

Aaron Buchwald, ISSCC2010 T1: "Specifying & Testing ADCs" [[https://www.nishanchettri.com/isscc-slides/2010%20ISSCC/Tutorials/T1.pdf](https://www.nishanchettri.com/isscc-slides/2010%20ISSCC/Tutorials/T1.pdf)]

John P. Keane, ISSCC2020, T5: "Fundamentals of Time-Interleaved ADCs" [[https://www.nishanchettri.com/isscc-slides/2020%20ISSCC/TUTORIALS/T5Visuals.pdf](https://www.nishanchettri.com/isscc-slides/2020%20ISSCC/TUTORIALS/T5Visuals.pdf)]

Chembiyan T, "SNR of an ADC in the presence of clock jitter" [[https://www.linkedin.com/posts/chembiyan-t-0b34b910_adcsnrjitter-activity-7171178121021304833-f2Wd?utm_source=share&utm_medium=member_desktop](https://www.linkedin.com/posts/chembiyan-t-0b34b910_adcsnrjitter-activity-7171178121021304833-f2Wd?utm_source=share&utm_medium=member_desktop)]

---

everynanocounts. Memos on FFT With Windowing. URL: [https://a2d2ic.wordpress.com/2018/02/01/memos-on-fft-with-windowing/](https://a2d2ic.wordpress.com/2018/02/01/memos-on-fft-with-windowing/)

How to choose FFT depth for ADC performance analysis (SINAD, ENOB). URL:[https://dsp.stackexchange.com/a/38201](https://dsp.stackexchange.com/a/38201)

Computation of Effective Number of Bits, Signal to Noise Ratio, & Signal to Noise & Distortion Ratio Using FFT. URL:[https://cdn.teledynelecroy.com/files/appnotes/computation_of_effective_no_bits.pdf](https://cdn.teledynelecroy.com/files/appnotes/computation_of_effective_no_bits.pdf)

Kester, Walt. (2009). Understand SINAD, ENOB, SNR, THD, THD + N, and SFDR so You Don't Get Lost in the Noise Floor. URL:[https://www.analog.com/media/en/training-seminars/tutorials/MT-003.pdf](https://www.analog.com/media/en/training-seminars/tutorials/MT-003.pdf)

T. C. Hofner: Dynamic ADC testing part I. Defining and testing dynamic ADC parameters, Microwaves & RF, 2000, vol. 39, no. 11, pp. 75-84,162

T. C. Hofner: Dynamic ADC testing part 2. Measuring and evaluating dynamic line parameters, Microwaves & RF, 2000, vol. 39, no. 13, pp. 78-94

AN9675: A Tutorial in Coherent and Windowed Sampling with A/D Converters [https://www.renesas.com/us/en/document/apn/an9675-tutorial-coherent-and-windowed-sampling-ad-converters](https://www.renesas.com/us/en/document/apn/an9675-tutorial-coherent-and-windowed-sampling-ad-converters)

APPLICATION NOTE 3190: Coherent Sampling Calculator (CSC)  [https://www.stg-maximintegrated.com/en/design/technical-documents/app-notes/3/3190.html](https://www.stg-maximintegrated.com/en/design/technical-documents/app-notes/3/3190.html)

Coherent Sampling (Very Brief and Simple) [https://www.dsprelated.com/thread/469/coherent-sampling-very-brief-and-simple](https://www.dsprelated.com/thread/469/coherent-sampling-very-brief-and-simple)

Signal Chain Basics #160: Making sense of coherent and noncoherent sampling in data-converter testing [https://www.planetanalog.com/signal-chain-basics-160-making-sense-of-coherent-and-noncoherent-sampling-in-data-converter-testing/](https://www.planetanalog.com/signal-chain-basics-160-making-sense-of-coherent-and-noncoherent-sampling-in-data-converter-testing/)

Signal Chain Basics #104: Understanding noise in ADCs [https://www.planetanalog.com/signal-chain-basics-part-104-understanding-noise-in-adcs/](https://www.planetanalog.com/signal-chain-basics-part-104-understanding-noise-in-adcs/)

Signal Chain Basics #101: ENOB Degradation Analysis Over Frequency Due to Jitter [https://www.planetanalog.com/signal-chain-basics-part-101-enob-degradation-analysis-over-frequency-due-to-jitter/](https://www.planetanalog.com/signal-chain-basics-part-101-enob-degradation-analysis-over-frequency-due-to-jitter/)

Clock jitter analyzed in the time domain, Part 1, Texas Instruments Analog Applications Journal (slyt379), Aug 2010 [https://www.ti.com/lit/an/slyt379/slyt379.pdf](https://www.ti.com/lit/an/slyt379/slyt379.pdf)

Clock jitter analyzed in the time domain, Part 2  [https://www.ti.com/lit/slyt389](https://www.ti.com/lit/slyt389)

Measurement of Total Harmonic Distortion and Its Related Parameters using Multi-Instrument [[pdf](https://www.virtins.com/doc/Measurement-of-Total-Harmonic-Distortion-and-Its-Related-Parameters-using-Multi-Instrument.pdf)]

Application Note AN-4: Understanding Data Converters' Frequency Domain Specifications [[pdf](https://www.datel.com/data/ads/adc-an4.pdf)]

Belleman, J. (2008). From analog to digital. 10.5170/CERN-2008-003.131.  [[pdf](https://cds.cern.ch/record/1100535/files/p131.pdf)]

HandWiki. Coherent sampling [[link](https://handwiki.org/wiki/Coherent_sampling)]

Luis Chioye, TI.  Leverage coherent sampling and FFT windows when evaluating SAR ADCs (Part 1) [[link](https://e2e.ti.com/blogs_/archives/b/precisionhub/posts/leverage-coherent-sampling-and-fft-windows-when-evaluating-sar-adcs-part-1)]

Coherent Sampling vs. Window Sampling | Analog Devices [https://www.analog.com/en/technical-articles/coherent-sampling-vs-window-sampling.html](https://www.analog.com/en/technical-articles/coherent-sampling-vs-window-sampling.html)

Understanding Effective Number of Bits [https://robustcircuitdesign.com/signal-chain-explorer/understanding-effective-number-of-bits/](https://robustcircuitdesign.com/signal-chain-explorer/understanding-effective-number-of-bits/)

ADC Input Noise: The Good, The Bad, and The Ugly. Is No Noise Good Noise? [[https://www.analog.com/en/resources/analog-dialogue/articles/adc-input-noise.html](https://www.analog.com/en/resources/analog-dialogue/articles/adc-input-noise.html)]

Walt Kester, Taking the Mystery out of the Infamous Formula, "SNR = 6.02N + 1.76dB," and Why You Should Care [[https://www.analog.com/media/en/training-seminars/tutorials/MT-001.pdf](https://www.analog.com/media/en/training-seminars/tutorials/MT-001.pdf)]

Dan Boschen, "How to choose FFT depth for ADC performance analysis (SINAD, ENOB)", [[https://dsp.stackexchange.com/a/38201](https://dsp.stackexchange.com/a/38201)]

