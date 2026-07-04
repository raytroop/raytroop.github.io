---
title: Loop and Partial Inductance
date: 2025-01-24 14:27:50
tags:
categories:
- sipi
mathjax: true
---



## Basis of Inductance

> Eric Bogatin. What Really Is Inductance? [[https://speedingedge.com/wp-content/uploads/BTS006_What_Is_Inductance-2.pdf](https://speedingedge.com/wp-content/uploads/BTS006_What_Is_Inductance-2.pdf)]

![image-20260124152308248](inductance/image-20260124152308248.png)

![image-20260124210314577](inductance/image-20260124210314577.png)

### Self-Inductance & Mutual Inductance

![image-20260124200404275](inductance/image-20260124200404275.png)

![image-20260124210821758](inductance/image-20260124210821758.png)$$\begin{align}
N_a &= L_a I_a + \color{red}M_{ab}I_b \\
N_b &= L_b I_b + \color{red}M_{ab}I_a
\end{align}$$



### Induced voltage

![image-20260124210346852](inductance/image-20260124210346852.png)

![image-20260125120847806](inductance/image-20260125120847806.png)

![image-20260125120937298](inductance/image-20260125120937298.png)

### Partial Inductance

![image-20260125183617687](inductance/image-20260125183617687.png)

![image-20260125183709820](inductance/image-20260125183709820.png)

### Loop Self & Mutual Inductance

![image-20260125195819018](inductance/image-20260125195819018.png)

![image-20260125202151186](inductance/image-20260125202151186.png)

###  Loop Mutual Inductance

![image-20260125211932743](inductance/image-20260125211932743.png)

### Equivalent Inductance of Multiple Inductors

![image-20260125212328197](inductance/image-20260125212328197.png)
$$
L_\text{series} = L_1 + L_{12} + L_2 +L_{12} = L_1 + L_2 + 2L_{12}
$$

$$
L_\text{parallel} = (L_1 + L_{12})\parallel (L_2 + L_{12}) = \frac{L_1L_2 +L_{12}(L_1+L_2)+L_{12}^2}{L_1+L_2+2L_{12}}
$$

### internal self-inductance 

![image-20260226234546294](inductance/image-20260226234546294.png)

|self-inductance|magnetic-field line  |
|--|--|
| internal self-inductance | inside the conductor |
| external self-inductance | outside the conductor |

![image-20260226235112730](inductance/image-20260226235112730.png)

![image-20260226235308288](inductance/image-20260226235308288.png)

---

![image-20260226233648052](inductance/image-20260226233648052.png)

| Frequency      | self-inductance                         |
| -------------- | --------------------------------------- |
| low frequency  | $L_\text{internal} + L_\text{external}$ |
| high frequency | $L_\text{external}$                     |



---

***cross-sectional area***

![image-20260227002304758](inductance/image-20260227002304758.png)

>  at low frequency



## Partial Inductance

**Loop Inductance** is the sum of **partial self-inductance** and **partial-mutual inductance**

![image-20250708230643776](inductance/image-20250708230643776.png)

### Magnetic Vector Potential (磁矢势)

> Youjin Deng. 5-3 静磁场的基本规律 [[http://staff.ustc.edu.cn/~yjdeng/EM2022/pdf/5-2(2022).pdf](http://staff.ustc.edu.cn/~yjdeng/EM2022/pdf/5-2(2022).pdf)]

磁场不能用标量势描述

![image-20250709195107708](inductance/image-20250709195107708.png)

![image-20250709195217587](inductance/image-20250709195217587.png)

> ![image-20250709200229266](inductance/image-20250709200229266.png)
>

---



![image-20250708231822291](inductance/image-20250708231822291.png)



### self partial inductance

![image-20250708233924675](inductance/image-20250708233924675.png)

### mutual partial inductance

![image-20250708234512418](inductance/image-20250708234512418.png)



### Ex. two-wire

![image-20250709001127400](inductance/image-20250709001127400.png)





---

> [[https://www.oldfriend.url.tw/Q3D/ansys_ch_Partial_Loop_Inductance.html](https://www.oldfriend.url.tw/Q3D/ansys_ch_Partial_Loop_Inductance.html)]

![image-20250602120913866](inductance/image-20250602120913866-1751987296814-45.png)

![img](inductance/30_Par03-1752499681539-2.jpg)



---

> Chapter 4.5. High Frequency Passive Devices [[https://www.cambridge.org/il/files/7713/6698/2369/HFIC_chapter_4_passives.pdf](https://www.cambridge.org/il/files/7713/6698/2369/HFIC_chapter_4_passives.pdf)]

![image-20260418113018549](inductance/image-20260418113018549.png)



## On-Chip Spiral Inductors

> Designer's Tips on RFIC Inductors [[https://www.rfinsights.com/concepts/tips-on-rfic-inductors/](https://www.rfinsights.com/concepts/tips-on-rfic-inductors/)]

---

![image-20260511215641943](inductance/image-20260511215641943.png)



### substrate-induced eddy-current loss

![image-20260604235223756](inductance/image-20260604235223756.png)

![image-20260604235818118](inductance/image-20260604235818118.png)



### 8-Shaped Inductor

> J. H. Mikkelsen, O. K. Jensen and T. Larsen, "Crosstalk coupling effects of CMOS co-planar spiral inductors," Proceedings of the IEEE 2004 Custom Integrated Circuits Conference [[https://sci-hub.jp/10.1109/CICC.2004.1358825](https://sci-hub.jp/10.1109/CICC.2004.1358825)]

![image-20260512011753324](inductance/image-20260512011753324.png)

![image-20260512012935994](inductance/image-20260512012935994.png)

![image-20260512013045872](inductance/image-20260512013045872.png)



---

> P. Guan et al., "8-Shaped Inductors: An Essential Addition to RFIC Designers' Toolbox," in IEEE Open Journal of the Solid-State Circuits Society, vol. 4, pp. 131-146, 2024 [[pdf](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=10668829)]

- **Field picture** 
- **Partial-inductance picture** 



![image-20260512013458630](inductance/image-20260512013458630.png)

![image-20260512013323760](inductance/image-20260512013323760.png)

![image-20260512013638832](inductance/image-20260512013638832.png)

---

![image-20260512013712902](inductance/image-20260512013712902.png)

![image-20260512013837084](inductance/image-20260512013837084.png)

![image-20260512013924643](inductance/image-20260512013924643.png)



## Transformer

| Quantity             | Symbol        | Meaning                                                      | Formula                                        |
| -------------------- | ------------- | ------------------------------------------------------------ | ---------------------------------------------- |
| Magnetic flux        | $\Phi$        | Magnetic field $\mathbf{B}$ passing through area $\mathbf{S}$ | $\Phi = \int_S \mathbf{B}\cdot d\mathbf{S}$    |
| Flux linkage         | $\lambda$     | Flux linked with coil **turns** $N$                          | $\lambda = N\Phi$                              |
| Induced EMF          | $\mathcal{E}$ | Voltage generated by changing flux linkage                   | $\mathcal{E} = -\mathrm{d}\lambda/\mathrm{d}t$ |
| Self-inductance      | $L$           | Flux linkage caused by own current                           | $L = \lambda/i$                                |
| Mutual inductance    | $M$           | Flux linkage caused by another coil's current                | $M = \lambda_{21}/i_1$                         |
| Coupling coefficient | $k$           | Magnetic coupling strength between inductors                 | $k = M/\sqrt{L_1L_2}$                          |



### ideal transformer

![image-20260704081621683](inductance/image-20260704081621683.png)

For an ideal **N:1** transformer,
$$
\boxed{V_1 = N V_2} \qquad \boxed{I_1 = -\frac{I_2}{N}}
$$
The **minus sign comes from power conservation**
$$
V_1 I_1 + V_2 I_2 = 0
$$
so
$$
N V_2 I_1 + V_2 I_2 = 0
$$
therefore
$$
I_1 = -\frac{I_2}{N}
$$

---



So Fig. 2.3 has exactly the same two-port equations as the original coupled inductors



### Electromotive Force (EMF) $\mathcal{E}$

***back emf***

![inductor_terminal_voltage_back_emf_schematic](inductance/inductor_terminal_voltage_back_emf_schematic.png)

### mutual inductance

$$
M_{12}=M_{21}=M \qquad \frac{N_1\Phi_{12}}{i_2}=\frac{N_2\Phi_{21}}{i_1}
=
M
$$

Important: this **does not mean**
$$
\Phi_{12} = \Phi_{21}
$$




### $k$ vs. $M$

**Coupling coefficient $k$** is based on **flux linkage ratios**, not directly magnetic flux ratios

![image-20260606085423509](inductance/image-20260606085423509.png)

![image-20260606085444200](inductance/image-20260606085444200.png)

![image-20260606085839666](inductance/image-20260606085839666.png)



---

---

任何封闭电路中感应电动势大小，等于穿过这一电路磁通量的变化率。
$$
\epsilon = -\frac{\mathrm{d}\Phi_B}{\mathrm{d}t}
$$
其中 $\epsilon$是电动势，单位为伏特

$\Phi_B$是通过电路的磁通量，单位为韦伯

电动势的方向（公式中的负号）由楞次定律决定

> **楞次定律**: 由于磁通量的改变而产生的感应电流，其方向为抗拒磁通量改变的方向。

> 在回路中产生感应电动势的原因是由于通过回路平面的磁通量的**变化**，而不是磁通量本身，即使通过回路的磁通量很大，但只要它不随时间变化，回路中依然不会产生感应电动势。

---

***自感电动势***

当电流$I$随时间变化时，在线圈中产生的自感电动势为
$$
\epsilon = -L\frac{\mathrm{d}I}{\mathrm{d}t}
$$


![image-20240713131201618](inductance/image-20240713131201618.png)

![image-20251022234419312](inductance/image-20251022234419312.png)

![image-20240713145005306](inductance/image-20240713145005306.png)

![image-20240713145212327](inductance/image-20240713145212327.png)





---

![image-20240713140911612](inductance/image-20240713140911612.png)

***magnetic flux***

![image-20240713135148710](inductance/image-20240713135148710.png)

***magnetic linkage***

![image-20240713135236291](inductance/image-20240713135236291.png)

> **同名端**：当两个*电流*分别从两个线圈的对应端子流入 ，其所 产生的磁场相互加强时，则这两个对应端子称为同名端。

![image-20240713142238398](inductance/image-20240713142238398.png)

![image-20240713142249362](inductance/image-20240713142249362.png)

![image-20240713142506673](inductance/image-20240713142506673.png)

---

> Integrated Transformer Models [[https://www.rfinsights.com/concepts/rfic-transformer-model/](https://www.rfinsights.com/concepts/rfic-transformer-model/)]

![image-20260619192653284](inductance/image-20260619192653284.png)



## reference

Bogatin, E. (2018). *Signal and power integrity, simplified*. Prentice Hall. [[pdf](https://www.oldfriend.url.tw/article/SI_PI_book/Signal%20and%20Power%20Integrity%20-%20Simplified_2nd_Eric%20Bogatin_Prentice%20Hall%20PTR_2010.pdf)]

Paul, Clayton R. *Inductance: Loop and Partial*. Hoboken, N.J. : [Piscataway, N.J.]: Wiley ; IEEE, 2010. [[pdf](https://picture.iczhiku.com/resource/eetop/sHkGlwJeEepldVnx.pdf)]

Spartaco Caniggia. Signal Integrity and Radiated Emission of High‐Speed Digital Systems. Wiley 2008

Luong, H. C., & Yin, J. (2016). *Transformer-based design techniques for oscillators and frequency dividers*. Springer International Publishing

---

ISSCC2002. Special Topic Evening Discussion Sessions SE1: Inductance: Implications and Solutions for High-Speed Digital Circuits
[[vSE1_Blaauw](https://engineering.purdue.edu/oxidemems/conferences/isscc2002/DATA/vSE1_Blaauw.pdf)], [[vSE1_Gauthier](https://engineering.purdue.edu/oxidemems/conferences/isscc2002/DATA/vSE1_Gauthier.pdf)], [[vSE1_Morton](https://engineering.purdue.edu/oxidemems/conferences/isscc2002/DATA/vSE1_Morton.pdf), [[vSE1_Restle](https://engineering.purdue.edu/oxidemems/conferences/isscc2002/DATA/vSE1_Restle/01.html)]]

Y. Massoud and Y. Ismail, "Gasping the impact of on-chip inductance," in IEEE Circuits and Devices Magazine, vol. 17, no. 4, pp. 14-21, July 2001 [[https://sci-hub.se/10.1109/101.950046](https://sci-hub.se/10.1109/101.950046)]

Clayton R. Paul, Partial Inductance [[https://ewh.ieee.org/soc/emcs/acstrial/newsletters/summer10/PP_PartialInductance.pdf](https://ewh.ieee.org/soc/emcs/acstrial/newsletters/summer10/PP_PartialInductance.pdf)]

Cheung-Wei Lam. Common Misconceptions about Inductance & Current Return Path [[https://ewh.ieee.org/r6/scv/emc/archive/022010Lam.pdf](https://ewh.ieee.org/r6/scv/emc/archive/022010Lam.pdf)]

Randy Wolff. Signal Loop Inductance in [Pin] and [Package Model] [[https://ibis.org/summits/feb10/wolff.pdf](https://ibis.org/summits/feb10/wolff.pdf)]

ANSYS Q3D Getting Started LE05. Module 5: Q3D Inductance Matrix Reduction [[https://innovationspace.ansys.com/courses/wp-content/uploads/sites/5/2021/07/Q3D_GS_2020R1_EN_LE05_Ind_Matrix.pdf](https://innovationspace.ansys.com/courses/wp-content/uploads/sites/5/2021/07/Q3D_GS_2020R1_EN_LE05_Ind_Matrix.pdf)]

