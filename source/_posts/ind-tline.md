---
title: Inductance & Transmission Line
date: 2025-01-24 14:27:50
tags:
categories:
- sipi
mathjax: true
---



## Basis of Inductance

> Eric Bogatin. What Really Is Inductance? [[https://speedingedge.com/wp-content/uploads/BTS006_What_Is_Inductance-2.pdf](https://speedingedge.com/wp-content/uploads/BTS006_What_Is_Inductance-2.pdf)]

![image-20260124152308248](ind-tline/image-20260124152308248.png)

![image-20260124210314577](ind-tline/image-20260124210314577.png)

### Self-Inductance & Mutual Inductance

![image-20260124200404275](ind-tline/image-20260124200404275.png)

![image-20260124210821758](ind-tline/image-20260124210821758.png)$$\begin{align}
N_a &= L_a I_a + \color{red}M_{ab}I_b \\
N_b &= L_b I_b + \color{red}M_{ab}I_a
\end{align}$$



### Induced voltage

![image-20260124210346852](ind-tline/image-20260124210346852.png)

![image-20260125120847806](ind-tline/image-20260125120847806.png)

![image-20260125120937298](ind-tline/image-20260125120937298.png)

### Partial Inductance

![image-20260125183617687](ind-tline/image-20260125183617687.png)

![image-20260125183709820](ind-tline/image-20260125183709820.png)

### Loop Self & Mutual Inductance

![image-20260125195819018](ind-tline/image-20260125195819018.png)

![image-20260125202151186](ind-tline/image-20260125202151186.png)

###  Loop Mutual Inductance

![image-20260125211932743](ind-tline/image-20260125211932743.png)

### Equivalent Inductance of Multiple Inductors

![image-20260125212328197](ind-tline/image-20260125212328197.png)
$$
L_\text{series} = L_1 + L_{12} + L_2 +L_{12} = L_1 + L_2 + 2L_{12}
$$

$$
L_\text{parallel} = (L_1 + L_{12})\parallel (L_2 + L_{12}) = \frac{L_1L_2 +L_{12}(L_1+L_2)+L_{12}^2}{L_1+L_2+2L_{12}}
$$







## Partial Inductance

**Loop Inductance** is the sum of **partial self-inductance** and **partial-mutual inductance**

![image-20250708230643776](ind-tline/image-20250708230643776.png)

### Magnetic Vector Potential (磁矢势)

> Youjin Deng. 5-3 静磁场的基本规律 [[http://staff.ustc.edu.cn/~yjdeng/EM2022/pdf/5-2(2022).pdf](http://staff.ustc.edu.cn/~yjdeng/EM2022/pdf/5-2(2022).pdf)]

磁场不能用标量势描述

![image-20250709195107708](ind-tline/image-20250709195107708.png)

![image-20250709195217587](ind-tline/image-20250709195217587.png)

> ![image-20250709200229266](ind-tline/image-20250709200229266.png)
>

---



![image-20250708231822291](ind-tline/image-20250708231822291.png)



### self partial inductance

![image-20250708233924675](ind-tline/image-20250708233924675.png)

### mutual partial inductance

![image-20250708234512418](ind-tline/image-20250708234512418.png)



### Ex. two-wire

![image-20250709001127400](ind-tline/image-20250709001127400.png)





---

![image-20250602120913866](ind-tline/image-20250602120913866-1751987296814-45.png)

![img](ind-tline/30_Par03-1752499681539-2.jpg)

> [[https://www.oldfriend.url.tw/Q3D/ansys_ch_Partial_Loop_Inductance.html](https://www.oldfriend.url.tw/Q3D/ansys_ch_Partial_Loop_Inductance.html)]



##   Current Return Path

![image-20250705171613361](ind-tline/image-20250705171613361-1751987296815-47.png)

Current return paths are frequency dependent $Z = R +j\omega L$

- Low frequency
  - $R$ dominates - current use as many returns as possible to have parallel resistances
- High frequency
  - $j\omega L$​ dominates - current use the *closest possible return path* to form *the smallest possible loop inductance*
- Very high frequency
  - The current would be confined to the *nearest* possible return only at ultra-high frequencies (skin effect)
  

![image-20250705170949035](ind-tline/image-20250705170949035-1751987296815-48.png)

---

**skin effect** & **Dielectric loss**

![image-20250705170028485](ind-tline/image-20250705170028485-1751987296816-49.png)

---

***EMX simulation***

**setup:**

![image-20250706004037966](ind-tline/image-20250706004037966-1751987296816-50.png)



**frequency sweep:**

![image-20250706010943996](ind-tline/image-20250706010943996-1751987296816-51.png)



> Cadence October 2020, *Analysis of a Figure-Eight Inductor with EMX RAK*
>
> ![image-20250706010216105](ind-tline/image-20250706010216105-1751987296817-52.png)



## RLC network

> [[https://web.stanford.edu/class/archive/ee/ee371/ee371.1066/handouts/markChapt.pdf](https://web.stanford.edu/class/archive/ee/ee371/ee371.1066/handouts/markChapt.pdf)]

![image-20250817105056325](ind-tline/image-20250817105056325.png)

![image-20250817105203031](ind-tline/image-20250817105203031.png)![image-20250817105308602](ind-tline/image-20250817105308602.png)



## Decoupling Capacitor

![image-20250705175343498](ind-tline/image-20250705175343498-1751987296814-46.png)

![image-20260125205518872](ind-tline/image-20260125205518872.png)

![image-20260125205941736](ind-tline/image-20260125205941736.png)

![image-20260125211108504](ind-tline/image-20260125211108504.png)

## Grounding


> Chapter 11 Layout and grounding [[http://ieb-srv1.upc.es/gieb/tecniques/doc/EMC/pdfs/ScienceDirect_articles_27Jul2018_12-16-10.699/Chapter-11---Layout-and-grounding_2007_EMC-for-Product-Designers.pdf](http://ieb-srv1.upc.es/gieb/tecniques/doc/EMC/pdfs/ScienceDirect_articles_27Jul2018_12-16-10.699/Chapter-11---Layout-and-grounding_2007_EMC-for-Product-Designers.pdf)]

*TODO* &#128197;



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

---

Yuriy Shlepnev. How Interconnects Work: Characteristic Impedance and Reflections [[https://www.linkedin.com/pulse/how-interconnects-work-characteristic-impedance-yuriy-shlepnev/](https://www.linkedin.com/pulse/how-interconnects-work-characteristic-impedance-yuriy-shlepnev/)]

—. How Interconnects Work: Bandwidth for Modeling and Measurements [[https://www.linkedin.com/pulse/how-interconnects-work-bandwidth-modeling-yuriy-shlepnev/?trackingId=874kpm3XuNyV9D0eP6IioA%3D%3D](https://www.linkedin.com/pulse/how-interconnects-work-bandwidth-modeling-yuriy-shlepnev/?trackingId=874kpm3XuNyV9D0eP6IioA%3D%3D)]

Eric Bogatin. Pop Quiz: When is an Interconnect Not a Transmission Line?  [[https://www.signalintegrityjournal.com/blogs/4-eric-bogatin-signal-integrity-journal-technical-editor/post/265-pop-quiz-when-is-an-interconnect-not-a-transmission-line](https://www.signalintegrityjournal.com/blogs/4-eric-bogatin-signal-integrity-journal-technical-editor/post/265-pop-quiz-when-is-an-interconnect-not-a-transmission-line)]

TeledyneLeCroy/SignalIntegrity Python tools for signal integrity applications [[SignalIntegrityApp](https://github.com/TeledyneLeCroy/SignalIntegrity)]

A Look at Transmission-Line Losses [[http://blog.teledynelecroy.com/2018/06/a-look-at-transmission-line-losses.html](http://blog.teledynelecroy.com/2018/06/a-look-at-transmission-line-losses.html)]

How Much Transmission-Line Loss is Too Much? [[http://blog.teledynelecroy.com/2018/06/how-much-transmission-line-loss-is-too.html](http://blog.teledynelecroy.com/2018/06/how-much-transmission-line-loss-is-too.html)]

Raymond Y. Chen, Raymond Y. Chen. Fundamentals of S Fundamentals of S-Parameter Parameter Modeling for Power Distribution Modeling for Power Distribution System (PDS) and SSO Analysis System (PDS) and SSO Analysis [[https://ibis.org/summits/jun05/chen.pdf](https://ibis.org/summits/jun05/chen.pdf)]

