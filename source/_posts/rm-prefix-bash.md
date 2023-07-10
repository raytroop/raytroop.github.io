---
title: Remove prefix from multiple files in Linux console
date: 2024-08-18 16:01:18
tags:
categories:
- devops
---


Bash
```
for file in prefix*; do mv "$file" "${file#prefix}"; done;
```
The for loop iterates over all files with the prefix. The do removes from all those files iterated over the prefix.

Here is an example to remove "bla_" form the following files:
```
bla_1.txt
bla_2.txt
bla_3.txt
blub.txt
```
Command
```
for file in bla_*; do mv "$file" "${file#bla_}";done;
```
Result in file system:
```
1.txt
2.txt
3.txt
blub.txt
```



> [[https://gist.github.com/guisehn/5438bbc22138435665c6e996493fe02b](https://gist.github.com/guisehn/5438bbc22138435665c6e996493fe02b)]
