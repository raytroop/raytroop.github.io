---
title: DAC-based FFE in PAM4 Transmitter
date: 2022-07-20 22:51:22
tags:
- pam4
- tx
- fir
- dac
categories:
- analog
mathjax: true
---

![image-20220721220225623](tx-pam4-fir-dac/image-20220721220225623.png)

One classic TX implementation contain:

- a DAC: **56GS/s** **8b** 
- a DSP: **8-tap FIR**

> C. Menolfi et al., "A 112Gb/S 2.6pJ/b 8-Tap FFE PAM-4 SST TX in 14nm CMOS," 2018 IEEE International Solid - State Circuits Conference - (ISSCC), 2018, pp. 104-106, doi: 10.1109/ISSCC.2018.8310205.

![image-20220721234522043](tx-pam4-fir-dac/image-20220721234522043.png)



## $\pi$-coil

![image-20220720232837839](tx-pam4-fir-dac/image-20220720232837839.png)

> J. Kim et al., "A 112Gb/s PAM-4 transmitter with 3-Tap FFE in 10nm CMOS," 2018 IEEE International Solid - State Circuits Conference - (ISSCC), 2018, pp. 102-104, doi: 10.1109/ISSCC.2018.8310204.

## reference

C. Menolfi et al., "A 112Gb/S 2.6pJ/b 8-Tap FFE PAM-4 SST TX in 14nm CMOS," 2018 IEEE International Solid - State Circuits Conference - (ISSCC), 2018, pp. 104-106, doi: 10.1109/ISSCC.2018.8310205.

E. Chong et al., "A 112Gb/s PAM-4, 168Gb/s PAM-8 7bit DAC-Based Transmitter in 7nm FinFET," ESSCIRC 2021 - IEEE 47th European Solid State Circuits Conference (ESSCIRC), 2021, pp. 523-526, doi: 10.1109/ESSCIRC53450.2021.9567801.

B. Razavi, "Design Techniques for High-Speed Wireline Transmitters," in IEEE Open Journal of the Solid-State Circuits Society, vol. 1, pp. 53-66, 2021, doi: 10.1109/OJSSCS.2021.3112398.

Wang, Z., Choi, M., Lee, K., Park, K., Liu, Z., Biswas, A., Han, J., Du, S., & Alon, E. (2022). An Output Bandwidth Optimized 200-Gb/s PAM-4 100-Gb/s NRZ Transmitter With 5-Tap FFE in 28-nm CMOS. IEEE Journal of Solid-State Circuits, 57(1), 21-31. https://doi.org/10.1109/JSSC.2021.3109562

J. Kim et al., "A 112Gb/s PAM-4 transmitter with 3-Tap FFE in 10nm CMOS," 2018 IEEE International Solid - State Circuits Conference - (ISSCC), 2018, pp. 102-104, doi: 10.1109/ISSCC.2018.8310204.

