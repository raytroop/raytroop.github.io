---
title: Custom Design with FinFETs
date: 2022-12-10 16:56:07
tags:
- finfet
categories:
- analog
mathjax: true
---



## Design Considerations

![image-20221210165644336](FinFET-Considerations/image-20221210165644336.png)



![image-20221210165916985](FinFET-Considerations/image-20221210165916985.png)



## Modeling Consideration

![image-20221217152830191](FinFET-Considerations/image-20221217152830191.png)

![image-20221210170042233](FinFET-Considerations/image-20221210170042233.png)



![mos_pro](FinFET-Considerations/mos_pro.drawio.svg)
$$\begin{align}
R_{d1} &\propto \frac{1}{N_{fins}} \\
R_{s1} &\propto \frac{1}{N_{fins}} \\
R_{g1} &\propto N_{fins} \\
C_{gd} &\propto N_{fins} \cdot N_{fingers} \cdot N_{multipler} \\
C_{gs} &= Cgd \\
C_{g1d} &\propto N_{fins} \\
C_{g1s} &= C_{g1d} \\
C_{g1d1} &\propto N_{fins} \\
C_{g1s1} &= C_{g1d1}  \\
C_{g1d1} &\simeq 2\times C_{g1d}
\end{align}$$



![image-20230708221056420](FinFET-Considerations/image-20230708221056420.png)



## Layout Consideration

### PODE & CPODE

> The PODE devices is extracted as parasitic devices in post-layout netlist

![image-20220213172653116](FinFET-Considerations/image-20220213172653116.png)



**DDB** is the **PODE** (poly on diffusion edge) in TSMC 16FFC process.

**SDB** is the **CPODE** (Common PODE) in TSMC 16FFC process.

> PO on OD edge (PODE) is a must and to define GATE that abuts OD vertical edge
>
> CPODE is used to connect two PODE cells together. It will isolate OD to save 1 poly pitch, via STI; Additional mask (12N) is required for manufacture 



![image-20221210145232826](FinFET-Considerations/image-20221210145232826.png)

![image-20221210150847737](FinFET-Considerations/image-20221210150847737.png)

### SAC & SAGC

#### self-aligned diffusion contacts (SACs)

As shown in Fig. 35 in older planar technology nodes, gate pitch is so relaxed such that S/D contacts and gate contacts can easily be placed next to each other without causing any shorting risk (see Fig. 35(a)). 

**As the gate pitch scales, there’s no room to put gate contacts next to S/D contacts, and gatecontacts have been pushed away from the active region and are only placed on the STI region.**

![image-20230708221916716](FinFET-Considerations/image-20230708221916716.png)

In addition, at tight gate pitch, even forming *S/D contact* without shorting to *gate metal* becomes very challenging. 

The idea of **self-aligned contacts (SAC)** has been introduced to mitigate the issue of S/D contact to gate shorts. 

As shown in Fig. 35(b), *the gate metal is fully encapsulated by a dielectric spacer and gate cap*, which protects the gate from shorting to the S/D contact. 

![image-20230708230238362](FinFET-Considerations/image-20230708230238362.png)



>  A dielectric cap is added on top of the gate so that if the contact overlaps the gate, no short occurs.
>
> **MD** layer represent SACs in PDK

![image-20230709005334372](FinFET-Considerations/image-20230709005334372.png)



#### self-aligned gate contacts (SAGCs)

**Self-aligned gate contacts (SAGCs)** have also been implemented and Denser standard cells can be achieved by eliminating the need to land contacts on the gate outside the active area.

SAGCs require the source/drain contacts to be capped with an insulator that is different from both contact and gate cap dielectrics to protect the source/drain contacts against a misaligned gate contact etch.



![image-20230708233009568](FinFET-Considerations/image-20230708233009568.png)



![image-20230708232429240](FinFET-Considerations/image-20230708232429240.png)

> According to the DRC of T foundary, poly extension > 0 um and space between MP and OD > 0 um., which demonstrate self-aligned gate contact is **not** introduced.





##### Contacted-Poly-Pitch (CPP)

> Wider Contacted-Poly-Pitch allows wider MD and VD size, which help reduce MEOL IRdrop

![Schematic representation of a logic standard cell layout (CPP = contacted poly pitch, FP = fin pitch, MP = metal pitch; cell height = number of metal lines per cell x MP).](https://www.imec-int.com/_next/image?url=%2Fsites%2Fdefault%2Ffiles%2F2022-02%2FFigure%25201%2520-%2520Logic%2520standard%2520cell%2520scaling.JPG&w=3840&q=75)

*Naoto Horiguchi. Entering the Nanosheet Transistor Era  [[link](https://www.imec-int.com/en/articles/entering-nanosheet-transistor-era-0)]*



### Gate Resistance

![image-20230709000326683](FinFET-Considerations/image-20230709000326683.png)

![image-20230709004432013](FinFET-Considerations/image-20230709004432013.png)

![image-20230709000637817](FinFET-Considerations/image-20230709000637817.png)

![image-20230709003917922](FinFET-Considerations/image-20230709003917922.png)





#### non-quasistatic (NQS) effect





## reference

Tom Quan, TSMC, Bob Lefferts, Fred Sendig, Synopsys, Custom Design with FinFETs - Best practices designing mixed-signal IP

Jacob, Ajey & Xie, Ruilong & Sung, Min & Liebmann, Lars & Lee, Rinus & Taylor, Bill. (2017). Scaling Challenges for Advanced CMOS Devices. International Journal of High Speed Electronics and Systems. 26. 1740001. 10.1142/S0129156417400018.

Joddy Wang, Synopsys ["FinFET SPICE Modeling"](https://www.mos-ak.org/washington_dc_2015/presentations/T03_Joddy_Wang_MOS-AK_Washington_DC_2015.pdf)  Modeling of Systems and Parameter Extraction Working Group 8th International MOS-AK Workshop (co-located with the IEDM Conference and CMC Meeting) Washington DC, December 9 2015

A. L. S. Loke et al., "Analog/mixed-signal design challenges in 7-nm CMOS and beyond," 2018 IEEE Custom Integrated Circuits Conference (CICC), San Diego, CA, USA, 2018, pp. 1-8, doi: 10.1109/CICC.2018.8357060.[[slides](https://ewh.ieee.org/r6/san_diego/sscs/events/slides/2018_05_23_AMSDesignChallengesIn7nmCMOS_AlvinLoke.pdf)]

Prof. Adam Teman, Advanced Process Technologies, [[pdf](https://www.eng.biu.ac.il/temanad/files/2022/03/Lecture-2-Advanced-Process-Technologies.pdf)]

Luke Collins. FinFET variability issues challenge advantages of new process [[link](https://www.techdesignforums.com/blog/2014/04/16/finfet-variability-challenges-advantages/)]

Loke, Alvin. (2020). FinFET technology considerations for circuit design (invited short course). BCICTS 2020 Monterey, CA

Alvin Leng Sun Loke, TSMC. Device and Physical Design Considerations for Circuits in FinFET Technology", ISSCC 2020

Prof. Adam Teman. Advanced Process Technologies [[pdf](https://www.eng.biu.ac.il/temanad/files/2022/03/Lecture-2-Advanced-Process-Technologies.pdf)]

A. L. S. Loke, C. K. Lee and B. M. Leary, "Nanoscale CMOS Implications on Analog/Mixed-Signal Design," 2019 IEEE Custom Integrated Circuits Conference (CICC), Austin, TX, USA, 2019, pp. 1-57, doi: 10.1109/CICC.2019.8780267.

A. L. S. Loke, Migrating Analog/Mixed-Signal Designs to FinFET Alvin Loke / Qualcomm. 2016 Symposia on VLSI Technology and Circuits
