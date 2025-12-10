---
title: Network Analysis and Scattering parameters
date: 2023-09-29 15:57:01
tags:
categories:
- dsp
mathjax: true
---

![image-20241124184248887](network/image-20241124184248887.png)



---

## Mixed-Mode S-parameter

> 12 May 2021 Introduction to Mixed-Mode S-parameters [[https://blog.teledynelecroy.com/2021/05/introduction-to-mixed-mode-s-parameters.html](https://blog.teledynelecroy.com/2021/05/introduction-to-mixed-mode-s-parameters.html)]

![image-20251025193029645](network/image-20251025193029645.png)

![image-20251025193127266](network/image-20251025193127266.png)

---

> Bert Simonovich. A Guide for Single-Ended to Mixed-Mode S-parameter Conversions [[https://www.signalintegrityjournal.com/articles/1832-a-guide-for-singleended-to-mixedmode-s-parameter-conversions](https://www.signalintegrityjournal.com/articles/1832-a-guide-for-singleended-to-mixedmode-s-parameter-conversions)]

![img](network/720M30Fig1.jpg)

***single-ended S-parameters***

![image-20251025193503968](network/image-20251025193503968.png)

***Mixed-mode S-parameters***

![img](network/fig5.jpg)

![img](network/fig6.jpg)

![image-20251025193746446](network/image-20251025193746446.png)

---

![image-20251025204726806](network/image-20251025204726806.png)

![image-20251025203655730](network/image-20251025203655730.png)



## Missing Term in KVL

> Prof. Kolb/Whites. EE 382 Applied Electromagnetics Lecture 8: Maxwell's Equations and Electrical CIrcuits [[http://montoya.sdsmt.edu/ee382/lectures/382Lecture8.pdf](http://montoya.sdsmt.edu/ee382/lectures/382Lecture8.pdf)]

![image-20250713101205684](network/image-20250713101205684.png)



## Transmission-line

![image-20250718223340699](network/image-20250718223340699.png)

### Telegrapher’s equations

> EECS 723- Microwave Engineering Spring 2.1 -The Lumped Element Circuit Model for Transmission Lines 
>
> 1/20/2005  [[https://www.ittc.ku.edu/~jstiles/723/handouts/2_1_Lumped_Element_Circuit_Model_package.pdf](https://www.ittc.ku.edu/~jstiles/723/handouts/2_1_Lumped_Element_Circuit_Model_package.pdf)]
>
> note [[https://www.ittc.ku.edu/~jstiles/723/handouts/section_2_1_The_Lumped_Element_Circuit_Model_package.pdf](https://www.ittc.ku.edu/~jstiles/723/handouts/section_2_1_The_Lumped_Element_Circuit_Model_package.pdf)]
>
> present [[https://www.ittc.ku.edu/~jstiles/723/handouts/section_2_1_The_Lumped_Element_Circuit_Model_present.pdf](https://www.ittc.ku.edu/~jstiles/723/handouts/section_2_1_The_Lumped_Element_Circuit_Model_present.pdf)]

![image-20250713102519144](network/image-20250713102519144.png)

![image-20250713102641016](network/image-20250713102641016.png)

### Transmission Line Wave Equation

![image-20250718220504696](network/image-20250718220504696.png)

![image-20250713104729920](network/image-20250713104729920.png)

> ![image-20250718224751665](network/image-20250718224751665.png)



###  Characteristic Impedance ($Z_0$)

![image-20250713112912199](network/image-20250713112912199.png)

![image-20250713113651799](network/image-20250713113651799.png)



---

> Remember, S-parameters **don't mean much** unless you know the value of the **reference impedance **(it's frequently called Z0).



simulator will read sp file's **Z0** parameter

![image-20220430214052538](network/image-20220430214052538.png)

![image-20220430214136970](network/image-20220430214136970.png)

![image-20220430214419283](network/image-20220430214419283.png)

> The default **Z0** exported by EMX is **50**



### Complex Propagation Constant $\gamma$

*TODO* &#128197;






###  Input impedance (Line Impedance)

![image-20250718231905402](network/image-20250718231905402.png)



### Reflection Coefficient

*TODO* &#128197;

![image-20250719081121034](network/image-20250719081121034.png)



### Steady-State Solution (DC voltage division)

> Sam Palermo. [[https://people.engr.tamu.edu/spalermo/ecen689/lecture3_ee689_tlines.pdf](https://people.engr.tamu.edu/spalermo/ecen689/lecture3_ee689_tlines.pdf)]
>
> Kyoung-Jae Chung. Special Topics in Radiation Engineering (High-voltage pulsed power engineering) [[https://ocw.snu.ac.kr/sites/default/files/NOTE/Lecture_03_Transmission%20line%20theory.pdf](https://ocw.snu.ac.kr/sites/default/files/NOTE/Lecture_03_Transmission%20line%20theory.pdf)]
>
> David R. Jackson. [[https://courses.egr.uh.edu/ECE/ECE3317/SectionJackson/Class%20Notes/Notes%208%203317%20Transmission%20Lines%20(Bounce%20Diagram).pdf](https://courses.egr.uh.edu/ECE/ECE3317/SectionJackson/Class%20Notes/Notes%208%203317%20Transmission%20Lines%20(Bounce%20Diagram).pdf)]
>
> Shouri Chatterjee [[https://web.iitd.ac.in/~shouri/ell112/material/txline.pdf](https://web.iitd.ac.in/~shouri/ell112/material/txline.pdf)]
>
> How can I go from transmission line model to lumped elements model? [[https://physics.stackexchange.com/a/386603](https://physics.stackexchange.com/a/386603)]

![image-20250713090925198](network/image-20250713090925198.png)



![image-20250713084136902](network/image-20250713084136902.png)

![image-20250713091613844](network/image-20250713091613844.png)




---


> E157 Introduction to Radio Frequency Circuit Design [[https://pages.hmc.edu/mspencer/e157/fa24/](https://pages.hmc.edu/mspencer/e157/fa24/)]
>
> Eric Bogatin. Pop Quiz: When is an Interconnect Not a Transmission Line? [[https://www.signalintegrityjournal.com/blogs/4-eric-bogatin-signal-integrity-journal-technical-editor/post/265-pop-quiz-when-is-an-interconnect-not-a-transmission-line](https://www.signalintegrityjournal.com/blogs/4-eric-bogatin-signal-integrity-journal-technical-editor/post/265-pop-quiz-when-is-an-interconnect-not-a-transmission-line)]
>
> Shen Lin. On-Chip Inductance and Coupling Effects [[http://eda.ee.ucla.edu/pub/asic.pdf](http://eda.ee.ucla.edu/pub/asic.pdf)]
>
> A. Deutsch *et al*., "When are transmission-line effects important for on-chip interconnections?," in *IEEE Transactions on Microwave Theory and Techniques*, vol. 45, no. 10, pp. 1836-1846, Oct. 1997
>
> Ho, Ron. “Chip Wires: Scaling and Efficiency.” (2003). [[https://www-vlsi.stanford.edu/people/alum/pdf/0303_Ho_Wires.pdf](https://www-vlsi.stanford.edu/people/alum/pdf/0303_Ho_Wires.pdf)]
>
> —. ISSCC 2007 T3: Dealing with Issues in VLSI Interconnect Scaling, by Ron Ho
>
> Tony Chan Carusone. ISSCC 2017 T6: Signal Integrity Analysis for Gb/s Links
>
> Byungsub Kim ISSCC 2022 T11: "Basics of Equalization Techniques: Channels, Equalization, and Circuits"



## Voltage scattering

![image-20250719072111526](network/image-20250719072111526.png)

![image-20241112201300108](network/image-20241112201300108.png)

**transmitted voltage**
$$
V= \frac{2Z_l}{Z_l+R_0}\frac{V_s}{2}= \frac{Z_l}{Z_l+R_0}\cdot V_s
$$



---

![image-20250719010415229](network/image-20250719010415229.png)

![image-20250719081657119](network/image-20250719081657119.png)

> ![image-20250719081836680](network/image-20250719081836680.png)



> CHAPTER 6 Transmission-Line Essentials for Digital Electronics [[https://ws.engr.illinois.edu/sitemanager/getfile.asp?id=178](https://ws.engr.illinois.edu/sitemanager/getfile.asp?id=178)]
>
> CHAPTER 7 Transmission-Line Analysis [[https://ws.engr.illinois.edu/sitemanager/getfile.asp?id=199](https://ws.engr.illinois.edu/sitemanager/getfile.asp?id=199)]



## Voltage Transfer Function

![image-20241030220203806](network/image-20241030220203806.png)

![image-20241030220131714](network/image-20241030220131714.png)

> ![image-20241030222403947](network/image-20241030222403947.png)



### Reflection Coefficients

![image-20241030222906229](network/image-20241030222906229.png)

![image-20241030222923491](network/image-20241030222923491.png)



## Impulse Response From S-Parameters

> David Banas. *A comparison of different techniques (i.e. - windowing, vector fitting, etc.) for extracting the impulse response from S-parameters.* [[https://github.com/capn-freako/ImpulseResponseFromSparameters/tree/main](https://github.com/capn-freako/ImpulseResponseFromSparameters/tree/main)]
>
> Sam Palermo. ECEN720: High-Speed Links Circuits and Systems Spring 2025 - Lecture 3: Time-Domain Reflectometry & S-Parameter Channel Models[[https://people.engr.tamu.edu/spalermo/ecen689/lecture3_ee720_tdr_spar.pdf](https://people.engr.tamu.edu/spalermo/ecen689/lecture3_ee720_tdr_spar.pdf)]

*TODO* &#128197;

### Rational Fit



#### Matlab/rationalfit

To resolve the convergence problem of s-parameter in Spectre simulator - `rationalfit` and write Verilog-A 

![image-20220630224525565](network/image-20220630224525565.png)

```matlab
filename  = 'touchstone/ISI.S4P';
s4p = read(rfdata.data, filename);
sdd_params = s2sdd(s2p.S_Parameters, 2);
sdd21 = squeeze(sdd_params(2, 1, :));   % s21
freq = s4p.Freq;

% rational fitting
weight = ones(size(sdd21));
weight(floor(end*3/4):end) = 0.2;
weight(2:10) = 0;

[hfit, errb] = rationalfit(freq, sdd21, 'IterationLimit', [4, 16], 'Delayfactor', 0.98, ...
    'Weight', weight, 'Tolerance', -38, 'NPoles', 32);
[sdd21_fit, ff] = freqresp(hfit, freq);

figure(1)
plot(freq/1e9, db(sdd21), 'b-'); hold on;
plot(ff/1e9, db(sdd21_fit), 'r-'); hold off; grid on;
legend('sdd21', 'sdd21\_fit');
xlabel('Freq (GHz)');
ylabel('magnitude (dB)');


ts = 1e-12;
n = 2^18;
trise = 4e-14;
[yout, tout] = stepresp(hfit, ts, n, trise);
figure(2)
plot(tout*1e12, yout, 'b-'); grid on;
xlabel('Time (ps)');
ylabel('V');
title('Step Response');


% write verilog-A
writeva(hfit, 'channel_32poles.va');
```



## Using S Parameters to Estimate Q

*TODO* &#128197;



> Jeff Walling. ECE 5984 Using S Parameters to Estimate Q [[https://youtu.be/PXgM6pGIRvk?si=YDeh-COQEBXKUiw-](https://youtu.be/PXgM6pGIRvk?si=YDeh-COQEBXKUiw-)]



## Reading S-parameters

> teledynelecroy. Reading S-parameters [[https://blog.teledynelecroy.com/2020/05/](https://blog.teledynelecroy.com/2020/05/)]
>
> keysight. How to Interpret Ripple in an S Parameters Measurement [[https://docs.keysight.com/kkbopen/how-to-interpret-ripple-in-an-s-parameters-measurement-849642201.html](https://docs.keysight.com/kkbopen/how-to-interpret-ripple-in-an-s-parameters-measurement-849642201.html)]
>
> You Measured What? Four Must-Know Checks Before Trusting Your Trace S-Parameters [[https://www.signalintegrityjournal.com/articles/4083-you-measured-what-four-must-know-checks-before-trusting-your-trace-s-parameters](https://www.signalintegrityjournal.com/articles/4083-you-measured-what-four-must-know-checks-before-trusting-your-trace-s-parameters)]


*TODO* &#128197;


## Spar in Tran simulation

![image-20250705210519145](network/image-20250705210519145.png)



## Spar in AC simulation

![image-20250816221249094](network/image-20250816221249094.png)

![image-20250816221939979](network/image-20250816221939979.png)



> ![image-20250816222126241](network/image-20250816222126241.png)




## reference

[microwaves101, S-parameters (https://www.microwaves101.com/encyclopedias/s-parameters)](https://www.microwaves101.com/encyclopedias/s-parameters)

Pupalaikis, P. (2020). *S-Parameters for Signal Integrity*. Cambridge: Cambridge University Press. doi:10.1017/9781108784863

Coelho, C. P., Phillips, J. R., & Silveira, L. M. (n.d.). Robust rational function approximation algorithm for model generation. Proceedings 1999 Design Automation Conference (Cat. No. 99CH36361). doi:10.1109/dac.1999.781313

Cadence IEEE IMS 2023, Introducing the Spectre S-Parameter Quality Checker and Rational Fit Model Generator [[https://support.cadence.com/apex/ArticleAttachmentPortal?id=a1O3w000009lplhEAA](https://support.cadence.com/apex/ArticleAttachmentPortal?id=a1O3w000009lplhEAA)]

The Complex Art Of Handling S-Parameters: The importance of extraction and fitting to circuit simulation involving S-parameters  [[https://semiengineering.com/the-complex-art-of-handling-s-parameters](https://semiengineering.com/the-complex-art-of-handling-s-parameters/)]

Dr. John Choma. EE 541, Fall 2006: Course Notes #2 Scattering Parameters: Concept, Theory, and Applications [[https://www.ieee.li/pdf/essay/scattering_parameters_concept_theory_applications.pdf](https://www.ieee.li/pdf/essay/scattering_parameters_concept_theory_applications.pdf)]

Dr. Ray Kwok . Network Techniques: Conversion between Filter Transfer Function and Filter Scattering (SMatrix) Parameters [[https://www.sjsu.edu/people/raymond.kwok/docs/project172/FTF%20to%20S-Matrix%20Spring%202011.pdf](https://www.sjsu.edu/people/raymond.kwok/docs/project172/FTF%20to%20S-Matrix%20Spring%202011.pdf)]

田庆诚教授 台湾中华大学 射频电路基础（公司培训）[[https://www.bilibili.com/video/BV1LA41177wr/?p=3&share_source=copy_web&vd_source=5a095c2d604a5d4392ea78fa2bbc7249](https://www.bilibili.com/video/BV1LA41177wr/?p=3&share_source=copy_web&vd_source=5a095c2d604a5d4392ea78fa2bbc7249)]
