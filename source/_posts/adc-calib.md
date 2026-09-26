---
title: ADC Characterization & Calibration
date: 2024-08-19 14:50:27
tags:
categories:
- adc-dac
mathjax: true
---

## Figures of Merit (FoMs)

> B. Murmann, "ADC Performance Survey 1997-2022," [Online]. Available: [[https://github.com/bmurmann/ADC-survey](https://github.com/bmurmann/ADC-survey)]
>
> Carsten Wulff, "Advanced Integrated Circuits 2025" [[http://analogicus.com/aic2025/2025/02/20/Lecture-6-Oversampling-and-Sigma-Delta-ADCs.html#high-resolution-fom](http://analogicus.com/aic2025/2025/02/20/Lecture-6-Oversampling-and-Sigma-Delta-ADCs.html#high-resolution-fom)]

![image-20260503082957057](adc-calib/image-20260503082957057.png)

![image-20250825173843550](adc-calib/image-20250825173843550.png)

**Walden FoM unit**: <span style="color:blue">**J/conv-step**</span>



![image-20260503113513018](adc-calib/image-20260503113513018.png)

![image-20260503092050266](adc-calib/image-20260503092050266.png)

For Scherier FoM (DR, SNDR)

![image-20260503110815315](adc-calib/image-20260503110815315.png)

![image-20260503111053594](adc-calib/image-20260503111053594.png)

![image-20260503120427004](adc-calib/image-20260503120427004.png)



![image-20260920225732153](adc-calib/image-20260920225732153.png)

|                             | Wang, ISSCC 24 | Pfaff, ISSCC 24 | Li, ISSCC 24 | Nguyen, ISSCC 24 |
| --------------------------- | -------------- | --------------- | ------------ | ---------------- |
| **Sampling rate (Fs) Gs/s** | 106            | 112             | 105          | 200              |
| **SNDR, hf (dB)**           | 30             | 25.5            | 39.2         | 36.1             |
| **RX Power**                | 288            | 448             | 698          | 400              |
| **FOM,hf (dB)**             | 82.6           | 76.5            | 88.0         | 90.1             |



## Offset & Gain Error

> Kwantae Kim, Integrated Analog Systems D - Lecture 10 (ADC) [[https://youtu.be/IEdbLNJb9wQ](https://youtu.be/IEdbLNJb9wQ)]

![image-20260426180449791](adc-calib/image-20260426180449791.png)

![image-20260426173822772](adc-calib/image-20260426173822772.png)

> ![image-20260426173906024](adc-calib/image-20260426173906024.png)

---

---



![image-20250825151821455](adc-calib/image-20250825151821455.png)

![image-20250825152414651](adc-calib/image-20250825152414651.png)

##  Offset Calibration

**measured** in **digital** domain: **long-term averages** of ADC out

> If the input has a nonzero mean, the output average also contains the signal’s DC component, so it does not identify offset alone

![image-20260925232441699](adc-calib/image-20260925232441699.png)

**corrected** in **analog** domain:  **ADC dynamic range reduction** due to the offset, which holds if we force the offset of each channel to zero rather than make the offsets of different channels equal

> ![image-20260925234147852](adc-calib/image-20260925234147852.png)



---



![image-20260926002408716](adc-calib/image-20260926002408716.png)

The offset-correction DAC here is a switched-capacitor DAC. Its digital code selects which capacitor bottom plates switch between ground and $V_{\mathrm{REF}}$

The op-amp holds the summing node approximately at **virtual ground**. The injected charge is balanced through feedback capacitor $C_2$, causing **$V_{\mathrm{res}}$ to change**.

For an ideal op-amp, the correction-induced output step is

$$
\boxed{\Delta V_{\mathrm{res}} =-\frac{\sum_k C_{D,k}\,\Delta V_{b,k}}{C_2}}
$$

where $C_{D,k}$ are the correction-DAC capacitors and $\Delta V_{b,k}$ are their bottom-plate voltage changes.

Thus, the DAC supplies a digitally controlled **charge correction**, which the MDAC converts into an output-voltage correction.

---

![image-20260926003059811](adc-calib/image-20260926003059811.png)

The correction DAC's bottom plates remain fixed during these trials, but **its capacitance still loads $X$**

neglecting other parasitic capacitances:

$$
G_{Q\rightarrow V,\mathrm{ideal}}=\frac{1}{C_{\mathrm{SAR}}}, \qquad \boxed{G_{Q\rightarrow V,\mathrm{loaded}} =\frac{1}{C_{\mathrm{SAR}}+C_{\mathrm{CALIB}}}}
$$

During a SAR bit trial, switching capacitor $C_k$ by $\Delta V_{b,k}$ therefore produces

$$
\Delta V_X=\frac{C_k\,\Delta V_{b,k}} {C_{\mathrm{SAR}}+C_{\mathrm{CALIB}}}
$$

 Every SAR DAC voltage step is reduced by

$$
\boxed{\alpha=\frac{C_{\mathrm{SAR}}} {C_{\mathrm{SAR}}+C_{\mathrm{CALIB}}}<1}
$$

**the SAR DAC gain decreases, whereas the ADC’s output-code-per-volt gain increases.** In the shown circuit, the sampling switch directly sets $V_X=V_{\mathrm{in}}$, so the sampled input is not attenuated. Smaller DAC steps mean more code is needed to balance the same input:
$$
\boxed{\frac{G_{\mathrm{ADC}}}{G_{\mathrm{ADC,ideal}}} =\frac{1}{\alpha} =1+\frac{C_{\mathrm{CALIB}}}{C_{\mathrm{SAR}}}}
$$



![sar-dac-step-and-adc-gain](adc-calib/sar-dac-step-and-adc-gain.svg)



## Testing

> Kent H. Lundberg "Analog-to-Digital Converter Testing"  [[https://www.mit.edu/~klund/A2Dtesting.pdf](https://www.mit.edu/~klund/A2Dtesting.pdf)]
>
> Tai-Haur Kuo, Da-Huei Lee "Analog IC Design: ADC Measurement" [[http://msic.ee.ncku.edu.tw/course/aic/202309/ch13%20(20230111).pdf](http://msic.ee.ncku.edu.tw/course/aic/202309/ch13%20(20230111).pdf)] [[http://msic.ee.ncku.edu.tw/course/aic/aic.html](http://msic.ee.ncku.edu.tw/course/aic/aic.html)]
>
> ESE 6680: Mixed Signal Design and Modeling "Lec 20: April 10, 2023 Data Converter Testing" [[https://www.seas.upenn.edu/~ese6680/spring2023/handouts/lec20.pdf](https://www.seas.upenn.edu/~ese6680/spring2023/handouts/lec20.pdf)]
>
> Degang Chen. "Distortion Analysis" [[https://class.ece.iastate.edu/djchen/ee435/2017/Lecture25.pdf](https://class.ece.iastate.edu/djchen/ee435/2017/Lecture25.pdf)]

*TODO* &#128197;



## ADCToolbox

> L. Jie and Z. Zhang. ADCToolbox [[https://github.com/Arcadia-1/ADCToolbox](https://github.com/Arcadia-1/ADCToolbox)]



***SNR vs NSD*** — full-scale noise spread over the Nyquist band

![image-20260530172252150](adc-calib/image-20260530172252150.png)

```python
## https://github.com/Arcadia-1/ADCToolbox/blob/main/python/src/adctoolbox/examples/02_spectrum/exp_s01_analyze_spectrum_simplest.py

import numpy as np
import matplotlib.pyplot as plt
from adctoolbox import analyze_spectrum, amplitudes_to_snr, snr_to_nsd

N_fft = 2**13
Fs = 100e6
Fin = 123/N_fft * Fs  # Coherent frequency
t = np.arange(N_fft) / Fs
A = 0.5
noise_rms = 10e-6
signal = 0.5 * np.sin(2*np.pi*Fin*t) + np.random.randn(N_fft) * noise_rms

# --- My own manual cross-check (not in exp_s01_analyze_spectrum_simplest.py) ---
# Hand-derived from first principles to sanity-check the amplitudes_to_snr /
# snr_to_nsd helpers below:
#   SNR = 10*log10( signal_power / noise_power ) = 10*log10( (A^2/2) / noise_rms^2 )
#   NSD = -SNR - 10*log10(Fs/2)  (full-scale noise spread over the Nyquist band)
snr_theroretical = 10*np.log10(A**2/2/noise_rms**2)
print(f"Theoretical SNR: {snr_theroretical:.2f} dB")
nsd_theoretical = -snr_theroretical - 10*np.log10(Fs/2)
print(f"Theoretical NSD: {nsd_theoretical:.2f} dBFS/Hz")
# --- end of my addition ---

snr_ref = amplitudes_to_snr(sig_amplitude=A, noise_amplitude=noise_rms)
nsd_ref = snr_to_nsd(snr_ref, fs=Fs, osr=1)

result = analyze_spectrum(signal, fs=Fs)

print(f"\n[setting] Noise RMS=[{noise_rms*1e6:.2f} uVrms], Theoretical SNR=[{snr_ref:.2f} dB], Theoretical NSD=[{nsd_ref:.2f} dBFS/Hz]")
print(f"[results] ENoB=[{result['enob']:.2f} b], SNDR=[{result['sndr_dbc']:.2f} dB], SFDR=[{result['sfdr_dbc']:.2f} dB], SNR=[{result['snr_dbc']:.2f} dB], NSD=[{result['nsd_dbfs_hz']:.2f} dBFS/Hz]\n")

plt.show()

# Theoretical SNR: 90.97 dB
# Theoretical NSD: -167.96 dBFS/Hz

# [setting] Noise RMS=[10.00 uVrms], Theoretical SNR=[90.97 dB], Theoretical NSD=[-167.96 dBFS/Hz]
# [results] ENoB=[14.82 b], SNDR=[90.99 dB], SFDR=[116.37 dB], SNR=[91.25 dB], NSD=[-168.24 dBFS/Hz]
```





## reference

Aaron Buchwald, ISSCC2010 T1: "Specifying & Testing ADCs"

Ahmed M. A. Ali. ISSCC2021 T5: Calibration Techniques in ADCs

Boris Murmann, ISSCC2022 SC1: Introduction to ADCs/DACs: Metrics, Topologies, Trade Space, and Applications

—， ISSCC2012 SC3: Introduction to ADCs/DACs: Metrics, Topologies, Trade Space, and Applications

—， A/D Converter Figures of Merit and Performance Trends
