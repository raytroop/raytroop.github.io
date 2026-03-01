---
title: Digitally Enhanced Mixed Signal Systems
date: 2024-12-08 15:45:16
tags:
categories:
- dsp
mathjax: true
---

*TODO* &#128197;



## ADC Calibration

> Ahmed Ali, ISSCC 2021 T5: Calibration Techniques in ADCs [[https://www.nishanchettri.com/isscc-slides/2021%20ISSCC/TUTORIALS/ISSCC2021-T5.pdf](https://www.nishanchettri.com/isscc-slides/2021%20ISSCC/TUTORIALS/ISSCC2021-T5.pdf)]
>

*TODO* &#128197;

### Offset Calibration

long-term average of all 32 sub-ADC samples = 0




### Gain Calibration

long-term average of *absolute values* of all 32 sub-ADC samples should be equal



### Background vs. foreground

*TODO* &#128197;







## Linear phase

![image-20241213232002042](digitally-enhanced/image-20241213232002042.png)

---

![image-20241213233748837](digitally-enhanced/image-20241213233748837.png)

![image-20241213233917966](digitally-enhanced/image-20241213233917966.png)

> [[https://web.ece.ucsb.edu/~yoga/courses/DSP/P10_Linear_phase_FIR.pdf](https://web.ece.ucsb.edu/~yoga/courses/DSP/P10_Linear_phase_FIR.pdf)]





## Digital DC Offset Correction

![image-20241229122711845](digitally-enhanced/image-20241229122711845.png)
$$
X- Y\cdot \beta z^{-1}\cdot \frac{1}{1-z^{-1}} = Y
$$
therefore
$$
\frac{Y}{X} = \frac{1-z^{-1}}{1-(1-\beta)z^{-1}}
$$



## VDD Droop Mitigation

![image-20250105134745277](digitally-enhanced/image-20250105134745277.png)

speed of voltage monitor does matter










## reference

Chadi Jabbour, ed, Digitally Enhanced Mixed Signal Systems. IET 2019

Jiang X, ed. *Digitally-Assisted Analog and Analog-Assisted Digital IC Design*. Cambridge University Press; 2015.

Ping-Hsuan Hsieh. SSCS Events: *Digitally-Enhanced Clock Generation and Distribution*; 20 August 2025.

ISSCC 2024 FORUM 3: Digitally Enhanced Analog Circuits: Trends & State-of-the-art Designs

Albert Jerng. ISSCC2012 T7: *Digital Calibration for RF Transceivers* [[https://www.nishanchettri.com/isscc-slides/2012%20ISSCC/TUTORIALS/ISSCC2012Visuals-T7.pdf](https://www.nishanchettri.com/isscc-slides/2012%20ISSCC/TUTORIALS/ISSCC2012Visuals-T7.pdf)]

Ahmed M. A. Ali. ISSCC2021 T5: *Calibration Techniques in ADCs* [[https://www.nishanchettri.com/isscc-slides/2021%20ISSCC/TUTORIALS/ISSCC2021-T5.pdf](https://www.nishanchettri.com/isscc-slides/2021%20ISSCC/TUTORIALS/ISSCC2021-T5.pdf)]

Salvatore Levantino. ISSCC2024 T5: *Calibration Techniques in PLLs* [[https://www.nishanchettri.com/isscc-slides/2024%20ISSCC/TUTORIALS/T5.pdf](https://www.nishanchettri.com/isscc-slides/2024%20ISSCC/TUTORIALS/T5.pdf)]

Chadi Jabbour, Telecom Paristech. ISCAS 2019 T12: Digitally Enhanced Mixed Signal Systems [[https://www.youtube.com/watch?v=rACuCSDm5jQ](https://www.youtube.com/watch?v=rACuCSDm5jQ)]

---

B. Farhang-Boroujeny (2013), *Adaptive Filters: Theory and Applications* (2nd ed.). John Wiley & Sons, Inc.

Simon O. Haykin (2014), "Adaptive Filter Theory" Prentice-Hall, Inc. 5rd edition

Diniz, P. S. R. (2020). *Adaptive Filtering: Algorithms and Practical Implementation* (5th ed.). Springer

Sen M. Kuo. Real-Time Digital Signal Processing: Fundamentals, Implementations and Applications, 3rd Edition. John Wiley & Sons 2013

Stankovic, Ljubisa. (2015). Digital Signal Processing with Selected Topics. 

---

A. Chan Carusone and D. A. Johns, "Analog Filter Adaptation Using a Dithered Linear Search Algorithm," *IEEE Int. Symp. Circuits and Syst.*, May 2002. [[PDF](http://www.eecg.utoronto.ca/~tcc/iscas_02a.pdf)], [[Slides]](http://www.eecg.utoronto.ca/~tcc/iscas_02a_slides.pdf)

—, Ph. D. Thesis, "Digital Algorithms for Analog Adaptive Filters", Feb. 2002. [[http://www.eecg.utoronto.ca/~tcc/thesis.pdf]](http://www.eecg.utoronto.ca/~tcc/thesis.pdf)

—, "Analog Adaptive Filters," tutorial at the *IEEE Int. Symp. Circuits and Syst.*, Bangkok, Thailand, May 2003. [[http://www.eecg.utoronto.ca/~tcc/iscas03_tutorial.pdf](http://www.eecg.utoronto.ca/~tcc/iscas03_tutorial.pdf)]

—, 2022 Optimization Tools for Future Wireline Transceivers [[https://www.ieeetoronto.ca/wp-content/uploads/2022/12/UofT-Future-of-Wireline-Workshop-2022.pdf](https://www.ieeetoronto.ca/wp-content/uploads/2022/12/UofT-Future-of-Wireline-Workshop-2022.pdf)]

David Johns, "Integrated Circuits for Digital Communications" [[https://www.eecg.toronto.edu/~johns/nobots/courses/ece1392/slides.pdf](https://www.eecg.toronto.edu/~johns/nobots/courses/ece1392/slides.pdf)]

Tai-Haur Kuo "Advanced Analog IC Design for Communications" [[http://msic.ee.ncku.edu.tw/course/AdvancedAnalogICDesign/AdvancedAnalogICDesign.html](http://msic.ee.ncku.edu.tw/course/AdvancedAnalogICDesign/AdvancedAnalogICDesign.html)]

