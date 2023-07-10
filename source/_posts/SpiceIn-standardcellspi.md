---
title: SpiceIn foundary's standard cell's spice netlist
date: 2022-10-22 22:42:37
tags:
- virtuoso
categories:
- cad
---

use **SpiceIn** GUI feature to map MOS parameter correctly in generated schematic

### Input

![image-20221022224745955](SpiceIn-standardcellspi/image-20221022224745955.png)

> The mos's total width (parameter name "w") value will update during **SpiceIn** trigger CDF callback automatically

### Output

![image-20221022225143844](SpiceIn-standardcellspi/image-20221022225143844.png)

### Device Map

![image-20221022225224751](SpiceIn-standardcellspi/image-20221022225224751.png)

> **User Prop Mapping** is significant setup, both *xxx.spi* and *Edit CDF* provide the essential information.
>
> The map syntax is *spice_para0 cdf_para0 spice_para1 cdf_para01 ... spice_paraN cdf_paraN*

![image-20221022225742497](SpiceIn-standardcellspi/image-20221022225742497.png)



### reference

Article (20488179) Title: How to use SpiceIn GUI feature to map MOS parameter correctly in generated schematic
URL: [https://support.cadence.com/apex/ArticleAttachmentPortal?id=a1O3w000009bdPWEAY](https://support.cadence.com/apex/ArticleAttachmentPortal?id=a1O3w000009bdPWEAY)

Article (11724692) Title: SpiceIn maps the netlist parameter to the CDF parameter incorrectly on the generated schematic devices  (e.g. w to wf)
URL: [https://support.cadence.com/apex/ArticleAttachmentPortal?id=a1Od0000000nZ2CEAU](https://support.cadence.com/apex/ArticleAttachmentPortal?id=a1Od0000000nZ2CEAU)
