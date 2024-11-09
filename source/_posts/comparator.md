---
title: Clocked Comparators
date: 2024-09-02 21:52:39
tags:
categories:
- analog
mathjax: true
---



## Noise Analysis

*TODO* &#128197;

The StrongARM latch completes switching actions and noise injections *even before the output begins to change*



## Noise Simulation

### PSS + Pnoise Method



> SNR during sampling region and decision region increase
>
> SNR during regeneration region is *constant*, where noise is critical 

$$
\text{SNR} = \frac{V_{o,sig}^2}{V_{o,n}^2} = \frac{V_{i,sig}^2}{V_{i,n}^2}
$$

we can get $V_{i,n}^2 = \frac{V_{i,sig}^2}{\text{SNR}}$, which is constant also

That is 
$$
V_{i,n}^2 = \frac{V_{i,sig}^2}{V_{o,sig}^2}V_{o,n}^2 = \frac{V_{o,n}^2}{A_v^2}
$$
where $V_{i,sig}$ is constant signal is applied to input of comparator



---

![image-20241109163928889](comparator/image-20241109163928889.png)



### Transient Noise Method

> Noise **Fmax** sets the bandwidth of the random noise sources that are injected at each time point in the transient analysis

---

![image-20241109154528160](comparator/image-20241109154528160.png)

![image-20241109154249513](comparator/image-20241109154249513.png)

> We can identify the RMS noise value easily by looking at 15.9% or 84.1% of CDF ($1\sigma$), the input-referred noise in the RMS is 0.9mV 

![image-20241109160311684](comparator/image-20241109160311684.png)

Thus, if $V_S$ is chosen so as to reduce the probability of zeros to 16%, then $V_S = 1\sigma$, which is also the total **root-mean square (rms)** noise referred to the input.



### Comparison of two methods





> E. Gillen, G. Panchanan, B. Lawton and D. O'Hare, "Comparison of transient and PNOISE simulation techniques for the design of a dynamic comparator," 2022 33rd Irish Signals and Systems Conference (ISSC), Cork, Ireland, 2022, pp. 1-5
>
> Chenguang Yang, "Comparator Design for High Speed ADC" [[https://lup.lub.lu.se/luur/download?func=downloadFile&recordOId=9164380&fileOId=9164388](https://lup.lub.lu.se/luur/download?func=downloadFile&recordOId=9164380&fileOId=9164388)]
>
> J. Conrad, J. Kauffman, S. Wilhelmstatter, R. Asthana, V. Belagiannis and M. Ortmanns, "Confidence Estimation and Boosting for Dynamic-Comparator Transient-Noise Analysis," *2024 22nd IEEE Interregional NEWCAS Conference (NEWCAS)*, Sherbrooke, QC, Canada, 2024, pp. 1-5





##  Common-Mode (Vcmi) Variation Effects

![image-20240925225059596](comparator/image-20240925225059596.png)

![image-20240925225823184](comparator/image-20240925225823184.png)





## offset simulation

*TODO* &#128197;



> T. Caldwell. ECE 1371S Advanced Analog Circuits [[http://individual.utoronto.ca/trevorcaldwell/course/comparators.pdf](http://individual.utoronto.ca/trevorcaldwell/course/comparators.pdf)]
>
> Eric Chang. EECS240-s18 Discussion 9 
>



---

![image-20241109092310123](comparator/image-20241109092310123.png)

> Graupner, Achim & Sobe, Udo. (2007). Offset-Simulation of Comparators. [[https://designers-guide.org/analysis/comparator.pdf](https://designers-guide.org/analysis/comparator.pdf)]
>
> ```
> Comment on "Offset-Simulation of Comparators"
> 
> If the input referred offset follows a normal distribution than it is sufficient to apply a single offset voltage to calculate the offset voltage.
> See details in Razavi, B., The StrongARM Latch [A Circuit for All Seasons], IEEE Solid-State Circuits Magazine, Volume:7, Issue: 2, Spring 2015
> ```



---

> Omran, Hesham. (2019). Fast and accurate technique for comparator offset voltage simulation. Microelectronics Journal. 89. 10.1016/j.mejo.2019.05.004. 
>
> Matthews, Thomas W. and Perry L. Heedley. “A simulation method for accurately determining DC and dynamic offsets in comparators.” *48th Midwest Symposium on Circuits and Systems, 2005.* (2005): 1815-1818 Vol. 2. [[https://athena.ecs.csus.edu/~pheedley/MSDL/MSDL_DOTB_cmp_test_bench_MWSCAS05.pdf](https://athena.ecs.csus.edu/~pheedley/MSDL/MSDL_DOTB_cmp_test_bench_MWSCAS05.pdf)]



## Hysteresis  


> P. Bruschi: Notes on Mixed Signal Design [http://www2.ing.unipi.it/~a008309/mat_stud/MIXED/archive/2019/Optional_notes/Chap_3_4_Comparators.pdf](http://www2.ing.unipi.it/~a008309/mat_stud/MIXED/archive/2019/Optional_notes/Chap_3_4_Comparators.pdf)

*TODO* &#128197;



## Kickback Noise

kick-back increases CDAC settling time

> *add pre-amp (more power)*
>
> Kickback noise trades with the *dimensions of the input transistors* and hence with the *offset voltage*

*TODO* &#128197;

-  affects the comparator's own decision
-  corrupts the input voltage while it is sensed by other circuits





> Figueiredo, Pedro & Vital, João. (2006). Kickback noise reduction techniques for CMOS latched comparators. Circuits and Systems II: Express Briefs, IEEE Transactions on. 53. 541 - 545. 10.1109/TCSII.2006.875308. [[https://sci-hub.se/10.1109/TCSII.2006.875308](https://sci-hub.se/10.1109/TCSII.2006.875308)]
>
> P. M. Figueiredo and J. C. Vital, "Low kickback noise techniques for CMOS latched comparators," 2004 IEEE International Symposium on Circuits and Systems (ISCAS), Vancouver, BC, Canada, 2004, pp. I-537 [[https://sci-hub.se/10.1109/ISCAS.2004.1328250](https://sci-hub.se/10.1109/ISCAS.2004.1328250)]
>
> Lei, Ka Meng & Mak, Pui-In & Martins, R.P.. (2013). Systematic analysis and cancellation of kickback noise in a dynamic latched comparator. Analog Integrated Circuits and Signal Processing. 77. 277-284. 10.1007/s10470-013-0156-1. [[https://rto.um.edu.mo/wp-content/uploads/docs/ruimartins_cv/publications/journalpapers/57.pdf](https://rto.um.edu.mo/wp-content/uploads/docs/ruimartins_cv/publications/journalpapers/57.pdf)]



## Metastability

*TODO* &#128197;

If the comparator can not generate a well-defined logical output in half of the clock period, we say the circuit is "**metastable**"







## Math Background

### Relating $\Phi$ and erf

 **Error Function** (**Erf**) of the standard Normal distribution
$$
\text{Erf}(x) = \frac{2}{\sqrt{\pi}}\int_0^x e^{-t^2} \mathrm{d}t.
$$
 **Cumulative Distribution Function** (**CDF**) of the standard Normal distribution
$$
\Phi(x) = \frac{1}{\sqrt{2\pi}}\int_{-\infty}^x e^{-z^2/2} \mathrm{d}z.
$$


![Figure](comparator/O6mNn.png)

$$\begin{align}
\Phi(x) &= \frac{\text{Erf}(x/\sqrt{2})+1}{2}. \\
\Phi(x\sqrt{2}) &= \frac{\text{Erf}(x) + 1}{2}
\end{align}$$

Considering the mean and standard deviation
$$
\Phi(x,\mu,\sigma)=\frac{1}{2}\left( 1+\text{Erf} \left( \frac{x-\mu}{\sigma\sqrt{2}} \right)\right)
$$

---

![image-20241109135425126](comparator/image-20241109135425126.png)

> John D. Cook. Relating Φ and erf [[https://www.johndcook.com/erf_and_normal_cdf.pdf](https://www.johndcook.com/erf_and_normal_cdf.pdf)]



## reference

Xu, H. (2018). Mixed-Signal Circuit Design Driven by Analysis: ADCs, Comparators, and PLLs. *UCLA*. ProQuest ID: Xu_ucla_0031D_17380. Merritt ID: ark:/13030/m5f52m8x. Retrieved from [[https://escholarship.org/uc/item/88h8b5t3](https://escholarship.org/uc/item/88h8b5t3)]

A. Abidi and H. Xu, "Understanding the Regenerative Comparator Circuit," Proceedings of the IEEE 2014 Custom Integrated Circuits Conference, San Jose, CA, 2014, pp. 1-8. [[https://picture.iczhiku.com/resource/ieee/WHiYwoUjPHwZPXmv.pdf](https://picture.iczhiku.com/resource/ieee/WHiYwoUjPHwZPXmv.pdf)]

T. Sepke, P. Holloway, C. G. Sodini and H. -S. Lee, "Noise Analysis for Comparator-Based Circuits," in IEEE Transactions on Circuits and Systems I: Regular Papers, vol. 56, no. 3, pp. 541-553, March 2009 [[https://dspace.mit.edu/bitstream/handle/1721.1/61660/Speke-2009-Noise%20Analysis%20for%20Comparator-Based%20Circuits.pdf](https://dspace.mit.edu/bitstream/handle/1721.1/61660/Speke-2009-Noise%20Analysis%20for%20Comparator-Based%20Circuits.pdf)]

Sepke, Todd. "Comparator design and analysis for comparator-based switched-capacitor circuits." (2006). [[https://dspace.mit.edu/handle/1721.1/38925](https://dspace.mit.edu/handle/1721.1/38925)]

P. Nuzzo, F. De Bernardinis, P. Terreni and G. Van der Plas, "Noise Analysis of Regenerative Comparators for Reconfigurable ADC Architectures," in *IEEE Transactions on Circuits and Systems I: Regular Papers*, vol. 55, no. 6, pp. 1441-1454, July 2008 [[https://picture.iczhiku.com/resource/eetop/SYirpPPPaAQzsNXn.pdf](https://picture.iczhiku.com/resource/eetop/SYirpPPPaAQzsNXn.pdf)]

J. Kim, B. S. Leibowitz, J. Ren and C. J. Madden, "Simulation and Analysis of Random Decision Errors in Clocked Comparators," in IEEE Transactions on Circuits and Systems I: Regular Papers, vol. 56, no. 8, pp. 1844-1857, Aug. 2009, doi: 10.1109/TCSI.2009.2028449. URL:[https://people.engr.tamu.edu/spalermo/ecen689/simulation_analysis_clocked_comparators_kim_tcas1_2009.pdf](https://people.engr.tamu.edu/spalermo/ecen689/simulation_analysis_clocked_comparators_kim_tcas1_2009.pdf)

Jaeha Kim, Lecture 12. Aperture and Noise Analysis of Clocked Comparators URL:[https://ocw.snu.ac.kr/sites/default/files/NOTE/7038.pdf](https://ocw.snu.ac.kr/sites/default/files/NOTE/7038.pdf)

Rabuske, Taimur & Fernandes, Jorge. (2017), Chapter 5 Noise-Aware Synthesis and Optimization of Voltage Comparators, "Charge-Sharing SAR ADCs for Low-Voltage Low-Power Applications"

Y. Luo, A. Jain, J. Wagner and M. Ortmanns, "Input Referred Comparator Noise in SAR ADCs," in IEEE Transactions on Circuits and Systems II: Express Briefs, vol. 66, no. 5, pp. 718-722, May 2019. [[https://sci-hub.se/10.1109/TCSII.2019.2909429](https://sci-hub.se/10.1109/TCSII.2019.2909429)]

Art Schaldenbrand, Senior Product Manager, Keeping Things Quiet: A New Methodology for Dynamic Comparator Noise Analysis URL:[https://www.cadence.com/content/dam/cadence-www/global/en_US/videos/tools/custom-_ic_analog_rf_design/NoiseAnalyisposting201612Chalk%20Talk.pdf](https://www.cadence.com/content/dam/cadence-www/global/en_US/videos/tools/custom-_ic_analog_rf_design/NoiseAnalyisposting201612Chalk%20Talk.pdf)

X. Tang et al., "An Energy-Efficient Comparator With Dynamic Floating Inverter Amplifier," in IEEE Journal of Solid-State Circuits, vol. 55, no. 4, pp. 1011-1022, April 2020 [[https://sci-hub.se/10.1109/JSSC.2019.2960485](https://sci-hub.se/10.1109/JSSC.2019.2960485)]

Chen, Long & Sanyal, Arindam & Ma, Ji & Xiyuan, Tang & Sun, Nan. (2016). Comparator Common-Mode Variation Effects Analysis and its Application in SAR ADCs. 10.1109/ISCAS.2016.7538972. [[https://labs.engineering.asu.edu/mixedsignals/wp-content/uploads/sites/58/2017/08/ISCAS_comp_long_2016.pdf](https://labs.engineering.asu.edu/mixedsignals/wp-content/uploads/sites/58/2017/08/ISCAS_comp_long_2016.pdf)]

V. Stojanovic, and V. G. Oklobdzija, "Comparative Analysis of Master–Slave Latches and Flip-Flops for High-Performance and Low-Power Systems," IEEE J. Solid-State Circuits, vol. 34, pp. 536–548, April 1999. [[https://www.ece.ucdavis.edu/~vojin/CLASSES/EEC280/Web-page/papers/Clocking/Vlada-Latches-JoSSC-Apr-1999.pdf](https://www.ece.ucdavis.edu/~vojin/CLASSES/EEC280/Web-page/papers/Clocking/Vlada-Latches-JoSSC-Apr-1999.pdf)]

C. Mangelsdorf, "Metastability: Deeply misunderstood [Shop Talk: What You Didn’t Learn in School]," in IEEE Solid-State Circuits Magazine, vol. 16, no. 2, pp. 8-15, Spring 2024

B. Razavi, **"The Design of a Comparator [The Analog Mind],"** IEEE Solid-State Circuits Magazine, Volume. 12, Issue. 4, pp. 8-14, Fall 2020. [https://www.seas.ucla.edu/brweb/papers/Journals/BR_SSCM_4_2020.pdf](https://www.seas.ucla.edu/brweb/papers/Journals/BR_SSCM_4_2020.pdf)

B. Razavi, **"The StrongARM Latch [A Circuit for All Seasons],"** IEEE Solid-State Circuits Magazine, Issue. 2, pp. 12-17, Spring 2015. [https://www.seas.ucla.edu/brweb/papers/Journals/BR_Magzine4.pdf](https://www.seas.ucla.edu/brweb/papers/Journals/BR_Magzine4.pdf)

CHUNG-CHUN (CC) CHEN. Why Transient Noise (Trannoise) Analysis for A Strong-arm Latch / Comparator? [[https://youtu.be/gpQggSM9_PE?si=apMd6yWVO1JHOHm_](https://youtu.be/gpQggSM9_PE?si=apMd6yWVO1JHOHm_)]

CHUNG-CHUN (CC) CHEN. Why A Dedicated Noise Analysis for A Strong-arm Latch / Comparator?  [[https://youtu.be/S5GnvFxuxUA?si=w38iLvzjr0azhu43](https://youtu.be/S5GnvFxuxUA?si=w38iLvzjr0azhu43)]

Rabuske, Taimur & Fernandes, Jorge. (2014). Noise-aware simulation-based sizing and optimization of clocked comparators. Analog Integr. Circuits Signal Process.. 81. 723-728. 10.1007/s10470-014-0428-4. [[https://sci-hub.se/10.1007/s10470-014-0428-4](https://sci-hub.se/10.1007/s10470-014-0428-4)]

Rabuske, Taimur & Fernandes, Jorge. (2016). Charge-Sharing SAR ADCs for Low-Voltage Low-Power Applications. 10.1007/978-3-319-39624-8. 
