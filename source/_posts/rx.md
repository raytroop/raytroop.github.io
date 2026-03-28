---
title: Wireline Receiver
date: 2025-06-07 10:31:43
tags:
categories:
- link
mathjax: true
---



![image-20250703212349339](rx/image-20250703212349339.png)



---

![image-20250726092747147](rx/image-20250726092747147.png)

*VGA/attenuator: ensure a constant swing at the slicer input regardless of the channel variation*

---





## CTLE Linearity

*TODO* &#128197;

![image-20260328182645140](rx/image-20260328182645140.png)



## Front-End Noise

> [https://people.engr.tamu.edu/spalermo/ecen689/lecture6_ee720_rx_circuits.pdf](https://people.engr.tamu.edu/spalermo/ecen689/lecture6_ee720_rx_circuits.pdf)

![image-20250726180326659](rx/image-20250726180326659.png)

> ![image-20250726181859362](rx/image-20250726181859362.png)






## CTLE transfer function

> Circuit Insights @ ISSCC2025: Circuits for Wireline Communications - Kevin Zheng [[https://youtu.be/8NZl81Dj45M&t=1045](https://youtu.be/8NZl81Dj45M&t=1045)]

![image-20260328182328792](rx/image-20260328182328792.png)

![image-20260328182339762](rx/image-20260328182339762.png)



## Decision Feedback Equalizer (DFE)

***speculative DFE*** is also known as ***loop unrolled DFE***, which solve the critical timing on first tap

### DFE architecture

![image-20260328182441169](rx/image-20260328182441169.png)



![image-20250607235201147](rx/image-20250607235201147.png)

Extensive work on DFEs has produced a multitude of architectures, which can be broadly categorized as "**direct**"" or "**unrolled**" (**speculative**) DFEs with "**full-rate**" or "**half-rate**" clocking



![image-20250608000306928](rx/image-20250608000306928.png)

![image-20250608000338808](rx/image-20250608000338808.png)

![image-20250608000357010](rx/image-20250608000357010.png)





> S. Ibrahim and B. Razavi, "Low-Power CMOS Equalizer Design for 20-Gb/s Systems," in *IEEE Journal of Solid-State Circuits*, vol. 46, no. 6, pp. 1321-1336, June 2011 [[https://sci-hub.se/10.1109/JSSC.2011.2134450](https://sci-hub.se/10.1109/JSSC.2011.2134450)]
>
> S. Ibrahim and B. Razavi, *Low-Power DFE Design* [[https://picture.iczhiku.com/resource/eetop/wykflwIuIQDzYNcB.PDF](https://picture.iczhiku.com/resource/eetop/wykflwIuIQDzYNcB.PDF)]


### DFE Error Propagation

> Geoff Zhang. Preliminary Studies on DFE Error Propagation, Precoding, and their Impact on KP4 FEC Performance for PAM4 Signaling Systems [[https://www.ieee802.org/3/ck/public/18_09/zhang_3ck_01a_0918.pdf](https://www.ieee802.org/3/ck/public/18_09/zhang_3ck_01a_0918.pdf)]
>
> Cathy Liu, The Effect of DFE Error Propagation [[https://www.ieee802.org/3/ap/public/nov05/liu_01_1105.pdf](https://www.ieee802.org/3/ap/public/nov05/liu_01_1105.pdf)]
>
> Yuchun Lu, Huawei, Elimination of DFE Error Propagation and Post-FEC Error Floor (Precoding 2.0) [[https://www.ieee802.org/3/ck/public/19_03/lu_3ck_01_0319.pdf](https://www.ieee802.org/3/ck/public/19_03/lu_3ck_01_0319.pdf)]
>
> Z. Wu and J. -R. Guo, "Analysis of UCIe 48/64 GT/s Electrical Links," in *IEEE Open Journal of the Solid-State Circuits Society* [[pdf](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=11150380)]

*TODO* &#128197;

![image-20260328182254717](rx/image-20260328182254717.png)




### PAM4 DFE

![image-20250525202236767](rx/image-20250525202236767.png)

![image-20250525210606180](rx/image-20250525210606180.png)



![image-20250525221556845](rx/image-20250525221556845.png)



![image-20250525221432513](rx/image-20250525221432513.png)

![image-20250525221148218](rx/image-20250525221148218.png)



> K. -C. Chen, W. W. -T. Kuo and A. Emami, "A 60-Gb/s PAM4 Wireline Receiver With 2-Tap Direct Decision Feedback Equalization Employing Track-and-Regenerate Slicers in 28-nm CMOS," in *IEEE Journal of Solid-State Circuits*, vol. 56, no. 3, pp. 750-762, March 2021 [[https://www.mics.caltech.edu/wp-content/uploads/2021/02/JSSC-2020-Xavier-PAM4-Receiver.pdf](https://www.mics.caltech.edu/wp-content/uploads/2021/02/JSSC-2020-Xavier-PAM4-Receiver.pdf)]
>
> Hongtao Zhang, DesignCon 2016. PAM4 Signaling for 56G Serial Link Applications − A Tutorial [[https://www.xilinx.com/publications/events/designcon/2016/slides-pam4signalingfor56gserial-zhang-designcon.pdf](https://www.xilinx.com/publications/events/designcon/2016/slides-pam4signalingfor56gserial-zhang-designcon.pdf)]



## reference

Miguel Gandara, MediaTek. CICC 2025 Circuit Insights: Basics of Wireline Receiver Circuits [[https://youtu.be/X4JTuh2Gdzg](https://youtu.be/X4JTuh2Gdzg)]

Tony Chan Carusone, Alphawave Semi. VLSI2025 SC2: Connectivity Technologies to Accelerate AI

H. Park et al., "7.4 A 112Gb/s DSP-Based PAM-4 Receiver with an LC-Resonator-Based CTLE for >52dB Loss Compensation in 4nm FinFET," 2025 IEEE International Solid-State Circuits Conference (ISSCC), San Francisco, CA, USA, 2025

Noman Hai, Synopsys, Canada CASS Talks 2025 - May 2, 2025: High-speed Wireline Interconnects: Design Challenges and Innovations in 224G SerDes [[https://www.youtube.com/live/wHNOlxHFTzY](https://www.youtube.com/live/wHNOlxHFTzY)]
