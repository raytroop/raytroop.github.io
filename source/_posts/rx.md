---
title: Wireline Receiver
date: 2025-06-07 10:31:43
tags:
categories:
- analog
mathjax: true
---



## DFE Error Propagation

*TODO* &#128197;

![image-20250609201647012](rx/image-20250609201647012.png)





> Geoff Zhang. Preliminary Studies on DFE Error Propagation, Precoding, and their Impact on KP4 FEC Performance for PAM4 Signaling Systems [[https://www.ieee802.org/3/ck/public/18_09/zhang_3ck_01a_0918.pdf](https://www.ieee802.org/3/ck/public/18_09/zhang_3ck_01a_0918.pdf)]



## CTLE transfer function

![image-20250609201257138](rx/image-20250609201257138.png)

> Circuit Insights @ ISSCC2025: Circuits for Wireline Communications - Kevin Zheng [[https://youtu.be/8NZl81Dj45M?si=J11oGnXnkJYPUi2n&t=1045](https://youtu.be/8NZl81Dj45M?si=J11oGnXnkJYPUi2n&t=1045)]



## DFE architecture

![image-20250609201522455](rx/image-20250609201522455.png)

![image-20250607235201147](rx/image-20250607235201147.png)

Extensive work on DFEs has produced a multitude of architectures, which can be broadly categorized as "**direct**"" or "**unrolled**" (**speculative**) DFEs with "**full-rate**" or "**half-rate**" clocking



![image-20250608000306928](rx/image-20250608000306928.png)

![image-20250608000338808](rx/image-20250608000338808.png)

![image-20250608000357010](rx/image-20250608000357010.png)





> S. Ibrahim and B. Razavi, "Low-Power CMOS Equalizer Design for 20-Gb/s Systems," in *IEEE Journal of Solid-State Circuits*, vol. 46, no. 6, pp. 1321-1336, June 2011 [[https://sci-hub.se/10.1109/JSSC.2011.2134450](https://sci-hub.se/10.1109/JSSC.2011.2134450)]
>
> S. Ibrahim and B. Razavi, *Low-Power DFE Design* [[https://picture.iczhiku.com/resource/eetop/wykflwIuIQDzYNcB.PDF](https://picture.iczhiku.com/resource/eetop/wykflwIuIQDzYNcB.PDF)]





## PAM4 DFE

![image-20250525202236767](rx/image-20250525202236767.png)

![image-20250525210606180](rx/image-20250525210606180.png)



![image-20250525221556845](rx/image-20250525221556845.png)



![image-20250525221432513](rx/image-20250525221432513.png)

![image-20250525221148218](rx/image-20250525221148218.png)



> K. -C. Chen, W. W. -T. Kuo and A. Emami, "A 60-Gb/s PAM4 Wireline Receiver With 2-Tap Direct Decision Feedback Equalization Employing Track-and-Regenerate Slicers in 28-nm CMOS," in *IEEE Journal of Solid-State Circuits*, vol. 56, no. 3, pp. 750-762, March 2021 [[https://www.mics.caltech.edu/wp-content/uploads/2021/02/JSSC-2020-Xavier-PAM4-Receiver.pdf](https://www.mics.caltech.edu/wp-content/uploads/2021/02/JSSC-2020-Xavier-PAM4-Receiver.pdf)]
>
> Hongtao Zhang, DesignCon 2016. PAM4 Signaling for 56G Serial Link Applications − A Tutorial [[https://www.xilinx.com/publications/events/designcon/2016/slides-pam4signalingfor56gserial-zhang-designcon.pdf](https://www.xilinx.com/publications/events/designcon/2016/slides-pam4signalingfor56gserial-zhang-designcon.pdf)]
