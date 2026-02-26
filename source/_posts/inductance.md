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

![image-20250602120913866](inductance/image-20250602120913866-1751987296814-45.png)

![img](inductance/30_Par03-1752499681539-2.jpg)

> [[https://www.oldfriend.url.tw/Q3D/ansys_ch_Partial_Loop_Inductance.html](https://www.oldfriend.url.tw/Q3D/ansys_ch_Partial_Loop_Inductance.html)]





## reference

Bogatin, E. (2018). *Signal and power integrity, simplified*. Prentice Hall. [[pdf](https://www.oldfriend.url.tw/article/SI_PI_book/Signal%20and%20Power%20Integrity%20-%20Simplified_2nd_Eric%20Bogatin_Prentice%20Hall%20PTR_2010.pdf)]

Paul, Clayton R. *Inductance: Loop and Partial*. Hoboken, N.J. : [Piscataway, N.J.]: Wiley ; IEEE, 2010. [[pdf](https://picture.iczhiku.com/resource/eetop/sHkGlwJeEepldVnx.pdf)]

Spartaco Caniggia. Signal Integrity and Radiated Emission of High‐Speed Digital Systems. Wiley 2008

---

ISSCC2002. Special Topic Evening Discussion Sessions SE1: Inductance: Implications and Solutions for High-Speed Digital Circuits
[[vSE1_Blaauw](https://engineering.purdue.edu/oxidemems/conferences/isscc2002/DATA/vSE1_Blaauw.pdf)], [[vSE1_Gauthier](https://engineering.purdue.edu/oxidemems/conferences/isscc2002/DATA/vSE1_Gauthier.pdf)], [[vSE1_Morton](https://engineering.purdue.edu/oxidemems/conferences/isscc2002/DATA/vSE1_Morton.pdf), [[vSE1_Restle](https://engineering.purdue.edu/oxidemems/conferences/isscc2002/DATA/vSE1_Restle/01.html)]]

Y. Massoud and Y. Ismail, "Gasping the impact of on-chip inductance," in IEEE Circuits and Devices Magazine, vol. 17, no. 4, pp. 14-21, July 2001 [[https://sci-hub.se/10.1109/101.950046](https://sci-hub.se/10.1109/101.950046)]

Clayton R. Paul, Partial Inductance [[https://ewh.ieee.org/soc/emcs/acstrial/newsletters/summer10/PP_PartialInductance.pdf](https://ewh.ieee.org/soc/emcs/acstrial/newsletters/summer10/PP_PartialInductance.pdf)]

Cheung-Wei Lam. Common Misconceptions about Inductance & Current Return Path [[https://ewh.ieee.org/r6/scv/emc/archive/022010Lam.pdf](https://ewh.ieee.org/r6/scv/emc/archive/022010Lam.pdf)]

Randy Wolff. Signal Loop Inductance in [Pin] and [Package Model] [[https://ibis.org/summits/feb10/wolff.pdf](https://ibis.org/summits/feb10/wolff.pdf)]

ANSYS Q3D Getting Started LE05. Module 5: Q3D Inductance Matrix Reduction [[https://innovationspace.ansys.com/courses/wp-content/uploads/sites/5/2021/07/Q3D_GS_2020R1_EN_LE05_Ind_Matrix.pdf](https://innovationspace.ansys.com/courses/wp-content/uploads/sites/5/2021/07/Q3D_GS_2020R1_EN_LE05_Ind_Matrix.pdf)]

