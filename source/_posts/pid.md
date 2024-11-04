---
title: PID Control
date: 2024-10-07 14:10:40
tags:
categories:
- dsp
mathjax: true
---


- proportional term (P) depends on the present error
- integral term (I) depends on past errors
- derivative term (D) depends on anticipated future errors 

> **PID** controller makes use of linear extrapolation of the measured output
>
> **PI** controller does not make use of any prediction of the future state of the system
>
> The prediction by linear extrapolation (D) can generate large undesired control signals because measurement noise is amplified, that's why **D** is not used widely
>
---


## reference

Gene F. Franklin, J. David Powell, and Abbas Emami-Naeini. 2018. Feedback Control of Dynamic Systems (8th Edition). Pearson.

Åström, K.J. & Murray, Richard. (2021). Feedback Systems: An Introduction for Scientists and Engineers Second Edition [[https://www.cds.caltech.edu/~murray/books/AM08/pdf/fbs-public_24Jul2020.pdf](https://www.cds.caltech.edu/~murray/books/AM08/pdf/fbs-public_24Jul2020.pdf)]

Yan Lu, ISSCC2021 T10: Fundamentals of Fully Integrated Voltage Regulators [[https://www.nishanchettri.com/isscc-slides/2021%20ISSCC/TUTORIALS/ISSCC2021-T10.pdf](https://www.nishanchettri.com/isscc-slides/2021%20ISSCC/TUTORIALS/ISSCC2021-T10.pdf)]
