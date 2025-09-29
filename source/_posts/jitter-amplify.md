---
title: Jitter Amplification
date: 2022-03-13 23:02:11
tags:
categories:
- noise
mathjax: true
---

![image-20250817101208717](jitter-amplify/image-20250817101208717.png)

---



![image-20250606203026237](jitter-amplify/image-20250606203026237.png)



***discrete time** jitter impulse response* (normalized to the input jitter stimulus similar to the procedure used to represent a conventional system impulse response)

![image-20250606203531304](jitter-amplify/image-20250606203531304.png)

> When impulsive jitter is injected into clock distribution circuits (i.e., a small incremental time delay or advance applied to an **individual** clock edge), it results in jitter in **multiple subsequent** edges in the output clock

![image-20250606215100752](jitter-amplify/image-20250606215100752.png)

![image-20250606215204625](jitter-amplify/image-20250606215204625.png)



## transient noise and rms_jitter function

![image-20220608233610066](jitter-amplify/image-20220608233610066.png)

![image-20220313230930333](jitter-amplify/image-20220313230930333.png)

> `RJ(rms)`: single Edge or Both Edge?
>
> `RJ(seed)`: what is it?



## phase noise method

Directly compare the input phase noise and output phase noise, the input waveform maybe is the PLL output or other clock distribution end point



## Jitter Impulse Response & Jitter Transfer Function

> assuming *linear, time-invariant phase response*
>
> ![image-20250522223530464](jitter-amplify/image-20250522223530464.png)
>
> n =5 buffers, fclk = 10GHz
>
> [[Alphawave’s CTO, Tony Chan Carusone, High Speed Communications Part 8 – On Die CMOS Clock Distribution ](https://youtu.be/nx5CiHcwrF0?si=QhOJmsW5IozRnF4F)]
>
> ![image-20250818230528344](jitter-amplify/image-20250818230528344.png)



Theoretically, the DC gain of JTF of low pass filter shall be ***1***. 
Unfortunately, the gain *less than 1* due to numerical error or nonlinearity

![image-20220313231027512](jitter-amplify/image-20220313231027512.png)



### Example
#### Low Pass Filter

![image-20220322124344158](jitter-amplify/image-20220322124344158.png)

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

![image-20220322124902394](jitter-amplify/image-20220322124902394.png)

![image-20220322124932584](jitter-amplify/image-20220322124932584.png)

> discrete time jitter impulse response
> 
> both input and output are discrete time signal, i.e. no sampling in the input, that's why ratio $1/T_s$ is not in the jtf

#### High Pass Filter

![image-20220327010223664](jitter-amplify/image-20220327010223664.png)

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

![image-20220327010421475](jitter-amplify/image-20220327010421475.png)

### inverter chain

![image-20220608232251056](jitter-amplify/image-20220608232251056.png)

![image-20220608232658054](jitter-amplify/image-20220608232658054.png)

![image-20220608232438188](jitter-amplify/image-20220608232438188.png)

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

![image-20220608233303576](jitter-amplify/image-20220608233303576.png)



## Colored Jitter Amplification

> ![image-20250522225506217](jitter-amplify/image-20250522225506217.png)
>
> [[Alphawave’s CTO, Tony Chan Carusone, High Speed Communications Part 8 – On Die CMOS Clock Distribution ](https://youtu.be/nx5CiHcwrF0?si=QhOJmsW5IozRnF4F)]

> ![image-20250522234522208](jitter-amplify/image-20250522234522208.png)
>
> Four major noise sources are included in the modeling: Input noise, DAC quantization noise (DAC QN), DCO random noise (DCO RN), and delay line random noise (DL RN).
>
> H. Kang *et al*., "A 42.7Gb/s Optical Receiver with Digital CDR in 28nm CMOS," *2023 IEEE Radio Frequency Integrated Circuits Symposium (RFIC)*, San Diego, CA, USA, 2023 [[https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=10630516](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=10630516)]



##  Dirac impulse at edge position

![image-20250606205753885](jitter-amplify/image-20250606205753885.png)



## Full-rate JTF

*Singe edge is using*

> *Half-rate*
>
> ![image-20250606220410050](jitter-amplify/image-20250606220410050.png)



![image-20250607113251021](jitter-amplify/image-20250607113251021.png)

```matlab
ji = 10;
jir = readmatrix("~/cargo/jir.csv");
jir = jir / ji;
jir_2e = jir(:, 2);		  % both edge
jir_1e = jir(1:2:end, 2); % single edge

[mag, w] = freqz(jir_2e, 1, [], 1);
plot(w, abs(mag), LineWidth=2);
hold on
[mag, w] = freqz(jir_1e, 1, [], 0.5);
plot(w, abs(mag), LineWidth=2);
grid on;
legend("2Edge", "1Edge")
title("JTF")
```



![image-20250607113553089](jitter-amplify/image-20250607113553089.png)

![image-20250607114048892](jitter-amplify/image-20250607114048892.png)

> fck = 1GHz
>
> Note: Phase Noise dBc is SSB, that's why we add *10log10(2)*



![image-20250607114018289](jitter-amplify/image-20250607114018289.png)



The calculated JTF  from JIR is *too **small*** compared with Pnoise simualtion

> *245.1/272.4 = 89.98%*

---



![image-20250607123008345](jitter-amplify/image-20250607123008345.png)

![image-20250607123126301](jitter-amplify/image-20250607123126301.png)

> *245.1/272.4 = 83.74%*

![image-20250607123235447](jitter-amplify/image-20250607123235447.png)





## Reference

[Sam Palermo, ECEN 720, Lecture 13 - Forwarded Clock Deskew Circuits](https://people.engr.tamu.edu/spalermo/ecen689/lecture13_ee720_fwd_clk_deskew.pdf)

B. Casper and F. O'Mahony, "Clocking Analysis, Implementation and Measurement Techniques for High-Speed Data Links-A Tutorial," in IEEE Transactions on Circuits and Systems I. [[https://people.engr.tamu.edu/spalermo/ecen689/clocking_analysis_hs_links_casper_tcas1_2009.pdf](https://people.engr.tamu.edu/spalermo/ecen689/clocking_analysis_hs_links_casper_tcas1_2009.pdf)]

Rhee, W. (2020). *Phase-locked frequency generation and clocking : architectures and circuits for modern wireless and wireline systems*. The Institution of Engineering and TechnologyMathuranathan Viswanathan, Digital Modulations using Matlab : Build Simulation Models from Scratch

Tony Chan Carusone, University of Toronto, Canada, 2022 CICC Educational Sessions "Architectural Considerations in 100+ Gbps Wireline Transceivers"

X. Mo, J. Wu, N. Wary and T. Chan Carusone, "Design Methodologies for Low-Jitter CMOS Clock Distribution," in IEEE Open Journal of the Solid-State Circuits Society, 2021 [[https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=9559395](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=9559395)]

Y. Zhao and B. Razavi, "Phase Noise Integration Limits for Jitter Calculation," *2022 IEEE International Symposium on Circuits and Systems (ISCAS)*, Austin, TX, USA, 2022 [[https://www.seas.ucla.edu/brweb/papers/Conferences/YZ_ISCAS_22.pdf](https://www.seas.ucla.edu/brweb/papers/Conferences/YZ_ISCAS_22.pdf)]

Thomas Toifl. TWEPP 2012. Low-power High-Speed CMOS I/Os: Design Challenges and Solutions [[https://indico.cern.ch/event/170595/contributions/266344/attachments/212179/297391/twepp_sept2012_final_v2.pdf](https://indico.cern.ch/event/170595/contributions/266344/attachments/212179/297391/twepp_sept2012_final_v2.pdf)]

Ganesh Balamurugan and Naresh Shanbhag, "Modeling and mitigation of jitter in multiGbps source-synchronous I/O links," *Proceedings 21st International Conference on Computer Design*, San Jose, CA, USA, 2003, pp. 254-260, doi: 10.1109/ICCD.2003 [[https://shanbhag.ece.illinois.edu/publications/ganesh-ICCD2203.pdf](https://shanbhag.ece.illinois.edu/publications/ganesh-ICCD2203.pdf)]

Balamurugan, G. & Casper, Bryan & Jaussi, James & Mansuri, Mozhgan & O'Mahony, Frank & Kennedy, Joseph. (2009). Modeling and Analysis of High-Speed I/O Links. Advanced Packaging, IEEE Transactions on. [[https://sci-hub.se/10.1109/TADVP.2008.2011366](https://sci-hub.se/10.1109/TADVP.2008.2011366)]

Jihwan Kim, ISSCC2019 F5: Design Techniques for a 112Gbs PAM-4 Transmitter