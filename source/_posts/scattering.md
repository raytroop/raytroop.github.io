---
title: Scattering parameters
date: 2023-09-29 15:57:01
tags:
categories:
- dsp
mathjax: true
---


## Voltage scattering


*TODO* &#128197;


## characteristic impedance ($Z_0$)

*TODO* &#128197;





## Voltage Transfer Function

![image-20241030220203806](scattering/image-20241030220203806.png)

![image-20241030220131714](scattering/image-20241030220131714.png)

> ![image-20241030222403947](scattering/image-20241030222403947.png)



### Reflection Coefficients

![image-20241030222906229](scattering/image-20241030222906229.png)

![image-20241030222923491](scattering/image-20241030222923491.png)



## Rational Fitting

*TODO* &#128197;



## Z0 
> Remember, S-parameters **don't mean much** unless you know the value of the **reference impedance **(it's frequently called Z0).



simulator will read sp file's **Z0** parameter



> The default **Z0** exported by EMX is **50**




## reference

[microwaves101, S-parameters (https://www.microwaves101.com/encyclopedias/s-parameters)](https://www.microwaves101.com/encyclopedias/s-parameters)

Pupalaikis, P. (2020). *S-Parameters for Signal Integrity*. Cambridge: Cambridge University Press. doi:10.1017/9781108784863

Coelho, C. P., Phillips, J. R., & Silveira, L. M. (n.d.). Robust rational function approximation algorithm for model generation. Proceedings 1999 Design Automation Conference (Cat. No. 99CH36361). doi:10.1109/dac.1999.781313

Cadence IEEE IMS 2023, Introducing the Spectre S-Parameter Quality Checker and Rational Fit Model Generator [[https://support.cadence.com/apex/ArticleAttachmentPortal?id=a1O3w000009lplhEAA](https://support.cadence.com/apex/ArticleAttachmentPortal?id=a1O3w000009lplhEAA)]

The Complex Art Of Handling S-Parameters: The importance of extraction and fitting to circuit simulation involving S-parameters  [[https://semiengineering.com/the-complex-art-of-handling-s-parameters](https://semiengineering.com/the-complex-art-of-handling-s-parameters/)]

Dr. John Choma. EE 541, Fall 2006: Course Notes #2 Scattering Parameters: Concept, Theory, and Applications [[https://www.ieee.li/pdf/essay/scattering_parameters_concept_theory_applications.pdf](https://www.ieee.li/pdf/essay/scattering_parameters_concept_theory_applications.pdf)]

Dr. Ray Kwok . Network Techniques: Conversion between Filter Transfer Function and Filter Scattering (SMatrix) Parameters [[https://www.sjsu.edu/people/raymond.kwok/docs/project172/FTF%20to%20S-Matrix%20Spring%202011.pdf](https://www.sjsu.edu/people/raymond.kwok/docs/project172/FTF%20to%20S-Matrix%20Spring%202011.pdf)]
