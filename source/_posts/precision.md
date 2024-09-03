---
title: Precision Techniques
date: 2024-07-17 23:11:07
tags:
categories:
- analog
mathjax: true
---

## Autozeroing

> offset is **sampled** and then subtracted from the input
>
> Measure the offset somehow and then subtract it from the input signal



### Residual Noise of Auto-zeroing

![image-20240826212343905](precision/image-20240826212343905.png)

---



![image-20240826213958740](precision/image-20240826213958740.png)



*pnosie Noise* Type: **timeaverage**

![image-20240826214306376](precision/image-20240826214306376.png)



> sinc filter come from *Zero-Order Hold*
>
> ![Fourier-transform-of-a-rectangle-function-a-and-a-sinc-function-b](precision/Fourier-transform-of-a-rectangle-function-a-and-a-sinc-function-b.png)



## Chopping

> offset is **modulated** away from the signal band and then filtered out
>
> Modulate the offset away from DC and then filter it out

**Good**: Magically reduces offset, 1/f noise, drift

**Bad**: But creates switching spikes, chopper ripple and other artifacts …



### Chopping in the Frequency Domain

> **Square-wave Modulation**
>
> defination of convolution $y(t) = x(t)*h(t)= \int_{-\infty}^{\infty} x(\tau)h(t-\tau)d\tau$
>
> for real signal $H(j\omega)*=H(-j\omega)$


![sq_mod.drawio](precision/sq_mod.drawio.svg)





## Dynamic Element Matching (DEM)

*TODO* &#128197;









## reference

C. C. Enz and G. C. Temes, "Circuit techniques for reducing the effects of op-amp imperfections: autozeroing, correlated double sampling, and chopper stabilization," in Proceedings of the IEEE, vol. 84, no. 11, pp. 1584-1614, Nov. 1996, doi: 10.1109/5.542410. [[http://www2.ing.unipi.it/~a008309/mat_stud/MIXED/archive/2019/Articles/Offset_canc_Enz_Temes_96.pdf](http://www2.ing.unipi.it/~a008309/mat_stud/MIXED/archive/2019/Articles/Offset_canc_Enz_Temes_96.pdf)]

Qinwen Fan, Evolution of precision amplifiers

Kofi Makinwa, ISSCC 2007 Dynamic-Offset Cancellation Techniques in CMOS [[https://picture.iczhiku.com/resource/eetop/sYkywlkpwIQEKcxb.pdf](https://picture.iczhiku.com/resource/eetop/sYkywlkpwIQEKcxb.pdf)]

Kofi Makinwa. Precision Analog Circuit Design: Coping with Variability, [[https://youtu.be/nA_DZtRqrTQ?si=6uyOpJhdnYm3iG9d](https://youtu.be/nA_DZtRqrTQ?si=6uyOpJhdnYm3iG9d)] [[https://youtu.be/uwRpP20Lprc?si=SGPta86jRCdECSob](https://youtu.be/uwRpP20Lprc?si=SGPta86jRCdECSob)]
