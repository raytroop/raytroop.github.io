---
title: What is the proper method to remove old kernels from a Red Hat Enterprise Linux system?
date: 2022-05-01 22:43:32
tags:
- linux
- yum
- rhel
categories:
- devops
---

**Red Hat Enterprise Linux 8**

The YUM version 4 (based on the upstream `DNF` project) method for removing kernels and keeping only the latest version and running kernel:

```bash
$ yum remove --oldinstallonly
```

From the `yum` man page:

```bash
dnf [options] remove --oldinstallonly
    Removes old installonly packages, keeping only latest versions and  version  of  running
    kernel.
```

