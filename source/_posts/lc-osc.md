---
title: LC Oscillator
date: 2025-10-10 21:04:49
tags:
categories:
- osc
mathjax: true
---

## 8-shaped inductor

> NXP BV, US8183971B2, *8-shaped inductor* [[pdf](https://patentimages.storage.googleapis.com/41/b1/ff/e53534a029c34d/US8183971.pdf)]
>
> Marvell, US9077310B2, *Pseudo-8-shaped inductor* [[pdf](https://patentimages.storage.googleapis.com/36/ad/f1/d8b740bb7b80d9/US9697938.pdf)]
> 
> P. Guan et al., "8-Shaped Inductors: An Essential Addition to RFIC Designers' Toolbox," in IEEE Open Journal of the Solid-State Circuits Society, vol. 4, pp. 131-146, 2024 [[pdf](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=10668829)]
>
> M. Pisati et al., "A 243-mW 1.25–56-Gb/s Continuous Range PAM-4 42.5-dB IL ADC/DAC-Based Transceiver in 7-nm FinFET," in IEEE Journal of Solid-State Circuits, vol. 55, no. 1, pp. 6-18, Jan. 2020 [[https://sci-hub.ru/10.1109/JSSC.2019.2936307](https://sci-hub.ru/10.1109/JSSC.2019.2936307)]

An **8-shaped (figure-8) inductor** is a specialized on-chip, high-Q component used to mitigate **electromagnetic coupling** and reduce **frequency pulling** in VCOs by generating opposing, self-canceling magnetic fields

*TODO* &#128197;

![image-20260511195827682](lc-osc/image-20260511195827682.png)



---

> Zou, Wei & Zou, Xuecheng & Ren, Daming & Zhang, Kefeng & Liu, Dongsheng & Ren, Zhixiong. (2019). 2.49-4.91 GHz wideband VCO with optimised 8-shaped inductor. Electronics Letters. [[https://sci-hub.jp/10.1049/el.2018.6012](https://sci-hub.jp/10.1049/el.2018.6012)]

![image-20260511230451153](lc-osc/image-20260511230451153.png)






## Capacitor Bank

> B. Sadhu and R. Harjani, "Capacitor bank design for wide tuning range LC VCOs: 850MHz-7.1GHz (157%)," Proceedings of 2010 IEEE International Symposium on Circuits and Systems, Paris, France, 2010 [[https://sci-hub.st/10.1109/ISCAS.2010.5537040](https://sci-hub.st/10.1109/ISCAS.2010.5537040)]

*TODO* &#128197;

![image-20251025222240141](lc-osc/image-20251025222240141.png)

>  large value KVCO is not favorable due to noise and possibly spurs at the control voltage



![image-20251026003354263](lc-osc/image-20251026003354263.png)

![image-20251026003228152](lc-osc/image-20251026003228152.png)




## LC Tank Q

![image-20260620145624711](lc-osc/image-20260620145624711.png)



![image-20260619143617541](lc-osc/image-20260619143617541.png)


---

---

***Definitions of Q***

![image-20251012100732881](lc-osc/image-20251012100732881.png)

Assuming **RLC** oscillator waveform is $V(t)=V_0\sin\omega_0 t$, $\omega_0 = \frac{1}{\sqrt{LC}}$ is resonant frequency

Energy stored
$$
E_t = \frac{1}{2}LI_0^2 = \frac{1}{2}CV_0^2
$$
Energy Dissipated per Cycle
$$
E_d = \frac{V_0^2}{2R}\frac{2\pi}{\omega_0}
$$
For $Q_4$, with $I_0=C\omega_0V_0$
$$
\boxed{Q_4  = 2\pi\frac{E_s}{E_d} = R\omega_0C = \frac{R}{\omega_0L}}
$$

which holds **at resonance**

![image-20251012100816733](lc-osc/image-20251012100816733.png)

For $Q_3$, suppose RLC tank is driven by $V_o\cos \omega t$ voltage source, then

*Peak Magnetic Energy*
$$
E_{pL} = \frac{1}{2}LI_0^2 = \frac{1}{2}L\left(\frac{V_0}{L\omega}\right)^2
$$
*Peak Electric Energy*
$$
E_{pC} = \frac{1}{2}CV_0^2
$$
with *Energy Lost per Cycle* $E_d = \frac{V_0^2}{2R}\frac{2\pi}{\omega_0}$, we have
$$
Q_3 = \frac{E_{pL} - E_{pC}}{E_d} = \left(\frac{1}{L\omega^2}-C\right)R\omega=\frac{R}{L\omega}\left(1 - \frac{\omega^2}{\omega^2_{SR}}\right)
$$

![image-20251012100931217](lc-osc/image-20251012100931217.png)



---

> EEE 211 ANALOG ELECTRONICS [[https://www.ee.bilkent.edu.tr/~eee211/LectureNotes/Chapter%20-%2004.pdf](https://www.ee.bilkent.edu.tr/~eee211/LectureNotes/Chapter%20-%2004.pdf)]

![image-20251213164211248](lc-osc/image-20251213164211248.png)

---

---

***Tank Impedance Near Resonance***

![image-20260620150838359](lc-osc/image-20260620150838359.png)

![image-20260620151219168](lc-osc/image-20260620151219168.png)
$$
\boxed{|Z(\omega_0\pm \omega_m)|^2 \cong \frac{1}{(2\omega_m C)^2}}\qquad\qquad \boxed{|Z(\omega_0\pm \omega_m)|^2 \cong R^2\left(\frac{\omega_0}{2Q\omega_m}\right)^2}
$$





## Output Amplitude

> Edgar Sanchez-Sinencio. ECEN 665, OSCILLATORS [[https://people.engr.tamu.edu/s-sanchez/665%20Oscillators.pdf](https://people.engr.tamu.edu/s-sanchez/665%20Oscillators.pdf)]



### NMOS Realization

![image-20251027223026549](lc-osc/image-20251027223026549.png)

*common mode current don't contribute to output amplitude*

---

![image-20251026105512862](lc-osc/image-20251026105512862.png)

> ![image-20251026122015538](lc-osc/image-20251026122015538.png)

---



![image-20251026121057564](lc-osc/image-20251026121057564.png)

```matlab
L0 = 1e-9 * 2;
RL0 = 0.25133 * 2;
C0 = 6.333e-12 / 2;
RC0 = 0.50264 * 2;

w0 = 1/sqrt(L0*C0);   % 12.566 Grad/s

QL = w0*L0/RL0;       % 50
QC = 1/(w0*C0)/RC0;   % 25

RLp0 = QL^2 * RL0;
RCp0 = QC^2 * RC0;
Rp = RLp0 * RCp0 / (RLp0 + RCp0);  % 418.8576 Ohm
Qtot_by_L = Rp/(w0*L0);    % 16.6664
Qtot_by_C = Rp*(w0*C0);    % 16.6664

I0 = 0.5e-3;
vp_p = 2/pi * I0 * Rp/2;     % 66.6633 mV

%%%% compute Qtot from simulation waveform
vp_p2p_sim = 132.8e-3;
Qtot_calc_L0 = vp_p2p_sim*pi/2/I0/(w0*L0);   % 16.6006
Qtot_calc_C0 = vp_p2p_sim*pi/2/I0*(w0*C0);   % 16.6006
```

### CMOS Realization

![image-20251027223323689](lc-osc/image-20251027223323689.png)

Owing to switch-off PMOS eliminating common mode current, all $I_T$ is differentially flowing in the tank.

![image-20251028211854604](lc-osc/image-20251028211854604.png)

---

![image-20251026122550988](lc-osc/image-20251026122550988.png)



> ![image-20251026122231321](lc-osc/image-20251026122231321.png)

### current limited vs voltage limited

![image-20251027215143039](lc-osc/image-20251027215143039.png)

![image-20251027215225227](lc-osc/image-20251027215225227.png)

![image-20251026121829983](lc-osc/image-20251026121829983.png)



## Cross-coupled Pair

![image-20251027224751015](lc-osc/image-20251027224751015.png)



?? Triode MOS noise



---



![image-20260618064000970](lc-osc/image-20260618064000970.png)

phase noise is independent of the transconductance of the transistors

![image-20260618063842453](lc-osc/image-20260618063842453.png)



## conduction angle

*TODO* &#128197;



## Current-biased & voltage-biased DCO

> S. Gallucci *et al*., "A Low-Noise Digital PLL With an Adaptive Common-Mode Resonance Tuning Technique for Voltage-Biased Oscillators," in *IEEE Journal of Solid-State Circuits*, vol. 60, no. 12, pp. 4572-4586, Dec. 2025

*TODO* &#128197;

![image-20260106224228115](lc-osc/image-20260106224228115.png)



## LC-VCO Temperature Sensitivities

> A. L. S. Loke *et al*., "A versatile low-jitter PLL in 90-nm CMOS for SerDes transmitter clocking," *Proceedings of the IEEE 2005 Custom Integrated Circuits Conference, 2005.*, San Jose, CA, USA, 2005 [[slides](https://ewh.ieee.org/r5/denver/sscs/Presentations/2005_09_Loke.pdf), [paper](https://sci-hub.se/10.1109/CICC.2005.1568728)]

![image-20251213154802429](lc-osc/image-20251213154802429.png)


$$
f=\frac{1}{2\pi\sqrt{L_p C_p}} = \frac{1}{2\pi\sqrt{L_s\frac{Q_L^2+1}{Q_L^2} C_s\frac{Q_C^2}{Q_C^2+1}}} = \frac{1}{2\pi\sqrt{L_sC_s}}\cdot \sqrt{\frac{1+1/Q_c^2}{1+1/Q_L^2}}
$$
Assuming the tank's Q is limited by the inductor's quality factor $Q_L$, i.e. $Q_L\ll Q_c$
$$
f\approx  \frac{1}{2\pi\sqrt{L_sC_s}}\cdot \sqrt{1-\frac{1}{Q_L^2}} =f_0\cdot\sqrt{1-\frac{1}{Q_L^2}}
$$
where $f_0=\frac{1}{\sqrt{L_sC_s}}$ is the first order approximation of the resonant frequency

![image-20251213161312529](lc-osc/image-20251213161312529.png)





## simulation in oscillator

### varactor simulation

Three methods:

- PSS +PSP (*pay attention to port termination and voltage amplitude*)
- PSS +PAC
- PSS Only

![image-20251026155903015](lc-osc/image-20251026155903015.png)

![image-20251026160758494](lc-osc/image-20251026160758494.png)

![image-20251026160408516](lc-osc/image-20251026160408516.png)



---

`rms` only scale magnitude $1/\sqrt{2}$ but retain phase for complex number, like harmonic

- `mag(vh('pss "/P5"))` = `mag(rms(vh('pss "/P5"))) * (2**0.5)` 
- `phaseDegUnwrapped(vh('pss "/P5"))` = `phaseDegUnwrapped(rms(vh('pss "/P5")))`

![image-20251026155120102](lc-osc/image-20251026155120102.png)





## reference

A. A. Abidi and D. Murphy, "How to Design a Differential CMOS LC Oscillator," in IEEE Open Journal of the Solid-State Circuits Society, vol. 5, pp. 45-59, 2025 [[https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=10818782](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=10818782)]

Pietro Andreani. ISSCC 2011 T1: Integrated LC oscillators

—. ISSCC 2017 F2: Integrated Harmonic Oscillators

—. SSCS Distinguished Lecture: RF Harmonic Oscillators Integrated in Silicon Technologies [[https://www.ieeetoronto.ca/wp-content/uploads/2020/06/DL-Toronto.pdf](https://www.ieeetoronto.ca/wp-content/uploads/2020/06/DL-Toronto.pdf)]

—. ESSCIRC 2019 Tutorials: RF Harmonic Oscillators Integrated in Silicon Technologies [[https://youtu.be/k1I9nP9eEHE](https://youtu.be/k1I9nP9eEHE)]

—. "Harmonic Oscillators in CMOS—A Tutorial Overview," in IEEE Open Journal of the Solid-State Circuits Society, vol. 1, pp. 2-17, 2021 [[pdf](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9530265)]

C. Samori, "Tutorial: Understanding Phase Noise in LC VCOs," *2016 IEEE International Solid-State Circuits Conference (ISSCC)*, San Francisco, CA, USA, 2016

—, "Understanding Phase Noise in LC VCOs: A Key Problem in RF Integrated Circuits," in *IEEE Solid-State Circuits Magazine*, vol. 8, no. 4, pp. 81-91, Fall 2016 [[https://sci-hub.se/10.1109/MSSC.2016.2573979](https://sci-hub.se/10.1109/MSSC.2016.2573979)]

—, Phase Noise in LC Oscillators: From Basic Concepts to Advanced Topologies [[https://www.ieeetoronto.ca/wp-content/uploads/2020/06/DL-VCO-short.pdf](https://www.ieeetoronto.ca/wp-content/uploads/2020/06/DL-VCO-short.pdf)]

Jun Yin. ISSCC 2025  T10:  mm-Wave Oscillator Design

---

Razavi, Behzad. RF Microelectronics. 2nd ed. Prentice Hall, 2012. [[pdf](https://picture.iczhiku.com/resource/eetop/WYKgsQqKzSDpFmbM.pdf)]

Lacaita, Andrea Leonardo, Salvatore Levantino, and Carlo Samori. *Integrated frequency synthesizers for wireless systems*. Cambridge University Press, 2007

M. Babaie, M. Shahmohammadi, R. B. Staszewski, (2019) "*RF CMOS Oscillators for Modern Wireless Applications"* River Publishers [[https://www.riverpublishers.com/pdf/ebook/RP_E9788793609488.pdf](https://www.riverpublishers.com/pdf/ebook/RP_E9788793609488.pdf)]

Manetakis, K. (2023). *Topics in LC Oscillators: Principles, phase noise, pulling, inductor design*. Springer Nature Switzerland Springer. [[eetop link](https://bbs.eetop.cn/thread-974577-1-1.html)]
