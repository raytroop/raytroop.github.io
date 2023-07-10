---
title: Isolation cells
date: 2022-05-27 10:18:10
tags:
- iso
- aon
categories:
- digital
---

Isolation cells are additional cells inserted by the synthesis tools for isolating the buses/wires crossing from **power-gated domain** of a circuit to its always-on domain (**AON**). 

> To prevent corruption of always-on domain, we clamp the nets crossing the power domains to a value depending upon the design.

*A simple circuit having a switchable (or gated) power domain*

![isolation-cells-1-1](isocells/isolation-cells-1-1.webp)

*The circuit shown in Figure 1, after isolation cells are inserted*

![isolation-cells-2](isocells/isolation-cells-2.webp)

### Always-On Buffer

![640?wx_fmt=png](https://img-blog.csdnimg.cn/img_convert/1c84b9b7423b064b12b09b1e72b641e5.png)

![image-20230211001607578](isocells/image-20230211001607578.png)

![image-20230211001708189](isocells/image-20230211001708189.png)

![image-20230211001849150](isocells/image-20230211001849150.png)

### reference

Isolation cells and Level Shifter cells URL: [https://vlsitutorials.com/isolation-cells-level-shifter-cells-low-power-vlsi/](https://vlsitutorials.com/isolation-cells-level-shifter-cells-low-power-vlsi/)
