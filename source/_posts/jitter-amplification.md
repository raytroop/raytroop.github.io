---
title: jitter amplification
date: 2022-03-13 23:02:11
tags:
categories:
- noise
mathjax: true
---

## transient noise and rms_jitter function

![image-20220608233610066](jitter-amplification/image-20220608233610066.png)

![image-20220313230930333](jitter-amplification/image-20220313230930333.png)

> `RJ(rms)`: single Edge or Both Edge?
>
> `RJ(seed)`: what is it?



## phase noise method

Directly compare the input phase noise and output phase noise, the input waveform maybe is the PLL output or other clock distribution end point



## Jitter Impulse Response(JIR) & Jitter Impulse Response(JIR)

> assuming *linear, time-invariant phase response*

![image-20220313231013645](jitter-amplification/image-20220313231013645.png)

![image-20220313231027512](jitter-amplification/image-20220313231027512.png)

![image-20220313231038542](jitter-amplification/image-20220313231038542.png)

### Example
#### Low Pass Filter

![image-20220322124344158](jitter-amplification/image-20220322124344158.png)

```matlab
N = 32;
x = zeros(N,1);
x(1) = 6;
x(2) = -2;
x(3) = 0.5;
x = x/5;
figure(1)
stem(x)
Y = fft(x, N);
figure(2)
plot(abs(Y(1:N/2)));
```

![image-20220322124902394](jitter-amplification/image-20220322124902394.png)

![image-20220322124932584](jitter-amplification/image-20220322124932584.png)

> discrete time jitter impulse response
> 
> both input and output are discrete time signal, i.e. no sampling in the input, that's why ratio $1/T_s$ is not in the jtf

#### High Pass Filter

![image-20220327010223664](jitter-amplification/image-20220327010223664.png)

```matlab
N = 128;
j_hp = zeros(N, 1);
j_hp(1)= 1;
j_hp(2) = 0.5;
j_hp(3) = -0.3;
j_hp(4) = 0.3;
j_hp(5) = -0.1;
jtf_hp = abs(fft(j_hp));
semilogx(jtf_hp(1:N/2+1));
xlabel('Freq');
ylabel('Jitter Amplification Factor');
grid on;
```

![image-20220327010421475](jitter-amplification/image-20220327010421475.png)

### inverter chain

![image-20220608232251056](jitter-amplification/image-20220608232251056.png)

![image-20220608232658054](jitter-amplification/image-20220608232658054.png)

![image-20220608232438188](jitter-amplification/image-20220608232438188.png)

```matlab
ji = 1e-12; % 1ps
data = importdata('/path/to/jir.csv');
jo = data.data(:, 2);
Ts = 31.25e-12;
Fs = 1/Ts;
jir = jo/ji;
N = 2^(nextpow2(length(jir)-1));
Y = fft(jir, N);
jtf = abs(Y(1:N/2+1));
freqs= Fs/N*(0:N/2);
plot(feqs/1e9, jtf, 'linewidth', 2);
grid on;
xlabel('Freq (GHz)');
ylabel('JTF');
title('JTF of inverter chain');
```

![image-20220608233303576](jitter-amplification/image-20220608233303576.png)

## Reference

[Sam Palermo, ECEN 720, Lecture 13 - Forwarded Clock Deskew Circuits](https://people.engr.tamu.edu/spalermo/ecen689/lecture13_ee720_fwd_clk_deskew.pdf)

B. Casper and F. O'Mahony, "Clocking Analysis, Implementation and Measurement Techniques for High-Speed Data Links-A Tutorial," in IEEE Transactions on Circuits and Systems I. [[https://people.engr.tamu.edu/spalermo/ecen689/clocking_analysis_hs_links_casper_tcas1_2009.pdf](https://people.engr.tamu.edu/spalermo/ecen689/clocking_analysis_hs_links_casper_tcas1_2009.pdf)]

Phase-Locked Frequency Generation and Clocking : Architectures and Circuits for Modern Wireless and Wireline Systems by Woogeun Rhee (2020, Hardcover) 

Mathuranathan Viswanathan, Digital Modulations using Matlab : Build Simulation Models from Scratch

Tony Chan Carusone, University of Toronto, Canada, 2022 CICC Educational Sessions "Architectural Considerations in 100+ Gbps Wireline Transceivers"

X. Mo, J. Wu, N. Wary and T. Chan Carusone, "Design Methodologies for Low-Jitter CMOS Clock Distribution," in IEEE Open Journal of the Solid-State Circuits Society, 2021 [[https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=9559395](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=9559395)]