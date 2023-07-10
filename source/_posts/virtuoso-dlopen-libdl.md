---
title: virtuoso "dlopen failed to open 'libdl.so'"
date: 2022-09-24 00:21:47
tags:
- virtuoso
categories:
- cad
---

```bash
$ sudo yum install glibc-devel  
```

```
Last metadata expiration check: 0:01:02 ago on Sat 24 Sep 2022 12:13:54 AM CST.                                                         
Dependencies resolved.
=========================================================================================================================================
 Package                            Architecture              Version                                    Repository                 Size
=========================================================================================================================================
Installing:
 glibc-devel                        x86_64                    2.28-189.5.el8_6                           baseos                     78 k
Installing dependencies:
 glibc-headers                      x86_64                    2.28-189.5.el8_6                           baseos                    482 k
 kernel-headers                     x86_64                    4.18.0-372.26.1.el8_6                      baseos                    9.4 M
 libxcrypt-devel                    x86_64                    4.1.1-6.el8                                baseos                     24 k

Transaction Summary
=========================================================================================================================================
Install  4 Packages
```

