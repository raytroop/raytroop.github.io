---
title: ESD and Protection
date: 2022-06-09 23:13:59
tags:
categories:
- analog
---
The **ESD design window** is defined as the difference between the breakdown voltage of the functional circuit (red line) and the maximum signal voltage (blue line)
![esddesignwindow-evolution](esd-protection/esddesignwindow-evolution.jpg)

## TLP

What makes **TLP** different than **ESD** ?

- **ESD** tests simulate real world events (HBM, MM, CDM)
- **TLP** does not simulate any real-world event
- **ESD** tests record failure level (*Qualification*)
- **TLP** tests record failure level and device behavior (*Characterization*)

> TLP is not a qualification test, but a characterization method, which describes the resistance of a device for a given stimulus, aka. *Device Characterization*
>
> Unlike ESD waveforms, TLP does not mimic any real world event

![image-20220609234548431](esd-protection/image-20220609234548431.png)

### TLP  and Curve Tracing

- Curve Tracing is DC; TLP is a short pulse
  - Shorter pulse - Reduced duty cycle, less heating, which means higher voltage before failure
  - Controlled Impedance - Allows device behavior to be observed
- Both measure resistance of device with increasing voltage

![image-20220609235252444](esd-protection/image-20220609235252444.png)

### Device Characterization with TLP

- Turn-on time
- Snapback voltage
- Performance changes with rise time

![image-20220609235427204](esd-protection/image-20220609235427204.png)

### VF-TLP and CDM differences

Question:

How well will VF-TLP results predict CDM testing performance?

Answer:

VF-TLP can be a guide to CDM failure levels, and provide a lot of understanding of a circuit's operation during CDM stressing, but simple correlations between VF-TLP failure current level and CDM withstand voltage levels are difficult to establish.

## snapback device
Unfortunately, this protection concept is not effective anymore in advanced FinFET technology.
Our analysis showed that both core and IO transistors are damaged at the onset of snapback in several FinFET processes.
![snapback](esd-protection/snapback.PNG)

## power clamp
Thanks to the device scaling the area is actually reasonable. However, the leakage becomes the main bottleneck.
![bigfet-concept](esd-protection/bigfet-concept.jpg)



## ESD diode

![image-20220618123654830](esd-protection/image-20220618123654830.png)

![image-20220618123821117](esd-protection/image-20220618123821117.png)

![image-20220618124644879](esd-protection/image-20220618124644879.png)

> both diode are reverse-biased in normal operation, the PN Junction capacitance is proportional to forward-bias voltage

| Device           |                           |
| ---------------- | ------------------------- |
| ndio_mac         | N+/P-well Diode           |
| pdio_mac         | P+/N-well Diode           |
| ndio_18_mac      | 1.8V N+/P-well Diode      |
| pdio_18_mac      | 1.8V P+/N-well Diode      |
| ndio_hia18_mac   | N-HIA Diode               |
| pdio_hia18_mac   | P-HIA Diode               |
| ndio_gated18_mac | Thick Oxide N-Gated Diode |
| pdio_gated18_mac | Thick Oxide P-Gated Diode |

> HIA_DIO can be used for logic or high speed circuits ESD protection
>
> HIA: high current application purpose (High Amp)
>
> There is no process difference between HIA_DIO and regular diode



![image-20220618191312489](esd-protection/image-20220618191312489.png)

![image-20220618183241535](esd-protection/image-20220618183241535.png)

![image-20220618191405428](esd-protection/image-20220618191405428.png)

| width (W)                    | 2.020E-07   |
| ---------------------------- | ----------- |
| **Length (L)**               | 1.922E-06   |
| **ArrayY (Ny)**              | 2           |
| **Perimeter (Ny\*2\*(W+L))** | 8.496E-06   |
| **Area (Ny\*W\*L)**          | 7.76488E-13 |

> - diode is drain/source originated, which is different from MOS (Gate originated) 
>
> - The perimeter of diode in DRC is different from  that in PERC deck, where PERC excludes the the left and right edge of OD

### MOS

![image-20220618191906210](esd-protection/image-20220618191906210.png)

![image-20220618192253726](esd-protection/image-20220618192253726.png)

![image-20220618192325486](esd-protection/image-20220618192325486.png)

> `l` in netlist has different definition for MOS and diode.
>
> MOS: length of channel
>
> diode: Gate space



## Reference

Introduction to Transmission Line Pulse (TLP), URL: [https://tools.thermofisher.com/content/sfs/brochures/TLP%20Presentation%20May%202009.pdf](https://tools.thermofisher.com/content/sfs/brochures/TLP%20Presentation%20May%202009.pdf)

VF-TLP and CDM differences, URL: [https://www.grundtech.com/app-note-vf-tlp-cdm-differences](https://www.grundtech.com/app-note-vf-tlp-cdm-differences)

ESD-Testing: HBM to very fast TLP URL: [https://www.thierry-lequeu.fr/data/ESREF/2004/Tut5.pdf](https://www.thierry-lequeu.fr/data/ESREF/2004/Tut5.pdf)

S. Kim et al., "Technology Scaling of ESD Devices in State of the Art FinFET Technologies," 2020 IEEE Custom Integrated Circuits Conference (CICC), 2020, pp. 1-6, doi: 10.1109/CICC48029.2020.9075899.

Barth, Jon. "TLP and VFTLP Testing of Integrated Circuit ESD Protection." (2015).
ESD protection for FinFET processes URL: [https://monthly-pulse.com/2021/01/19/esd-protection-for-finfet-processes/](https://monthly-pulse.com/2021/01/19/esd-protection-for-finfet-processes/)

Yuanzhong Zhou, D. Connerney, R. Carroll and T. Luk, "Modeling MOS snapback for circuit-level ESD simulation using BSIM3 and VBIC models," Sixth international symposium on quality electronic design (isqed'05), 2005, pp. 476-481, doi: 10.1109/ISQED.2005.81.
