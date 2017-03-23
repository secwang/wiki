<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [dump  assembly code](#dump--assembly-code)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

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
