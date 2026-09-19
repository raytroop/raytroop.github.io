---
title: PI-based CDR
date: 2025-08-15 22:14:29
tags:
categories:
- link
mathjax: true
---

![image-20260918203511797](pi-cdr/image-20260918203511797.png)

> Wang, Zhaowen. *Efficient and High-Performance Clocking Circuits for High-Speed Data Links*. 2022. Columbia University, PhD dissertation. *Academic Commons*,[[https://academiccommons.columbia.edu/doi/10.7916/g3f1-4e71](https://academiccommons.columbia.edu/doi/10.7916/g3f1-4e71)]

The PI-based architecture decouples the high-frequency clock synthesis and local clock deskew, allowing to optimize the power consumption and circuit area at a system level



## Phase Interpolator (PI)

!!! Clock Edges

And for a phase interpolator, you need those reference clocks to be completely the opposite. Ideally they would be **triangular** shaped

![image-20240821203756602](pi-cdr/image-20240821203756602.png)

> *four input clocks given by the cyan, black, magenta, red*



> John T. Stonick, ISSCC 2011 tutorial. "DPLL Based Clock and Data Recovery"



***kink problem***

![image-20240919223032380](pi-cdr/image-20240919223032380.png)

> B. Razavi, **"The Design of a Phase Interpolator [The Analog Mind],"** IEEE Solid-State Circuits Magazine, Volume. 15, Issue. 4, pp. 6-10, Fall 2023.([https://www.seas.ucla.edu/brweb/papers/Journals/BR_SSCM_4_2023.pdf](https://www.seas.ucla.edu/brweb/papers/Journals/BR_SSCM_4_2023.pdf))



### Predistortion - sinusoidal

the interpolating inverters near the midscale can be made weaker so as to obtain more uniform phase increments. Alternatively, those at the top and bottom of the array can be made stronger

#### Single-Quadrant PI

$$
V_o(t) = m \cdot \sin(\omega t + \frac{\pi}{2}) + p\cdot \sin(\omega t) = m\cdot \cos(\omega t) + p\cdot \sin(\omega t) = \sqrt{m^2+p^2} \sin(\omega t + \phi)
$$

where $\tan \phi = \frac{m}{p} = \frac{1-p}{p}$ and $p = \frac{1}{1+\tan \phi}$



![image-20251016235032393](pi-cdr/image-20251016235032393.png)

```matlab
phi = (32:-1:0)./32*pi/2;
p_ideal = 1./(1+tan(phi));
delta_p_ideal = abs(p_ideal(1:end-1) - p_ideal(2:end));
phi_ideal = atan((1-p_ideal)./p_ideal);


p_lin = (0:1:32)/32;
phi_lin = atan((1-p_lin)./p_lin);
delta_p_lin = abs(p_lin(1:end-1) - p_lin(2:end));


delta_plr_predist = ones(1,11)*0.035;
delta_pm_predist = ones(1,10) * (1-2*sum(delta_plr_predist))/10;
delta_p_predist = [delta_plr_predist delta_pm_predist delta_plr_predist];
p_predist = [0 cumsum(delta_p_predist)];
phi_predist = atan((1-p_predist)./p_predist);


subplot(2,2,1)
plot(phi/pi*180, p_ideal, 'ro-', LineWidth=3)
hold on
plot(phi_lin/pi*180, p_lin, 'bs-', LineWidth=3)
grid on; legend('ideal', 'linear', fontsize=12)
xlabel('Phase'); ylabel('p')

subplot(2,2,2)
plot(phi(1:end-1)/pi*180, delta_p_ideal, 'ro-', LineWidth=3)
hold on
plot(phi_lin(1:end-1)/pi*180, delta_p_lin, 'bs-', LineWidth=3)
plot(phi_predist(1:end-1)/pi*180, delta_p_predist, 'gd-', LineWidth=3)
grid on; legend('ideal', 'linear', 'predistortion', fontsize=12)
xlabel('Phase'); ylabel('\Delta p')

subplot(2,2, [3,4])

plot(0:1:32, phi/pi*180, 'ro-', LineWidth=3)
hold on
plot(0:1:32, phi_lin/pi*180, 'bs-', LineWidth=3)
plot(0:1:32, phi_predist/pi*180, 'gd-', LineWidth=3)
grid on; legend('ideal', 'linear', 'predistortion', fontsize=12)
xlabel('code p'); ylabel('Phase')
```



#### Eight-Quadrant PI

![pi-region.drawio](pi-cdr/pi-region.drawio.svg)
$$\begin{align}
V_o(t) &= m \cdot \sin(\omega t + \frac{\pi}{4}) + p\cdot \sin(\omega t) = \frac{\sqrt{2}}{2}m\cdot \cos(\omega t) + \left( \frac{\sqrt{2}}{2}m + p\right)\cdot \sin(\omega t) \\
&= \sqrt{m^2 + p^2 +\sqrt{2}pm}\cdot \sin(\omega t + \phi)
\end{align}$$

where $\tan\phi = \frac{\sqrt{2}m}{\sqrt{2}m+2p} = \frac{\sqrt{2}-\sqrt{2}p}{\sqrt{2}+(2-\sqrt{2})p}$

![image-20251017002836647](pi-cdr/image-20251017002836647.png)

```matlab
phi = (16:-1:0)./16*pi/4;
p_ideal = 2^0.5*(1-tan(phi))./(2*tan(phi)+2^0.5*(1-tan(phi)));
delta_p_ideal = abs(p_ideal(1:end-1) - p_ideal(2:end));
phi_ideal = atan((2^0.5 - 2^0.5*p_ideal)./(2^0.5 + (2-2^0.5)*p_ideal));


p_lin = (0:1:16)/16;
phi_lin = atan((2^0.5 - 2^0.5*p_lin)./(2^0.5 + (2-2^0.5)*p_lin));
delta_p_lin = abs(p_lin(1:end-1) - p_lin(2:end));


delta_plr_predist = ones(1,4)*0.066;
delta_pm_predist = ones(1,8) * (1-2*sum(delta_plr_predist))/8;
delta_p_predist = [delta_plr_predist delta_pm_predist delta_plr_predist];
p_predist = [0 cumsum(delta_p_predist)];
phi_predist = atan((2^0.5 - 2^0.5*p_predist)./(2^0.5 + (2-2^0.5)*p_predist));


subplot(2,2,1)
plot(phi/pi*180, p_ideal, 'ro-', LineWidth=3)
hold on
plot(phi_lin/pi*180, p_lin, 'bs-', LineWidth=3)
grid on; legend('ideal', 'linear', fontsize=12)
xlabel('Phase'); ylabel('p')

subplot(2,2,2)
plot(phi(1:end-1)/pi*180, delta_p_ideal, 'ro-', LineWidth=3)
hold on
plot(phi_lin(1:end-1)/pi*180, delta_p_lin, 'bs-', LineWidth=3)
plot(phi_predist(1:end-1)/pi*180, delta_p_predist, 'gd-', LineWidth=3)
grid on; legend('ideal', 'linear', 'predistortion', fontsize=12)
xlabel('Phase'); ylabel('\Delta p')

subplot(2,2, [3,4])

plot(0:1:16, phi/pi*180, 'ro-', LineWidth=3)
hold on
plot(0:1:16, phi_lin/pi*180, 'bs-', LineWidth=3)
plot(0:1:16, phi_predist/pi*180, 'gd-', LineWidth=3)
grid on; legend('ideal', 'linear', 'predistortion', fontsize=12)
xlabel('code p'); ylabel('Phase')
```



### Predistortion - square wave

> Weinlader, Daniel, Thomas H. Lee and James A. Gasbarro. "Precision CMOS receivers for VLSI testing applications." (2001). [[https://www-vlsi.stanford.edu/people/alum/pdf/0111_Weinlader_Precision_CMOS_Receivers_.pdf](https://www-vlsi.stanford.edu/people/alum/pdf/0111_Weinlader_Precision_CMOS_Receivers_.pdf)]

![image-20251017213153657](pi-cdr/image-20251017213153657.png)

Suppose $V_i(t) =  1- e^{-\frac{t}{\tau}}$ and $V_q(t) =  1-e^{-\frac{t-\Delta t}{\tau}}$  with $t\ge \Delta t$
$$
\frac{1}{2} = (1-\alpha)\cdot V_i(t) + \alpha \cdot V_q(t)
$$
yield triggering time
$$
t = \tau \ln\left[ 1 + \alpha \left(e^{\frac{\Delta t}{\tau}}-1\right)\right] + \tau \ln 2
$$
Then
$$\begin{align}
\frac{\partial t}{\partial \alpha} &= \tau \frac{e^{\frac{\Delta t}{\tau }}-1}{1+\alpha(e^{\frac{\Delta t}{t}}-1)} \gt 0 \\
\frac{\partial^2 t}{\partial \alpha^2} &= -\tau \frac{\left(e^{\frac{\Delta t}{\tau }}-1\right)^2}{\left(1+\alpha(e^{\frac{\Delta t}{t}}-1)\right)^2} \lt 0
\end{align}$$

As a conclusion, ***heavier weight while $\alpha$ approaching to 1*** in order to improve linearity

![image-20251017220740310](pi-cdr/image-20251017220740310.png)

```python
import numpy as np
import matplotlib.pyplot as plt

tau = 15  # ps
t = np.linspace(6, 56, 500001)

vi = 1- np.exp(-t/tau)
vq = 1 - np.exp(-(t-6)/tau)	# \Detla t = 6

td = []
alpha_list = np.linspace(0, 101, 101,  endpoint=False)/100

plt.figure(figsize=(20,8))
plt.subplot(1, 3, 1)
for alpha in alpha_list:
    viq = (1-alpha) * vi + alpha*vq
    differences  = np.abs((viq - 0.5))
    closest_index = np.argmin(differences)
    t_closest = t[closest_index]
    td.append(t_closest)
    plt.plot(t,viq)
plt.plot([0, 60], [0.5,0.5], '--c', linewidth=3); plt.grid()
plt.xlabel('t', fontsize=14); plt.ylabel('Voltage', fontsize=14)

td = np.array(td) - td[0]
d_td = td[1:] - td[:-1]

plt.subplot(1, 3, 2)
plt.plot(alpha_list, td, 'ro-', linewidth=2)
plt.grid(); plt.xlabel(r'$\alpha$', fontsize=14); plt.ylabel(r'$t_d$', fontsize=14)

plt.subplot(1, 3, 3)
plt.plot(alpha_list[:-1], d_td, 'bo-')
plt.grid(); plt.xlabel(r'$\alpha$', fontsize=14); plt.ylabel(r'$\Delta t_d$', fontsize=14)

plt.show()
```



### Input/Output amplitude

A **constant Output amplitude** is desired because the *swing-dependent delay characteristic* of the CML-to-CMOS (C2C) circuit results in *AM–PM distortion* which eventually manifests as phase nonlinearity


### Current-Mode Phase Interpolator

### Voltage-Mode Phase Interpolator

### Integrating-Mode Phase Interpolator



## Sampling Offset due to PI Nonlinearity

> Wang, Zhaowen. *Efficient and High-Performance Clocking Circuits for High-Speed Data Links*. 2022. Columbia University, PhD dissertation. *Academic Commons*,[[https://academiccommons.columbia.edu/doi/10.7916/g3f1-4e71](https://academiccommons.columbia.edu/doi/10.7916/g3f1-4e71)]

![image-20260919082930453](pi-cdr/image-20260919082930453.png)



Let $T=T_{\mathrm{LSB}}$, and write a PI’s output time as

$$
t(k)=t_{\mathrm{ref}}+[k+I(k)]T
$$

where $I(k)=\mathrm{INL}(k)$, expressed in LSBs. Then

$$
\mathrm{DNL}(k)=\frac{t(k+1)-t(k)}{T}-1 =I(k+1)-I(k)
$$

Thus INL describes the error at a code, while DNL describes the error in one code-to-code step.

<span style="color:white; background-color:black">**1. Why $(0.5+|\mathrm{DNL}_p|)T$?**</span>

For an ideal PI, available phases are spaced by $T$. If the desired transition lies halfway between two available phases, selecting the nearest phase leaves an error of

$$
|E_e|\le \frac{T}{2}
$$

That explains the **$0.5$**

With DNL, a particular step has width

$$
t(k+1)-t(k)=[1+\mathrm{DNL}(k)]T
$$

A larger step means a larger gap in which the desired phase might lie.

The excerpt can be read as budgeting

$$
\underbrace{0.5T}_{\text{nominal quantization}} + \underbrace{|\mathrm{DNL}_p|T}_{\text{nonlinearity allowance}}
$$

But for a monotonic PI that actually selects the nearest available phase, the tighter bound is **half the largest actual step**:

$$
\boxed{|E_e| \le \frac{1+\max_k\mathrm{DNL}(k)}{2}T \le \left(0.5+\frac{|\mathrm{DNL}_p|}{2}\right)T}
$$

So the paper's $0.5+|\mathrm{DNL}_p|$ is a looser bound under this model



<span style="color:white; background-color:black">**2. Why does the data-clock bound become $(1+|\mathrm{DNL}_p|+|\mathrm{INL}_{pp}|)T$?**</span>

$E_e$ and $E_d$ are **timing errors**, measured in seconds—not the clock times themselves

- **$E_e$: edge-sampling clock error** relative to the ideal data-transition time:
  $$
  E_e=t_e-t_{\text{transition}}.
  $$
  
- **$E_d$: data-sampling clock error** relative to the ideal data-sampling time, assumed here to be half a UI after that transition:
  $$
  E_d=t_d-\left(t_{\text{transition}}+\frac{\mathrm{UI}}{2}\right).
  $$

Here $t_e$ and $t_d$ are the **actual sampling times**. A positive error means the clock samples **late**; a negative error means it samples **early**.

Writing $H=\mathrm{UI}/2$, these definitions give

$$
\boxed{E_d=E_e+\underbrace{(t_d-t_e-H)}_{\text{error in edge-to-data spacing}}.}
$$

Let the desired edge-to-data spacing be

$$
H=\frac{\mathrm{UI}}{2},
$$

and let the data-clock code be $k+m$ when the edge-clock code is $k$. Then

$$
t_d-t_e=mT+[I(k+m)-I(k)]T.
$$

Consequently, the data-clock error relative to its ideal sampling position is

$$
\boxed{ E_d = E_e +\underbrace{(mT-H)}_{\text{spacing quantization}} +\underbrace{[I(k+m)-I(k)]T}_{\text{relative INL error}}. }
$$

If $m$ is chosen by rounding $H/T$, then

$$
|mT-H|\le 0.5T.
$$

Combining this with the paper’s edge-clock allowance gives

$$
|E_d| \le \underbrace{(0.5+|\mathrm{DNL}_p|)T}_{\text{edge-clock error}} +\underbrace{0.5T}_{\text{spacing quantization}} +\underbrace{\mathrm{INL}_{pp}T}_{\text{relative INL error}},
$$

which produces the quoted expression.

Using tighter edge-clock bound

$$
|E_d| \le \underbrace{\left(0.5+\frac{|\mathrm{DNL}_p|}{2}\right)T_{\mathrm{LSB}}}_{\text{edge-clock error}} +\underbrace{0.5T_{\mathrm{LSB}}}_{\text{spacing quantization}} +\underbrace{\mathrm{INL}_{pp}T_{\mathrm{LSB}}}_{\text{relative INL error}},
$$

so

$$
\boxed{|E_d|\le \left(1+\frac{|\mathrm{DNL}_p|}{2}+\mathrm{INL}_{pp}\right)T_{\mathrm{LSB}}}
$$



If $H/T$ is an integer—for example, a full-period PI with a number of steps divisible by eight can represent $45^\circ$ exactly—then $mT-H=0$. That extra $0.5T$ is unnecessary. (If the desired edge-to-data spacing is exactly representable by an integer number of PI steps, the spacing-quantization term vanishes, and the constant $1$ becomes $0.5$)



---

The CDR finds an edge-clock code, and the data-clock code is obtained by adding a fixed code offset

With $T=T_{\mathrm{LSB}}$ and $H=\mathrm{UI}/2$:

$$
k_e=k,\qquad m=\operatorname{round}\left(\frac{H}{T}\right),\qquad k_d=k_e+m
$$

Here, $m$ is **a number of PI steps**, not a time. Thus, for an **ideal PI**, the timing relationship is

$$
\boxed{ t_d=t_e+\operatorname{round}\left(\frac{\mathrm{UI}}{2T}\right)T}
$$

The circuit operates continuously: the CDR adjusts $k_e$, and the data-clock code follows as $k_d=k_e+m$. It does not need to measure a numerical value of $t_e$ before generating the data clock.

For **nonlinear PIs**, adding $m$ codes does not necessarily add exactly $mT$ in time. Assuming a common timing reference,

$$
\boxed{ t_d=t_e+mT+ \left[I_d(k_e+m)-I_e(k_e)\right]T}
$$

That last term is precisely the relative INL error we discussed. The subscripts allow the edge and data clocks to come from different PIs.



## Deterministic Jitter due to PI Nonlinearity

![image-20260919083229868](pi-cdr/image-20260919083229868.png)

$$
K_{f,PI} = \frac{1/2^N}{T_m/T_o}\cdot \frac{1}{T_o} = \frac{f_m}{2^N}
$$
![pi-code.drawio](pi-cdr/pi-code.drawio.svg)

---

<span style="color:white; background-color:black">**For DCO**</span>
$$
K_{f,DCO} = \frac{K_T}{T_o}\cdot \frac{1}{T_o} = \frac{K_T}{T_o^2}
$$




## PI vs. PLL based CDR

> PCI Express Jitter Modeling Revision 1.0RD July 14, 2004

![image-20250816121744921](pi-cdr/image-20250816121744921.png)

![image-20260602202522018](pi-cdr/image-20260602202522018.png)
$$
H_1 - \left[H_1(1-H_3) + H_2H_3\right] = (H_1-H_2)H_3
$$





## reference

A. K. Mishra, Y. Li, P. Agarwal and S. Shekhar, "Improving Linearity in CMOS Phase Interpolators," in IEEE Journal of Solid-State Circuits, vol. 58, no. 6, pp. 1623-1635, June 2023 [[pdf](https://sudip.sites.olt.ubc.ca/files/2023/04/77.-Improving_Linearity_in_CMOS_Phase_Interpolators.pdf)]

Cortiula A, Menin D, Bandiziol A, Driussi F, Palestri P. Modeling of Phase-Interpolator-Based Clock and Data Recovery for High-Speed PAM-4 Serial Interfaces. *Electronics*. 2025; [[https://www.mdpi.com/2079-9292/14/10/1979](https://www.mdpi.com/2079-9292/14/10/1979)]

G. Souliotis, A. Tsimpos and S. Vlassis, "Phase Interpolator-Based Clock and Data Recovery With Jitter Optimization," in *IEEE Open Journal of Circuits and Systems*, vol. 4, pp. 203-217, 2023 [[https://ieeexplore.ieee.org/document/10184121](https://ieeexplore.ieee.org/document/10184121)]

B. Razavi, "The Design of a Phase Interpolator [The Analog Mind]," in *IEEE Solid-State Circuits Magazine*, vol. 15, no. 4, pp. 6-10, Fall 2023 [[https://www.seas.ucla.edu/brweb/papers/Journals/BR_SSCM_4_2023.pdf](https://www.seas.ucla.edu/brweb/papers/Journals/BR_SSCM_4_2023.pdf)]
