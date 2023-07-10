---
title: Metastability and Synchronizer 
date: 2023-08-10 20:57:37
tags:
categories:
- digital
mathjax: true
---

## Sequentail logic deal

We guarantee setup & hold time / minimum clock width, FF guarantees propagation delay (clock -> q delay)

We can not keep our part of the deal because asynchronous signal may change in the setup/hold window

FF enters a metastable state, as a result it does not guarantee propagation delay


## What is a metastable flip flop?


> Non-Regenerative flipflop: **NOT** suitable for synchronization

> Regenerative flipflop: Feedback loop must be isolated



## Probability of entering a metastable state


## Metastability resolution time constant ($\tau$) of flip-flops

$$
T_W = T_0 \cdot e^{-t_r/\tau}
$$

- $T_W$: metastability window width for a given $t_r$ ($|T_{clk}-T_d| - T_{meta}$)
where $T_{meta}$ is the data failing point ($t_r=\infty$)

- $T_0$: metastability window width at zero resolution time

- $t_r$: resolution time (clock to output delay)

- $\tau$: resolution time constant





## Recovering from a metastable state


### in a latch


### in a flipflop


## Probability of failure


## Techniques to improve MTBF


## Data Flip-Flops Vs. Synchronizer Flip-Flops

![image-20230704230313635](synchronizer-metastability/image-20230704230313635.png)









## reference

Chen, Doris T., Deshanand P. Singh, Jeffrey Chromczak, David M. Lewis, Ryan Fung, David Neto and Vaughn Betz. “A comprehensive approach to modeling, characterizing and optimizing for metastability in FPGAs.” Symposium on Field Programmable Gate Arrays (2010).

Jerome Cox. Synchronizers And Data Flip-Flops are Different [[https://ee.usc.edu/async2015/web/wp-content/uploads/2015/03/S1_P4_ASYNC2015IndustrialPaperDFF.pdf](https://ee.usc.edu/async2015/web/wp-content/uploads/2015/03/S1_P4_ASYNC2015IndustrialPaperDFF.pdf)]

J. U. Horstmann, H. W. Eichel and R. L. Coates, "Metastability behavior of CMOS ASIC flip-flops in theory and test," in IEEE Journal of Solid-State Circuits, vol. 24, no. 1, pp. 146-157, Feb. 1989, doi: 10.1109/4.16314.

Steve Golson. Synchronization and Metastability [[https://trilobyte.com/pdf/golson_snug14.pdf](https://trilobyte.com/pdf/golson_snug14.pdf)]

J. Reiher, M. R. Greenstreet and I. W. Jones, "Explaining Metastability in Real Synchronizers," 2018 24th IEEE International Symposium on Asynchronous Circuits and Systems (ASYNC), Vienna, Austria, 2018, pp. 59-67, doi: 10.1109/ASYNC.2018.00024.

A. Cantoni, J. Walker and T. -D. Tomlin, "Characterization of a Flip-Flop Metastability Measurement Method," in IEEE Transactions on Circuits and Systems I: Regular Papers, vol. 54, no. 5, pp. 1032-1040, May 2007, doi: 10.1109/TCSI.2007.895514.

S. Yang, I. W. Jones and M. R. Greenstreet, "Synchronizer Performance in Deep Sub-Micron Technology," 2011 17th IEEE International Symposium on Asynchronous Circuits and Systems, Ithaca, NY, USA, 2011, pp. 33-42, doi: 10.1109/ASYNC.2011.19.

Max Maxfield. Meandering Musings on Metastability [[https://www.eejournal.com/article/meandering-musings-on-metastability/](https://www.eejournal.com/article/meandering-musings-on-metastability/)]

R. Ginosar, "Metastability and Synchronizers: A Tutorial," in IEEE Design & Test of Computers, vol. 28, no. 5, pp. 23-35, Sept.-Oct. 2011, doi: 10.1109/MDT.2011.113. [[https://webee.technion.ac.il/~ran/papers/Metastability-and-Synchronizers.IEEEDToct2011.pdf](https://webee.technion.ac.il/~ran/papers/Metastability-and-Synchronizers.IEEEDToct2011.pdf)]
