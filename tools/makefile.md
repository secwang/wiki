---
title: "makefile"
date: 2016-06-30 23:00
---
[TOC]

# usage
```
$@ 在指令被运行时，被宏替换为目标。
$^ 被宏替换为所有的依赖目标。
$< ，可以替换所依赖的第一个目标。
%.obj  在 make 里指代为 *.obj。
```
# phony
what is phony?

# sample

```
DOT=$(wildcard *.dot)
DOTPNG=$(DOT:.dot=.png)

all: dot

dot: $(DOTPNG)

%.png : %.dot	
	dot -Tpng $< > $@

.PHONY: dot

clean :
	rm *.png 

```
