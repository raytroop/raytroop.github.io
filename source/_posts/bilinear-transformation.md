---
title: Bilinear Transformation
date: 2023-05-21 10:59:33
tags:
categories:
- dsp
mathjax: true
---



**Bilinear Transformation**, also known as **Bilinear Approximation**,  an algebraic transformation between the variables $s$ and $z$ that maps the entire $j\Omega$-axis in the $s$-plane to *one revolution of the unit circle* in the $z$-plane. 

That is, with this approach, $-\infty \le \Omega \le +\infty$ maps onto $-\pi \le \omega \le +\pi$, the transformation between the continuous-time and discrete-time frequency variables is necessarily **nonlinear**.

With $H_c(s)$ denoting the continuous-time system function and $H(z)$ the discrete-time system function, the bilinear transformation corresponds to replacing $s$ by
$$
s=\frac{2}{T_d}\left( \frac{1-z^{-1}}{1+z^{-1}} \right)
$$


that is,
$$
H(z) = H_c\left( \frac{2}{T_d}\left( \frac{1-z^{-1}}{1+z^{-1}} \right) \right)
$$










## reference

[AN001] Designing from zero an IIR filter in Verilog using biquad structure and bilinear discretization. URL:[https://www.controlpaths.com/articles/an001_designing_iir_biquad_filter_bilinear/](https://www.controlpaths.com/articles/an001_designing_iir_biquad_filter_bilinear/)

Frequency warping using the bilinear transform. URL:[https://www.controlpaths.com/2022/05/09/frequency-warping-using-the-bilinear-transform/](https://www.controlpaths.com/2022/05/09/frequency-warping-using-the-bilinear-transform/)

Digital control loops. Theoretical approach. URL:[https://www.controlpaths.com/2022/02/28/digital-control-loops-theoretical-approach/](https://www.controlpaths.com/2022/02/28/digital-control-loops-theoretical-approach/)

Simulation of DSP algorithms in Verilog. URL:[https://www.controlpaths.com/2023/05/20/simulation-of-dsp-algorithms-in-verilog/](https://www.controlpaths.com/2023/05/20/simulation-of-dsp-algorithms-in-verilog/)

Implementing a digital biquad filter in Verilog. URL:[https://www.controlpaths.com/2021/04/19/implementing-a-digital-biquad-filter-in-verilog/](https://www.controlpaths.com/2021/04/19/implementing-a-digital-biquad-filter-in-verilog/)

Implementing a FIR filter using folding. URL:[https://www.controlpaths.com/2021/05/17/implementing-a-fir-filter-using-folding/](https://www.controlpaths.com/2021/05/17/implementing-a-fir-filter-using-folding/)

Oppenheim, Alan V. and Cram. “Discrete-time signal processing : Alan V. Oppenheim, 3rd edition.” (2011).

Extras: PID Compensator with Bilinear Approximation URL:[https://ctms.engin.umich.edu/CTMS/index.php?aux=Extras_PIDbilin](https://ctms.engin.umich.edu/CTMS/index.php?aux=Extras_PIDbilin)
