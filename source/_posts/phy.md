---
title: Physical Layer (PHY) 
date: 2026-03-31 20:44:28
tags:
categories:
- link
mathjax: true
---

![image-20260331225337870](phy/image-20260331225337870.png)

| Sublayer | Layer Type      | Primary Responsibility | Key Processes                                        |
| :------- | :-------------- | :--------------------- | :--------------------------------------------------- |
| **PCS**  | Digital         | Data Preparation       | Encoding (64b/66b), Scrambling, Alignment            |
| **PMA**  | Mixed-Signal    | Serialization & Timing | SerDes, Clock Recovery, Data Framing                 |
| **PMD**  | Analog/Physical | Medium Interface       | Signal Conversion (Optics/Electrical), MDI Interface |



## RX Elastic Buffer

> Joe Winkles, *Elastic Buffer Implementations in PCI Express Devices* [[pdf](https://www.docdroid.net/B4VS5Nv/mindshare-pcie-elastic-buffer-pdf)]

bridge between ***Recovered Clock Domain*** and ***Local Clock Domain***

![image-20260331221404321](phy/image-20260331221404321.png)

![image-20260331231925843](phy/image-20260331231925843.png)

## Lane-to-Lane Skew

*TODO* &#128197;



## First In First Out (FIFO) 

> Clifford E. Cummings, *Simulation and Synthesis Techniques for Asynchronous FIFO Design with Asynchronous Pointer Comparisons* [[pdf](https://twins.ee.nctu.edu.tw/courses/ip_core_04/resource_pdf/cummings1_final.pdf)]

*TODO* &#128197;



## Scrambler

*TODO* &#128197;



## Link Training and Initialization (LTSSM)

*TODO* &#128197;



## reference

John Swindle, *PCIe 1.1 Phy Design Considerations*

Hidehiro Toyoda, Shinji Nishimura, and Masato Shishikura, *PMD architecture with skew compensation mechanism for parallel link* [[https://www.ieee802.org/3/hssg/public/nov06/nishimura_01_1106.pdf](https://www.ieee802.org/3/hssg/public/nov06/nishimura_01_1106.pdf)]

Kamesh Velmail, Samsung, *Challenges, Complexities and Advanced Verification Techniques in Stress Testing of Elastic Buffer in High Speed SERDES IPs* [[pdf](https://dvcon-proceedings.org/wp-content/uploads/challenges-complexities-and-advanced-verification-techniques-in-stress-testing-of-elastic-buffer-in-high-speed-serdes-ips-paper.pdf)]

