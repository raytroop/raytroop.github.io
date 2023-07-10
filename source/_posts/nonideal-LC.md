---
title: Non ideal capacitor and inductor
date: 2023-12-24 16:35:23
tags:
categories:
- analog
mathjax: true
---

## Conversion Relationships

### Capacitor

![image-20231224163730529](nonideal-LC/image-20231224163730529.png)

---

![image-20240119000951498](nonideal-LC/image-20240119000951498.png)

![image-20240119001025892](nonideal-LC/image-20240119001025892.png)

![image-20240119001309410](nonideal-LC/image-20240119001309410.png)



### Inductor

![image-20231224163740411](nonideal-LC/image-20231224163740411.png)

### Derivation

![image-20231224163905233](nonideal-LC/image-20231224163905233.png)

![image-20231224163916109](nonideal-LC/image-20231224163916109.png)

---

![image-20231224212914366](nonideal-LC/image-20231224212914366.png)

![image-20231224212625409](nonideal-LC/image-20231224212625409.png)

![image-20231224212541383](nonideal-LC/image-20231224212541383.png)

$V_o = V_i |A|e^{j\theta}$, and $A_r = |A|\cos\theta$, $A_i = |A|\sin\theta$

Then $I_i = (V_i - V_o)sC_f= V_i(1-|A|e^{j\theta})sC_f$, impedance is shown as below

$$\begin{align}
Z &= \frac{V_i}{I_i} \\
&= \frac{1}{(1-|A|e^{j\theta})j\omega C_f} \\
&= -\frac{j}{\omega C_f\frac{1+|A|^2-2|A|\cos\theta}{1-|A|\cos\theta}} + \frac{|A|\sin\theta}{\omega C_f (1+|A|^2-2|A|\cos\theta)} \\
\end{align}$$

$C_\text{eq}$ and $R_\text{eq}$ are obtained
$$\begin{align}
C_\text{eq} &= \frac{1+|A|^2-2A_r}{1-A_r}\cdot C_f \\
R_\text{eq} &= \frac{A_i}{1+|A|^2-2A_r}\cdot \frac{1}{\omega C_f}
\end{align}$$



## series or parallel representation







## reference

Tank Circuits/Impedances [[https://stanford.edu/class/ee133/handouts/lecturenotes/lecture5_tank.pdf](https://stanford.edu/class/ee133/handouts/lecturenotes/lecture5_tank.pdf)]

Resonant Circuits  [[https://web.ece.ucsb.edu/~long/ece145b/Resonators.pdf](https://web.ece.ucsb.edu/~long/ece145b/Resonators.pdf)]

Series & Parallel Impedance Parameters and Equivalent Circuits [[https://assets.testequity.com/te1/Documents/pdf/series-parallel-impedance-parameters-an.pdf](https://assets.testequity.com/te1/Documents/pdf/series-parallel-impedance-parameters-an.pdf)]

ES Lecture 35: Non ideal capacitor, Capacitor Q and series RC to parallel RC conversion [[https://youtu.be/CJ_2U5pEB4o?si=4j4CWsLSapeu-hBo](https://youtu.be/CJ_2U5pEB4o?si=4j4CWsLSapeu-hBo)]

