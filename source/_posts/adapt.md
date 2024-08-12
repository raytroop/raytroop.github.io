---
title: Adaptation in Wireline
date: 2024-08-11 11:07:31
tags:
categories:
- analog
mathjax: true
---

## Least-Mean-Square (LMS) 

> minimum mean square error (MMSE) 

This simplified version of LMS algorithm is identical to the *zero-forcing* algorithm which minimizes the ISI at data samples

###  Sign-Sign LMS (SS-LMS)




> T11: Basics of Equalization Techniques: Channels, Equalization, and Circuits, 2022 IEEE International Solid-State Circuits Conference
>
> V. Stojanovic et al., "Autonomous dual-mode (PAM2/4) serial link transceiver with adaptive equalization and data recovery," in IEEE Journal of Solid-State Circuits, vol. 40, no. 4, pp. 1012-1026, April 2005, doi: 10.1109/JSSC.2004.842863.
>
> Jinhyung Lee, Design of High-Speed Receiver for Video Interface with Adaptive Equalization; Phd thesis, August 2019. [thesis link](http://dcollection.snu.ac.kr/common/orgView/000000157003)
>
> Paulo S. R. Diniz, Adaptive Filtering: Algorithms and Practical Implementation, 5th edition
>
> E. -H. Chen et al., "Near-Optimal Equalizer and Timing Adaptation for I/O Links Using a BER-Based Metric," in IEEE Journal of Solid-State Circuits, vol. 43, no. 9, pp. 2144-2156, Sept. 2008



### DFE h0 Estimator

summer output
$$
r_k = a_kh_0+\left(\sum_{n=-\infty,n\neq0}^{+\infty}a_{k-n}h_n-\sum_{n=1}^{\text{ntap}}\hat{a}_{k-n}\hat{h}_n\right)
$$
error slicer analog output
$$
e_k=r_k-\hat{a}_k \hat{h}_0
$$
error slicer digital output
$$
\hat{e}_k=|e_k|
$$
It's NOT possible to implement $e_k$, which need to determine $\hat{a}_k=|r_k|$ in no time. One method to approach this problem is calculate $e_k^{a_k=1}=r_k-\hat{a}_k \hat{h}_0$ and $e_k^{a_k=-1}=r_k+\hat{a}_k \hat{h}_0$, then select the right one based on $\hat{a}_k$

The update  equation based on Sign-Sign-Least Mean square (SS-LMS) and loss function $L(\hat{h}_{\text{0~ntap}})=E(e_k^2)$
$$
\hat{h}_n(k+1) = \hat{h}_n(k)+\mu \cdot |e_k|\cdot \hat{a}_{k-n}
$$
Where $n \in [0,...,\text{ntap}]$. This way, we can obtain $\hat{h}_0$, $\hat{h}_1$, $\hat{h}_2$, ...

> $\hat{h}_0$ is used in AFE adaptation

We may encounter difficulty if the first tap of DFE is unrolled, its $e_k$ is modified as follow
$$
r_k = a_kh_0+\left(\sum_{n=-\infty,n\neq0}^{+\infty}a_{k-n}h_n-\sum_{n=2}^{\text{ntap}}\hat{a}_{k-n}\hat{h}_n\right)
$$
Where there is NO $\hat{h}_1$

To find $\hat{h}_1$, we shall use different pattern for even and odd error slicer




## Maximum Likelihood Sequence Estimation (MLSE)



![image-20240807233152154](adapt/image-20240807233152154.png)



> [IBIS-AMI Modeling and Correlation Methodology for ADC-Based SerDes Beyond 100 Gb/s [https://static1.squarespace.com/static/5fb343ad64be791dab79a44f/t/63d807441bcd266de258b975/1675102025481/SLIDES_Track02_IBIS_AMI_Modeling_and_Correlation_Tyshchenko.pdf](https://static1.squarespace.com/static/5fb343ad64be791dab79a44f/t/63d807441bcd266de258b975/1675102025481/SLIDES_Track02_IBIS_AMI_Modeling_and_Correlation_Tyshchenko.pdf)]
>
> M. Emami Meybodi, H. Gomez, Y. -C. Lu, H. Shakiba and A. Sheikholeslami, "Design and Implementation of an On-Demand Maximum-Likelihood Sequence Estimation (MLSE)," in IEEE Open Journal of Circuits and Systems, vol. 3, pp. 97-108, 2022, doi: 10.1109/OJCAS.2022.3173686.
>
> Zaman, Arshad Kamruz (2019). A Maximum Likelihood Sequence Equalizing Architecture Using Viterbi Algorithm for ADC-Based Serial Link. Undergraduate Research Scholars Program. Available electronically from [[https://hdl.handle.net/1969.1/166485](https://hdl.handle.net/1969.1/166485)]



There are several variants of MLSD (Maximum Likelihood Sequence Detection), including:

- Viterbi Algorithm
- Decision Feedback Sequence Estimation (DFSE)
- Soft-Output MLSD




> [Evolution Of Equalization Techniques In High-Speed SerDes For Extended Reaches. [https://semiengineering.com/evolution-of-equalization-techniques-in-high-speed-serdes-for-extended-reaches/](https://semiengineering.com/evolution-of-equalization-techniques-in-high-speed-serdes-for-extended-reaches/)]





## Mueller-Muller A

| pattern | main cursor               |
| ------- | ------------------------- |
| 0**1**1 | $s_{011}=-h_1+h_0+h_{-1}$ |
| 1**1**0 | $s_{110}=h_1+h_0-h_{-1}$  |
| 1**0**0 | $s_{100}=h_1-h_0-h_{-1}$  |
| 0**0**1 | $s_{001}=-h_1-h_0+h_{-1}$ |

During adapting,  we make

- 0**1**1 & 1**1**0 are approaching to each other
- 1**0**0 & 0**0**1 are approaching to each other

Then, $h_{-1}$ and $h_1$ are same, which is desired



## Mueller-Muller B

MMPD infers the channel response from baud-rate samples of the received data, the adaptation aligns the sampling clock such that pre-cursor is equal to the post-cursor in the *pulse response*

![image-20240807230029591](adapt/image-20240807230029591.png)



> Faisal A. Musa. "HIGH-SPEED BAUD-RATE CLOCK RECOVERY" [[https://www.eecg.utoronto.ca/~tcc/thesis-musa-final.pdf](https://www.eecg.utoronto.ca/~tcc/thesis-musa-final.pdf)]
>
> Faisal A. Musa."CLOCK RECOVERY IN HIGH-SPEED MULTILEVEL SERIAL LINKS" [[https://www.eecg.utoronto.ca/~tcc/faisal_iscas03.pdf](https://www.eecg.utoronto.ca/~tcc/faisal_iscas03.pdf)]
>
> Eduardo Fuentetaja. "Analysis of the M&M Clock Recovery Algorithm" [[https://edfuentetaja.github.io/sdr/m_m_analysis/](https://edfuentetaja.github.io/sdr/m_m_analysis/)]
>
> Liu T, Li T, Lv F, Liang B, Zheng X, Wang H, Wu M, Lu D, Zhao F. Analysis and Modeling of Mueller–Muller Clock and Data Recovery Circuits. *Electronics*. 2021; 10(16):1888.
>
> Youzhi Gu . Analysis of Mueller-Muller Clock and Data Recovery Circuits with a Linearized Model
>
> Baud-Rate CDRs [[https://ocw.snu.ac.kr/sites/default/files/NOTE/Lec%206%20-%20Clock%20and%20Data%20Recovery.pdf](https://ocw.snu.ac.kr/sites/default/files/NOTE/Lec%206%20-%20Clock%20and%20Data%20Recovery.pdf)]
>
> F. Spagna *et al*., "A 78mW 11.8Gb/s serial link transceiver with adaptive RX equalization and baud-rate CDR in 32nm CMOS," *2010 IEEE International Solid-State Circuits Conference - (ISSCC)*, San Francisco, CA, USA, 2010, pp. 366-367, doi: 10.1109/ISSCC.2010.5433823.

![image-20240810095006113](adapt/image-20240810095006113.png)

![image-20240808001201612](adapt/image-20240808001201612.png)


![image-20240808001256515](adapt/image-20240808001256515.png)


![image-20240808001449664](adapt/image-20240808001449664.png)

![image-20240808001501485](adapt/image-20240808001501485.png)



## Sign-Sign Mueller-Muller CDR

![image-20240807232814202](adapt/image-20240807232814202.png)





## reference

Stojanovic, Vladimir & Ho, A. & Garlepp, B. & Chen, Fred & Wei, J. & Alon, Elad & Werner, C. & Zerbe, J. & Horowitz, M.A.. (2004). Adaptive equalization and data recovery in a dual-mode (PAM2/4) serial link transceiver. IEEE Symposium on VLSI Circuits, Digest of Technical Papers. 348 - 351. 10.1109/VLSIC.2004.1346611. 

A. A. Bazargani, H. Shakiba and D. A. Johns, "MMSE Equalizer Design Optimization for Wireline SerDes Applications," in *IEEE Transactions on Circuits and Systems I: Regular Papers*, doi: 10.1109/TCSI.2023.3328807.