---
title: How to squash all git commits into one?
date: 2023-08-10 23:47:23
tags:
categories:
- devops
---

[https://stackoverflow.com/a/9254257/8037585](https://stackoverflow.com/a/9254257/8037585)

As of [git 1.6.2](https://github.com/git/git/blob/master/Documentation/RelNotes/1.6.2.txt#L118), you can use `git rebase --root -i`

For each commit except the first, change `pick` to `squash`.



this works find, but I had to do a forced push. be careful! `git push -f`
