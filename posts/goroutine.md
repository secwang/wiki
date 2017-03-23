---
title: "Some details about the goroutine and the interface system."
date: 2013-09-20 9:00
---

[TOC]


协程的特征有

-   能够在单一的系统线程中模拟多个任务的并发执行。
-   在一个特定的时间，只有一个任务在运行，即并非真正地并行。
-   被动的任务调度方式，即任务没有主动抢占时间片的说法。当一个任务正在执行时，外部没有办法中止它。要进行任务切换，只能通过由该任务自身调用`yield()`来主动出让CPU使用权。
-   每个协程都有自己的堆栈和局部变量

实现协程需要四个部分

-   任务及任务管理
-   任务调度器
-   异步IO
-   channel

每一个任务需要保存以下这几个关键数据：

-   任务上下文，用于在切换任务时保持当前任务的运行环境
-   栈
-   状态
-   该任务所对应的业务函数
-   任务的调用参数
-   之前和之后的任务

初始化一个任务需要：

-   创建并设置一个task对象
-   将task添加到alltask任务列表
-   将task设为就绪

整个golang维护一个alltask 任务列表，循环执行任务列表中的任务。任务之间的切换通过contextswitch函数进行实现。

协程中发生任务切换会有以下两种情况

-    主动让出，调用yeild
-    IO堵塞

第一种情况，所发生的事情是

-   将正在执行的任务放回到等待队列中，免得永远无法再切换回来；
-   将该任务的状态设置为`yield`；
-   进行任务切换。

第二种情况，所发生的事情是

-   执行其他状态为yield的程序，执行完之后，对IO状态进行监听
-   如果读写成功，把对应的任务设为可执行
-   执行alltask列表

channel的实现

-   内存缓存，用于存放元素；
-   发送队列；
-   接受队列。

golang的接口系统

> Languages with methods typically fall into one of two camps: prepare tables for all the method calls statically (as in C++ and Java), or do a method lookup at each call (as in Smalltalk and its many imitators, JavaScript and Python included) and add fancy caching to make that call efficient. Go sits halfway between the two: it has method tables but computes them at run time. I don't know whether Go is the first language to use this technique, but it's certainly not a common one. (I'd be interested to hear about earlier examples; leave a comment below.）
>
从机器的角度如何判断一个类型实现了一个接口的所有方法？一个简单的逻辑就是需要获取这个类型的所有方法集合（集合A），并获取该接口包含的所有方法集合（集合B），然后判断列表B是否为列表A的子集，是则意味着某类型实现了某接口。

本质上是为类型维护表，接口查询和接口赋值的本质是维护的表中的字符串匹配。
