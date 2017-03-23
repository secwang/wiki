---
title: "java bytecode"
date: 2016-11-19 08:00
---
[TOC]


# Resources
- jvm bytecode http://cory.li/bytecode-hacking/
- jvm http://docs.oracle.com/javase/specs/jvms/se7/html/jvms-3.html 


# workflow to exec java byte code

shoulde install https://wiki.openjdk.java.net/display/CodeTools/asmtools,we don't need bitescript anymore.

java -jar asmtools.jar jasm [options] filename.jasm
java -jar asmtools.jar jdis [options] filename.class

compare with jasmtools.
javap -c some time may get more clear result.


# java Use of Constants, Local Variables, and Control Constructs 





