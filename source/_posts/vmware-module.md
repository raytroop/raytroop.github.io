---
title: Build VMware host modules
date: 2024-01-30 22:06:27
tags:
categories:
- devops
---



```
git clone git@github.com:mkubecek/vmware-host-modules.git
cd vmware-host-modules/
git checkout origin/workstation-17.0.2
make -j`nproc`
sudo make install
sudo modprobe -v vmmon
sudo modprobe -v vmnet
sudo vmware-networks --start
```

