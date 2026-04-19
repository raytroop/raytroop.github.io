---
title: Signal Integrity Characterization
date: 2025-04-19 09:51:01
tags:
categories:
- sipi
mathjax: true
---



## TDR Impedance

> Amit Bahl, How TDR Impedance Measurements Work [[https://www.protoexpress.com/blog/tdr-impedance-measurements/](https://www.protoexpress.com/blog/tdr-impedance-measurements/)]
>
> Minh Quach. Signal Integrity Consideration and Analysis 4/30/2004 *Frequency & Time Domain Measurements/Analysis* [[https://ewh.ieee.org/r5/denver/sscs/Presentations/2004_04_Quach.pdf](https://ewh.ieee.org/r5/denver/sscs/Presentations/2004_04_Quach.pdf)]
>
> 江上渔樵, 在ADS中查看TDR的3种方法 [[https://zhuanlan.zhihu.com/p/420350734](https://zhuanlan.zhihu.com/p/420350734)]



### VtStep vs TDR

> Abhargava, *TDR Analysis using Agilent ADS* [[https://abhargava.wordpress.com/wp-content/uploads/2014/01/performing-tdr-analysis-using-agilent-ads.pdf](https://abhargava.wordpress.com/wp-content/uploads/2014/01/performing-tdr-analysis-using-agilent-ads.pdf)]
>
> Mike Steinberger, *TDR: Reading the Tea Leaves* [[https://siguys.com/wp-content/uploads/2016/01/TDR_TeaLeaves.pdf](https://siguys.com/wp-content/uploads/2016/01/TDR_TeaLeaves.pdf)]

![image-20260419164454411](si/image-20260419164454411.png)

![image-20260419165629435](si/image-20260419165629435.png)

### S11 vs TDR

> Vladimir Dmitriev-Zdorov, Mentor Graphics, DesignCon 2014, *Computation of Time Domain Impedance Profile from S-Parameters: Challenges and Methods* [[link](https://www.researchgate.net/publication/339032423_DesignCon_2014_Computation_of_Time_Domain_Impedance_Profile_from_S-Parameters_Challenges_and_Methods)]
>
> [ADS: 1-10] TDR Impedance (Part 2) TDRインピーダンス解析 [[https://youtu.be/ACINktqpM50](https://youtu.be/ACINktqpM50)]
>
> ADS `tdr_sp_imped`

*TODO* &#128197;





## Reading S-parameters

> teledynelecroy. Reading S-parameters [[https://blog.teledynelecroy.com/2020/05/](https://blog.teledynelecroy.com/2020/05/)]
>
> keysight. How to Interpret Ripple in an S Parameters Measurement [[https://docs.keysight.com/kkbopen/how-to-interpret-ripple-in-an-s-parameters-measurement-849642201.html](https://docs.keysight.com/kkbopen/how-to-interpret-ripple-in-an-s-parameters-measurement-849642201.html)]
>
> You Measured What? Four Must-Know Checks Before Trusting Your Trace S-Parameters [[https://www.signalintegrityjournal.com/articles/4083-you-measured-what-four-must-know-checks-before-trusting-your-trace-s-parameters](https://www.signalintegrityjournal.com/articles/4083-you-measured-what-four-must-know-checks-before-trusting-your-trace-s-parameters)]

*TODO* &#128197;





### Ripple in an S Parameters

![image-20260110134112029](si/image-20260110134112029.png)

![image-20260110134010253](si/image-20260110134010253.png)









### Using S Parameters to Estimate Q

> Jeff Walling. ECE 5984 Using S Parameters to Estimate Q [[https://youtu.be/PXgM6pGIRvk](https://youtu.be/PXgM6pGIRvk)]

*TODO* &#128197;





## reference

Bogatin, Eric. 2020. *Bogatin’s Practical Guide to Transmission Line Design and Characterization for Signal Integrity Applications / .Eric Bogatin.* Artech House.

keysight, Signal Integrity Characterization Techniques [[pdf](https://www.keysight.com/us/en/assets/7121-1077/ebooks/Signal-Integrity-Characterization-Techniques.pdf)]

Tim Wang-Lee, DesignCon 2026 KEF: Mastering TDR and De-embedding Through Simulation and Measurement [[link](https://www.keysight.com/us/en/assets/9926-01167/seminar-materials/DesignCon26-KEF-Bridging-Worlds-Mastering-TDR-and-De-embedding-through-Simulation-and-Measurement.pdf)]

Csaba SOOS, Signal and Power Integrity Design Practices [[https://indico.cern.ch/event/358837/attachments/714663/1930957/Signal_and_Power_Integrity_Practices.pdf](https://indico.cern.ch/event/358837/attachments/714663/1930957/Signal_and_Power_Integrity_Practices.pdf)]

