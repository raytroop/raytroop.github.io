---
title: Rocky Linux 8 rpm for cadence binary and cdnshelp
date: 2022-02-02 15:15:19
tags:
categories:
- devops
---

**qt5 and openssl**

```bash
sudo yum install openssl compat-openssl10 qca-qt5-ossl.x86_64 openssl-devel
```

**library preparation for EDA installation**

```
libc6, gdb
dc
libncurses5-dev
libncurses5-dev:i386
g++
pstack
libelf1:i386
libgcc-4.8-dev:i386
libstdc++6:i386
gcc-multilib
g++-multilib
libc6-dbg
libc6-dbg:i386
libexpat-dev
libexpat-dev:i386libxss-dev
libxpm4
libxpm4:i386
libmng2
libxss-dev:i386
libxft2
libxft2:i386
libxmu6
libxmu6:i386
libjpeg62-dev
libjpeg62-dev:i386
gnome-core
gnome-core:i386
xfce4
libxml2:i386
libxml2, libXft-dev
libXft-dev:i386
libSM
libSM:i386
libpng3
libpng3:i386
libxi6
libxi6:i386
glibc.i686
libX11.i686
libX11-devel.i686
libX11-devel.x86_64
gcc-c++
compat-readline5
libXext.i686
libXtst.i686
redhat-lsb.i686
libXrender.i686
glibc-devel.i686
zlib.i686
ncompress.x86_64
ksh
openmotif22.i686
openmotif22.x86_64
xterm
```

