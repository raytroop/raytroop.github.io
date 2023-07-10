---
title: How to fix Electromigration ?
date: 2022-05-03 19:53:27
tags:
- em
- dfm
- layout
- emir
categories:
- analog
---

| Type    | wider wire | downsize drivers | decrease fanout |
| ------- | ---------- | ---------------- | --------------- |
| RJ JMAX |            | &check;          | &check;         |
| JAVG    |            |                  |                 |
| JABSAVG |            |                  |                 |
| JACPEAK |            |                  |                 |
| JACRMS  | &check;    | &check;          | &check;         |

> - Iavg
>
>   The average value of the current, which is the effective DC current
>
> - Irms
>
>   Irms rule relates to the heat or Joule-heating of metal lines
>   
> - Ipeak
>
>   The main goal of the Ipeak limits is to ensure that no thermal breakdown could occur on single overshoot events. If the signal may not have a high current density but if it has a very large peak current density, then, local melting will happen and cause failures



![image-20220503205418275](fix-em/image-20220503205418275.png)



**reference**

Posser, Gracieli & Sapatnekar, Sachin & Reis, Ricardo. (2017). Electromigration Inside Logic Cells. 10.1007/978-3-319-48899-8. 

A. B. Kahng, S. Nath and T. S. Rosing, "On potential design impacts of electromigration awareness," 2013 18th Asia and South Pacific Design Automation Conference (ASP-DAC), 2013, pp. 527-532, doi: 10.1109/ASPDAC.2013.6509650.

Kumar, Neeraj and Mohammad S. Hashmi. “Study, analysis and modeling of electromigration in SRAMs.” (2014).

N. S. Nagaraj, F. Cano, H. Haznedar and D. Young, "A practical approach to static signal electromigration analysis," Proceedings 1998 Design and Automation Conference. 35th DAC. (Cat. No.98CH36175), 1998, pp. 572-577, doi: 10.1109/DAC.1998.724536.

Blaauw, David & Oh, Chanhee & Zolotov, Vladimir & Dasgupta, Aurobindo. (2003). Static electromigration analysis for on-chip signal interconnects. Computer-Aided Design of Integrated Circuits and Systems, IEEE Transactions on. 22. 39 - 48. 10.1109/TCAD.2002.805728. 
