---
title: compile vim from source with GUI support
date: 2022-02-02 16:45:26
tags:
- vim
categories:
- devops
---

```bash
# gtk3 in Rocky Linux 8.5
./configure --with-features=huge --enable-gui=gtk3 --enable-python3interp --prefix=/usr
make -j`nproc`
sudo make install
```

## binkey

Inserting a new line below: `o`

above: `O`

To insert before the cursor: `i`

After: `a`

Before the line (home): `I`

Append at the end of line: `A`
