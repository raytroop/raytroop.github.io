---
title: Script to remove .cdslck files
date: 2022-02-02 16:50:56
tags:
- shell
categories:
- cad
---

```sh
 #!/bin/sh 
tree -if | grep 'cdslck' > txt 
var=`cat txt`
for i in $var; do
	rm -i $i
done
rm -i txt
```

<https://wikis.ece.iastate.edu/vlsi/index.php/Tips_%26_Tricks#Locked_Files_in_Cadence>

