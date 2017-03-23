<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [arch](#arch)
- [systemTap session](#systemtap-session)
- [format](#format)
  - [quick add](#quick-add)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

---
title: "systemtap"
date: 2016-06-30 23:00
---
[TOC]

## arch 
The essential idea behid a SystemTap script to name evets, and to give them handlers.When SystemTap runs the script, SystemTap monitors for the event; once the evnet occurs, the Linux kernel then runs the handler as a qucik sub-routine, then resumes;

## systemTap session 

1. First, SystemTap checks the script against the existing tapset library (normally in /usr/share/systemtap/tapset/ for any tapsets used. SystemTap will then substitute any located tapsets with their corresponding definitions in the tapset library.
2. SystemTap then translates the script to C, running the system C compiler to create a kernel module from it. The tools that perform this step are contained in the systemtap package (refer to Section 2.1.1, “Installing SystemTap” for more information).
3. SystemTap loads the module, then enables all the probes (events and handlers) in the script. The staprun in the systemtap-runtime package (refer to Section 2.1.1, “Installing SystemTap” for more information) provides this functionality.
4. As the events occur, their corresponding handlers are executed.
5. Once the SystemTap session is terminated, the probes are disabled, and the kernel module is unloaded.


## format 

```
probe event {statements}
function function_name(arguments) {statements} 
probe event {function_name(arguments)}
```


### quick add

To add value to a statistical aggregate, use the operator <<< value.

```
global reads 
probe vfs.read {
    reads[execname()] <<< count
}
```
