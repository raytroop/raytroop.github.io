---
title: cascaded PLLs & wireline transceiver
date: 2025-05-24 07:32:02
tags:
categories: analog
mathjax: true
---

> To understand the impact of the clock jitter on the performance of a wireline system, *the transfer functions of the PLL in the transmitter side* and *the CDR loop in the receiver* should be taken into consideration
>
> ![image-20250524111908032](cascaded-plls/image-20250524111908032.png)



![image-20250524091655525](cascaded-plls/image-20250524091655525.png)

![image-20250524131517606](cascaded-plls/image-20250524131517606.png)



> *the **minimum** jitter* occurs at the point where the *transmit PLL UGB is **minimum*** and *the CDR UGB is **maximized***

- the net rms jitter that impacts the performance of a wireline transceiver is much lower than the rms jitter of the transmit PLL
- the jitter requirements of the transmit PLL on the wireline system is much more relaxed compared to the wireless transceiver  

## reference

Chembiyan T, A General Theory of Cascaded PLL Design [[link](https://media.licdn.com/dms/document/media/v2/D561FAQFvRADxXYwdhg/feedshare-document-pdf-analyzed/B56Zb4ktDGHwAY-/0/1747927149379?e=1749081600&v=beta&t=r_mMzwFUR0kPR0LdWSbeEGzMVk5hOC2qaiVqMVZbnGA)]

Nicola Da Dalt, ISSCC 2012 T5: JITTER basic and advanced concepts, statistics and applications [[https://www.nishanchettri.com/isscc-slides/2012%20ISSCC/TUTORIALS/ISSCC2012Visuals-T5.pdf](https://www.nishanchettri.com/isscc-slides/2012%20ISSCC/TUTORIALS/ISSCC2012Visuals-T5.pdf)]
