---
title: Model Library Setup 
date: 2023-01-14 21:59:30
tags:
- virtuoso
categories:
- cad
---

In order to set up model files automatically in the *Model Library Setup* form for Spectre or AMS simulator in ADE Explorer or ADE Assembler

Add the following line in your  `.cdsinit`

```skill
envSetVal( "spectre.envOpts" "modelFiles" 'string "<path_to model_file>/myModels.scs")
```

or

```
envSetVal("spectre.envOpts" "modelFiles" 'string "moreModels;ff mymodels;tt")
```



![image-20230114220458438](ModelLibrarySetup/image-20230114220458438.png)
