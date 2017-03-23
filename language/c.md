---
title: "c and assembly language"
date: 2016-12-07 08:00
---
[TOC]

# dump  assembly code

```
clang++ -S -mllvm --x86-asm-syntax=intel test.cpp
clang -S -mllvm --x86-asm-syntax=intel test.c
```
