---
title: Relative Sensitivity
date: 2023-07-12 01:26:15
tags:
- parasitic
categories:
- analog
mathjax: true
---



Assuming Target  $T$ ( for example, the total resistance) is  function of $x_1,x_2,...,x_N$, then total variation can be expressed as 

$$\begin{align}
dT  &= \sum_{n=1}^N\frac{\partial T}{\partial x_n}dx_n \\
&= \sum_{n=1}^N\frac{\partial T}{\partial x_n}x_n\cdot \frac{dx_n}{x_n}
\end{align}$$

Then, we obtain relative variation
$$\begin{align}
\frac{dT}{T} &= \sum_{n=1}^N\frac{\partial T}{\partial x_n}\frac{x_n}{T}\cdot \frac{dx_n}{x_n}  \\
&= \sum_{n=1}^N S_{x_n}^T \cdot \frac{dx_n}{x_n}
\end{align}$$

&#11088; where $S_{x_n}^T=\frac{\partial T}{\partial x_n}\frac{x_n}{T}$ is **relative sensitivity**

> **relative sensitivity** connect $\frac{dx_n}{x_n}$ with total relative variation $\frac{dT}{T}$



And $dT$ can be expressed as 
$$
dT =\sum_{n=1}^N S_{x_n}^T T\cdot \frac{dx_n}{x_n} = \sum_{n=1}^N x_n'\cdot \frac{dx_n}{x_n}
$$
&#11088; where $x_n'= S_{x_n}^T T$ is the contribution of $x_n$ in $T$

&#11088; For parallel or series resistors, it can prove $\sum_{n=1}^N S_{x_n}^T = 1$ and $ \sum_{n=1}^N x_n'=T$
