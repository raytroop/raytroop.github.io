---
title: Oscillators in Action
date: 2024-12-26 12:36:49
tags:
categories:
- analog
mathjax: true
---

## Temperature compensation for VCO

*Temperature compensation for the VCO oscillation frequency* is a critical issue

*TODO* &#128197;



## Capacitor Bank

> B. Sadhu and R. Harjani, "Capacitor bank design for wide tuning range LC VCOs: 850MHz-7.1GHz (157%)," Proceedings of 2010 IEEE International Symposium on Circuits and Systems, Paris, France, 2010 [[https://sci-hub.st/10.1109/ISCAS.2010.5537040](https://sci-hub.st/10.1109/ISCAS.2010.5537040)]

*TODO* &#128197;

## Perturbation Projection Vector (PPV)

*TODO* &#128197;



> Helene Thibieroz, Customer Support CIC. Using Spectre RF Noise-Aware PLL Methodology to Predict PLL Behavior Accurately  [[https://citeseerx.ist.psu.edu/document?repid=rep1&type=pdf&doi=3056e59ea76165373f90152f915a829d25dabebc](https://citeseerx.ist.psu.edu/document?repid=rep1&type=pdf&doi=3056e59ea76165373f90152f915a829d25dabebc)]
>
> Aditya Varma Muppala. Perturbation Projection Vector (PPV) Theory | Oscillators 11 | MMIC 16 [[https://youtu.be/rbbHfZGT6Jo](https://youtu.be/rbbHfZGT6Jo)]



## Limit Cycles

> ***Nonlinear*** Dynamics

 ![image-20250622202023590](osc-sim/image-20250622202023590.png)



> [[https://adityamuppala.github.io/assets/Notes_YouTube/MMIC_Limit_Cycles.pdf](https://adityamuppala.github.io/assets/Notes_YouTube/MMIC_Limit_Cycles.pdf)]



## ISF assumption

![image-20250626210829173](osc-sim/image-20250626210829173.png)



> [[https://adityamuppala.github.io/assets/Notes_YouTube/Oscillators_ISF_model.pdf](https://adityamuppala.github.io/assets/Notes_YouTube/Oscillators_ISF_model.pdf)]



![image-20250629080430980](osc-sim/image-20250629080430980.png)



## Periodic ISF: Noise Folding

![image-20250629080632902](osc-sim/image-20250629080632902.png)

When performing the ***phase noise computation integral***, there will be a negligible contribution from all terms, other than $n=m$

![image-20250629083344136](osc-sim/image-20250629083344136.png)

> ![image-20250629083453955](osc-sim/image-20250629083453955.png)

Given $i(t) = I_m \cos[(m\omega_0 +\Delta \omega)t]$,

$$\begin{align}
\phi(t) &= \frac{1}{q_\text{max}}\left[\frac{C_0}{2}\int_{-\infty}^t I_m\cos((m\omega_0 +\Delta \omega)\tau)d\tau + \sum_{n=1}^\infty C_n\int_{-\infty}^t I_m\cos((m\omega_0 +\Delta \omega)\tau)\cos(n\omega_0\tau)d\tau\right] \\
&= \frac{I_m}{q_\text{max}}\left[\frac{C_0}{2}\int_{-\infty}^t \cos((m\omega_0 +\Delta \omega)\tau)d\tau + \sum_{n=1}^\infty C_n\int_{-\infty}^t \frac{\cos((m\omega_0 + \Delta \omega+ n\omega_0)\tau)+ \cos((m\omega_0+\Delta \omega - n\omega_0)\tau)}{2}d\tau\right]
\end{align}$$

If $m=0$
$$
\phi(t) \approx \frac{I_0C_0}{2q_\text{max}\Delta \omega}\sin(\Delta\omega t)
$$
If $m\neq 0$ and $m=n$
$$
\phi(t) \approx \frac{I_mC_m}{2q_\text{max}\Delta \omega}\sin(\Delta\omega t)
$$


> $m\omega_0 +\Delta \omega \ge 0$
>
> ![image-20250629105156403](osc-sim/image-20250629105156403.png)



![image-20250629100444702](osc-sim/image-20250629100444702.png)

> A. Hajimiri and T. H. Lee, "A general theory of phase noise in electrical oscillators," in *IEEE Journal of Solid-State Circuits*, vol. 33, no. 2, pp. 179-194, Feb. 1998 
>
> ![image-20250629102112814](osc-sim/image-20250629102112814.png)



### Corrections to "A General Theory of Phase Noise in Electrical Oscillators"

>  A. Hajimiri and T. H. Lee, "Corrections to "A General Theory of Phase Noise in Electrical Oscillators"," in *IEEE Journal of Solid-State Circuits*, vol. 33, no. 6, pp. 928-928, June 1998 [[https://sci-hub.se/10.1109/4.678662](https://sci-hub.se/10.1109/4.678662)]
>
>  Ali Hajimiri. Phase Noise in Oscillators [[http://www-smirc.stanford.edu/papers/Orals98s-ali.pdf](http://www-smirc.stanford.edu/papers/Orals98s-ali.pdf)]
>
>  L. Lu, Z. Tang, P. Andreani, A. Mazzanti and A. Hajimiri, "Comments on “Comments on “A General Theory of Phase Noise in Electrical Oscillators””," in *IEEE Journal of Solid-State Circuits*, vol. 43, no. 9, pp. 2170-2170, Sept. 2008 [[https://sci-hub.se/10.1109/JSSC.2008.2005028](https://sci-hub.se/10.1109/JSSC.2008.2005028)]

![image-20250629104527666](osc-sim/image-20250629104527666.png)

> ![image-20250629081831223](osc-sim/image-20250629081831223.png)



Given $i(t) = I_m \cos[(m\omega_0 - \Delta \omega)t]$ and $m \ge 1$

$$\begin{align}
\phi(t) &= \frac{1}{q_\text{max}}\left[\frac{C_0}{2}\int_{-\infty}^t I_m\cos((m\omega_0 -\Delta \omega)\tau)d\tau + \sum_{n=1}^\infty C_n\int_{-\infty}^t I_m\cos((m\omega_0 -\Delta \omega)\tau)\cos(n\omega_0\tau)d\tau\right] \\
&= \frac{I_m}{q_\text{max}}\left[\frac{C_0}{2}\int_{-\infty}^t \cos((m\omega_0 -\Delta \omega)\tau)d\tau + \sum_{n=1}^\infty C_n\int_{-\infty}^t \frac{\cos((m\omega_0 - \Delta \omega+ n\omega_0)\tau)+ \cos((m\omega_0-\Delta \omega - n\omega_0)\tau)}{2}d\tau\right]
\end{align}$$



If $m\ge 1$ and $m=n$
$$
\phi(t) \approx \frac{I_mC_m}{2q_\text{max}\Delta \omega}\sin(\Delta\omega t)
$$
That is

|                          | $m = 0$                                                      | $m\gt 0$ & $m\omega_0+\Delta \omega$                         | $m\gt 0$ & $m\omega_0-\Delta \omega$                         |
| ------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| $\phi(t)$                | $\frac{I_0C_0}{2q_\text{max}\Delta \omega}\sin(\Delta\omega t)$ | $\frac{I_mC_m}{2q_\text{max}\Delta \omega}\sin(\Delta\omega t)$ | $\frac{I_mC_m}{2q_\text{max}\Delta \omega}\sin(\Delta\omega t)$ |
| $P_{SBC}(\Delta \omega)$ | $10\log(\frac{I_0^2C_0^2}{16q_\text{max}^2\Delta \omega^2})$ | $10\log(\frac{I_m^2C_m^2}{16q_\text{max}^2\Delta \omega^2})$ | $10\log(\frac{I_m^2C_m^2}{16q_\text{max}^2\Delta \omega^2})$ |

$$\begin{align}
\mathcal{L}\{\Delta \omega\} &= 10\log\left(\frac{I_0^2C_0^2}{16q_\text{max}^2\Delta \omega^2} +  2\frac{I_m^2C_m^2}{16q_\text{max}^2\Delta \omega^2}\right) \\
&= 10\log\left(\frac{\overline{i_n^2/\Delta f}\cdot \frac{C_0^2}{2} }{4q_\text{max}^2\Delta \omega^2} + \frac{\overline{i_n^2/\Delta f}\cdot\sum_{m=1}^\infty C_m^2 }{4q_\text{max}^2\Delta \omega^2}\right) \\
&= 10\log \frac{\overline{i_n^2/\Delta f}(C_0^2/2+\sum_{m=1}^\infty C_m^2)}{4q_\text{max}^2\Delta \omega^2} \\
&= 10\log \frac{\overline{i_n^2/\Delta f}\cdot \Gamma_\text{rms}^2}{2q_\text{max}^2\Delta \omega^2}
\end{align}$$




![image-20250629065454831](osc-sim/image-20250629065454831.png)

![image-20250629073305626](osc-sim/image-20250629073305626.png)



> Carlo Samori, Phase Noise in LC Oscillators: From Basic Concepts to Advanced Topologies [[https://www.ieeetoronto.ca/wp-content/uploads/2020/06/DL-VCO-short.pdf](https://www.ieeetoronto.ca/wp-content/uploads/2020/06/DL-VCO-short.pdf)]

## ISF & $1/f$-noise up-conversion

*TODO* &#128197;

![image-20250626211817628](osc-sim/image-20250626211817628.png)



## ISF Simulation

![image-20241113232703941](osc-sim/image-20241113232703941.png)



### PSS + PXF Method

> Yizhe Hu, "A Simulation Technique of Impulse Sensitivity Function (ISF) Based on Periodic Transfer Function (PXF)" [[https://bbs.eetop.cn/thread-869343-1-1.html](https://bbs.eetop.cn/thread-869343-1-1.html)]



*TODO* &#128197;



### Transient Method

> David Dolt. ECEN 620 Network Theory - Broadband Circuit Design: "VCO ISF Simulation" [[https://people.engr.tamu.edu/spalermo/ecen620/ISF_SIM.pdf](https://people.engr.tamu.edu/spalermo/ecen620/ISF_SIM.pdf)]

![image-20241016211020230](osc-sim/image-20241016211020230.png)

![image-20241016211101204](osc-sim/image-20241016211101204.png)

![image-20241016211115630](osc-sim/image-20241016211115630.png)



> To compare the ring oscillator and VCO the **total injected charge** to both should be the **same**



## Tail filter

*TODO* &#128197;

![image-20250808205658082](osc-sim/image-20250808205658082.png)



> P. Liu et al., "A 128Gb/s ADC/DAC Based PAM-4 Transceiver with >45dB Reach in 3nm FinFET," 2025 Symposium on VLSI Technology and Circuits (VLSI Technology and Circuits), Kyoto, Japan, 2025
>
> E. Hegazi, H. Sjoland and A. Abidi, "A filtering technique to lower oscillator phase noise," *2001 IEEE International Solid-State Circuits Conference. Digest of Technical Papers. ISSCC (Cat. No.01CH37177)*, San Francisco, CA, USA, 2001 [[paper](https://engineering.purdue.edu/oxidemems/conferences/isscc2001/DATA/D23_4.pdf), [slides](https://engineering.purdue.edu/oxidemems/conferences/isscc2001/DATA/SS23_4.pdf)]
>
> —, "A filtering technique to lower LC oscillator phase noise," in *IEEE Journal of Solid-State Circuits*, vol. 36, no. 12, pp. 1921-1930, Dec. 2001 [[https://people.engr.tamu.edu/spalermo/ecen620/filtering_tech_lc_osc_hegazi_jssc_2001.pdf](https://people.engr.tamu.edu/spalermo/ecen620/filtering_tech_lc_osc_hegazi_jssc_2001.pdf)]
>
> D. Murphy, H. Darabi and H. Wu, "Implicit Common-Mode Resonance in LC Oscillators," in IEEE Journal of Solid-State Circuits, vol. 52, no. 3, pp. 812-821, March 2017, [[https://sci-hub.st/10.1109/JSSC.2016.2642207](https://sci-hub.st/10.1109/JSSC.2016.2642207)]
>
> —, "25.3 A VCO with implicit common-mode resonance," 2015 IEEE International Solid-State Circuits Conference - (ISSCC) Digest of Technical Papers, San Francisco, CA, USA, 2015 [[https://sci-hub.st/10.1109/ISSCC.2015.7063116](https://sci-hub.st/10.1109/ISSCC.2015.7063116)]
>
> Lecture 16: VCO Phase Noise [[https://people.engr.tamu.edu/spalermo/ecen620/lecture16_ee620_vco_pn.pdf](https://people.engr.tamu.edu/spalermo/ecen620/lecture16_ee620_vco_pn.pdf)]



## Injection Locking

*TODO* &#128197;



---

"Topics in IC (Wireline Transceiver Design): Lec 4 - Injection Locked Oscillators" [[https://ocw.snu.ac.kr/sites/default/files/NOTE/Lec%204%20-%20Injection%20Locked%20Oscillators.pdf](https://ocw.snu.ac.kr/sites/default/files/NOTE/Lec%204%20-%20Injection%20Locked%20Oscillators.pdf)]

Cowan, Glenn. (2024). Mixed-Signal CMOS for Wireline Communication: Transistor-Level and System-Level Design Considerations

Mozhgan Mansuri. ISSCC2021 SC3: Clocking, Clock Distribution, and Clock Management in Wireline/Wireless Subsystems [[https://www.nishanchettri.com/isscc-slides/2021%20ISSCC/SHORT%20COURSE/ISSCC2021-SC3.pdf](https://www.nishanchettri.com/isscc-slides/2021%20ISSCC/SHORT%20COURSE/ISSCC2021-SC3.pdf)]

Aditya Varma Muppala. Oscillator Theory - Injection Locking [[note](https://adityamuppala.github.io/assets/Notes_YouTube/Injection_Locking_YouTube.pdf), [video1](https://youtu.be/uelsciruAXw), [video2](https://youtu.be/kUsH4WhEybI)]

Min-Seong Choo. Review of Injection-Locked Oscillators [[https://journal.theise.org/jse/wp-content/uploads/sites/2/2020/09/JSE-2020-0001.pdf](https://journal.theise.org/jse/wp-content/uploads/sites/2/2020/09/JSE-2020-0001.pdf)]


## capacitance simulation



### VCO varactor

> Two methods: 1. pss + pac; 2. pss+psp

#### PSS + PAC

![image-20220510192206354](osc-sim/image-20220510192206354.png)

pss time domain

![image-20220510192351590](osc-sim/image-20220510192351590.png)

using the **0-harmonic**

![image-20220510192447040](osc-sim/image-20220510192447040.png)

#### PSS + PSP

![image-20220510192753324](osc-sim/image-20220510192753324.png)

using **Y11** of `psp`

![image-20220510192639080](osc-sim/image-20220510192639080.png)

#### comparison

![image-20220510193036717](osc-sim/image-20220510193036717.png)

> which are same

### inverter input

R-C, ***series*** equivalent circuit

![invCap](osc-sim/invCap.png)


### inverter output

R-C, ***parallel*** equivalent circuit



---

#### AC simulation

![image-20250628112910588](osc-sim/image-20250628112910588.png)

@vi = 0

![image-20250628104042741](osc-sim/image-20250628104042741.png)

sweep vi from 0 to 800mV (vdd)

![image-20250628105510374](osc-sim/image-20250628105510374.png)



---

#### SP simulation

![image-20250628112857124](osc-sim/image-20250628112857124.png)

![image-20250628112620876](osc-sim/image-20250628112620876.png)



> EEStream. Cadence - How to find device capacitance - DC simulation, SP simulation and Large-signal SP simulation [[https://www.youtube.com/watch?v=M3zP6eJnONk](https://www.youtube.com/watch?v=M3zP6eJnONk)]
>
> ![image-20250628114414562](osc-sim/image-20250628114414562.png)



## reference

Jiří Lebl. **Notes on Diffy Qs: Differential Equations for Engineers** [[link](https://www.jirka.org/diffyqs/)]

Matt Charnley. **Differential Equations: An Introduction for Engineers** [[link](https://sites.rutgers.edu/matthew-charnley/course-materials/differential-equations-an-introduction-for-engineers/)]

Åström, K.J. & Murray, Richard. (2021). **Feedback Systems: An Introduction for Scientists and Engineers Second Edition** [[https://www.cds.caltech.edu/~murray/books/AM08/pdf/fbs-public_24Jul2020.pdf](https://www.cds.caltech.edu/~murray/books/AM08/pdf/fbs-public_24Jul2020.pdf)]

Strogatz, S.H. (2015). **Nonlinear Dynamics and Chaos: With Applications to Physics, Biology, Chemistry, and Engineering (2nd ed.)**. CRC Press [[https://www.biodyn.ro/course/literatura/Nonlinear_Dynamics_and_Chaos_2018_Steven_H._Strogatz.pdf](https://www.biodyn.ro/course/literatura/Nonlinear_Dynamics_and_Chaos_2018_Steven_H._Strogatz.pdf)]

Cadence Blog, "Resonant Frequency vs. Natural Frequency in Oscillator Circuits"  [[link](https://resources.pcb.cadence.com/blog/2019-resonant-frequency-vs-natural-frequency-in-oscillator-circuits)]

---

Aditya Varma Muppala. Oscillators [[https://youtube.com/playlist?list=PL9Trid0A4Da2fOmYTEjhAnUkGPxyiH7H6&si=ILxn8hfkMYjXW5f4](https://youtube.com/playlist?list=PL9Trid0A4Da2fOmYTEjhAnUkGPxyiH7H6&si=ILxn8hfkMYjXW5f4)]

P.E. Allen - 2003. ECE 6440 - Frequency Synthesizers: Lecture 160 – Phase Noise - II [[https://pallen.ece.gatech.edu/Academic/ECE_6440/Summer_2003/L160-PhNoII(2UP).pdf](https://pallen.ece.gatech.edu/Academic/ECE_6440/Summer_2003/L160-PhNoII(2UP).pdf)]

Y. Hu, T. Siriburanon and R. B. Staszewski, "Intuitive Understanding of Flicker Noise Reduction via Narrowing of Conduction Angle in Voltage-Biased Oscillators," in IEEE Transactions on Circuits and Systems II: Express Briefs, vol. 66, no. 12, pp. 1962-1966, Dec. 2019 [[https://sci-hub.se/10.1109/TCSII.2019.2896483](https://sci-hub.se/10.1109/TCSII.2019.2896483)]

S. Levantino, P. Maffezzoni, F. Pepe, A. Bonfanti, C. Samori and A. L. Lacaita, "Efficient Calculation of the Impulse Sensitivity Function in Oscillators," in IEEE Transactions on Circuits and Systems II: Express Briefs, vol. 59, no. 10, pp. 628-632, Oct. 2012 [[https://sci-hub.se/10.1109/TCSII.2012.2208679](https://sci-hub.se/10.1109/TCSII.2012.2208679)]

S. Levantino and P. Maffezzoni, "Computing the Perturbation Projection Vector of Oscillators via Frequency Domain Analysis," in IEEE Transactions on Computer-Aided Design of Integrated Circuits and Systems, vol. 31, no. 10, pp. 1499-1507, Oct. 2012 [[https://sci-hub.se/10.1109/TCAD.2012.2194493](https://sci-hub.se/10.1109/TCAD.2012.2194493)]

Thomas H. Lee. Linearity, Time-Variation, Phase Modulation and Oscillator Phase Noise [[https://class.ece.iastate.edu/djchen/ee507/PhaseNoiseTutorialLee.pdf](https://class.ece.iastate.edu/djchen/ee507/PhaseNoiseTutorialLee.pdf)]

Y. Hu, T. Siriburanon and R. B. Staszewski, "Oscillator Flicker Phase Noise: A Tutorial," in *IEEE Transactions on Circuits and Systems II: Express Briefs*, vol. 68, no. 2, pp. 538-544, Feb. 2021 [[https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9286468](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9286468)]

Jaeha Kim. Lecture 8. Special Topics: Design Trade -Offs in LC -Tuned Oscillators [[https://ocw.snu.ac.kr/sites/default/files/NOTE/7033.pdf](https://ocw.snu.ac.kr/sites/default/files/NOTE/7033.pdf)]

A. Demir, A. Mehrotra and J. Roychowdhury, "Phase noise in oscillators: a unifying theory and numerical methods for characterization," in *IEEE Transactions on Circuits and Systems I: Fundamental Theory and Applications*, vol. 47, no. 5, pp. 655-674, May 2000 [[https://sci-hub.se/10.1109/81.847872](https://sci-hub.se/10.1109/81.847872)]

---

A. A. Abidi and D. Murphy, "How to Design a Differential CMOS LC Oscillator," in IEEE Open Journal of the Solid-State Circuits Society, vol. 5, pp. 45-59, 2025 [[https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=10818782](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=10818782)]

Akihide Sai, Toshiba. ISSCC 2023 T5: All-digital PLLs From Fundamental Concepts to Future Trends [[https://www.nishanchettri.com/isscc-slides/2023%20ISSCC/TUTORIALS/T5.pdf](https://www.nishanchettri.com/isscc-slides/2023%20ISSCC/TUTORIALS/T5.pdf)]

---

Pietro Andreani. ISSCC 2011 T1: Integrated LC oscillators [[slides](https://www.nishanchettri.com/isscc-slides/2011%20ISSCC/TUTORIALS/ISSCC2011Visuals-T1.pdf),[transcript](https://www.nishanchettri.com/isscc-slides/2011%20ISSCC/TUTORIALS/Transcription_T1.pdf)]

—. ISSCC 2017 F2: Integrated Harmonic Oscillators

—. SSCS Distinguished Lecture: RF Harmonic Oscillators Integrated in Silicon Technologies [[https://www.ieeetoronto.ca/wp-content/uploads/2020/06/DL-Toronto.pdf](https://www.ieeetoronto.ca/wp-content/uploads/2020/06/DL-Toronto.pdf)]

—. ESSCIRC 2019 Tutorials: RF Harmonic Oscillators Integrated in Silicon Technologies [[https://youtu.be/k1I9nP9eEHE?si=fns9mf3aHjMJobPH](https://youtu.be/k1I9nP9eEHE?si=fns9mf3aHjMJobPH)]

Jun Yin. ISSCC 2025  T10:  mm-Wave Oscillator Design

