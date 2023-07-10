---
title: Network Analysis
date: 2023-09-29 15:57:01
tags:
categories:
- dsp
mathjax: true
---



![image-20240704212740246](network/image-20240704212740246.png)





## Rational Fit



### Matlab/rationalfit

To resolve the convergence problem of s-parameter in Spectre simulator - `rationalfit` and write Verilog-A 

![image-20220630224525565](network/image-20220630224525565.png)

```matlab
filename  = 'touchstone/ISI.S4P';
s4p = read(rfdata.data, filename);
sdd_params = s2sdd(s2p.S_Parameters, 2);
sdd21 = squeeze(sdd_params(2, 1, :));   % s21
freq = s4p.Freq;

% rational fitting
weight = ones(size(sdd21));
weight(floor(end*3/4):end) = 0.2;
weight(2:10) = 0;

[hfit, errb] = rationalfit(freq, sdd21, 'IterationLimit', [4, 16], 'Delayfactor', 0.98, ...
    'Weight', weight, 'Tolerance', -38, 'NPoles', 32);
[sdd21_fit, ff] = freqresp(hfit, freq);

figure(1)
plot(freq/1e9, db(sdd21), 'b-'); hold on;
plot(ff/1e9, db(sdd21_fit), 'r-'); hold off; grid on;
legend('sdd21', 'sdd21\_fit');
xlabel('Freq (GHz)');
ylabel('magnitude (dB)');


ts = 1e-12;
n = 2^18;
trise = 4e-14;
[yout, tout] = stepresp(hfit, ts, n, trise);
figure(2)
plot(tout*1e12, yout, 'b-'); grid on;
xlabel('Time (ps)');
ylabel('V');
title('Step Response');


% write verilog-A
writeva(hfit, 'channel_32poles.va');
```



## Z0 
> Remember, S-parameters **don't mean much** unless you know the value of the **reference impedance **(it's frequently called Z0).



simulator will read sp file's **Z0** parameter

![image-20220430214052538](network/image-20220430214052538.png)

![image-20220430214136970](network/image-20220430214136970.png)

![image-20220430214419283](network/image-20220430214419283.png)

> The default **Z0** exported by EMX is **50**



## reference

[microwaves101, S-parameters (https://www.microwaves101.com/encyclopedias/s-parameters)](https://www.microwaves101.com/encyclopedias/s-parameters)

Pupalaikis, P. (2020). *S-Parameters for Signal Integrity*. Cambridge: Cambridge University Press. doi:10.1017/9781108784863

Coelho, C. P., Phillips, J. R., & Silveira, L. M. (n.d.). Robust rational function approximation algorithm for model generation. Proceedings 1999 Design Automation Conference (Cat. No. 99CH36361). doi:10.1109/dac.1999.781313

Cadence IEEE IMS 2023, Introducing the Spectre S-Parameter Quality Checker and Rational Fit Model Generator [[https://support.cadence.com/apex/ArticleAttachmentPortal?id=a1O3w000009lplhEAA](https://support.cadence.com/apex/ArticleAttachmentPortal?id=a1O3w000009lplhEAA)]

The Complex Art Of Handling S-Parameters: The importance of extraction and fitting to circuit simulation involving S-parameters  [[https://semiengineering.com/the-complex-art-of-handling-s-parameters](https://semiengineering.com/the-complex-art-of-handling-s-parameters/)]
