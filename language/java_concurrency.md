---
title: "java concurrency"
date: 2016-06-30 08:00
---
[TOC]


###java  concurrency 
#### java thread join
wait java thread end.
#### manage java lifecycle
start()
involuntarily
close threads is very expensive.

#### overview of thread pool
thread pool patten
call center like a queue


## executorSerivice
executorServer implement execute

runnable
one way task not return a result
callable
two way task return a result.
run asysc task
future
represent the result of an asynchronous task
can be canceled and tested to see if task is done

java8 provide multi core future.

scheduledExecutorService

completionService.
executor and a blocking queue




java support serval types of atomic actoins onvariables

atomic operations
volatile variables
atomic variables

monitor object
two synchronization
mutual exclusion
coordination


---
synchrionization lock.?

ReentratLock 
ReentrantReadWriteLock
StampedLock
Semaphore
ConditionObject
CyclicBarrier
Phaser

---
park(),unpark,compareAndSwap ae in native java.
---

Common lock idiom
1. store lock data member in a local final variable
2. tryp finally block
unlock in the finally part.


---
lock free and thread safe.

atomic is visible to all thread.

aotmic is implement hardware. compare and swap.

---
extensively 

java.util.concurrent.locks



----

volatile  

store in main mermory instead in cache

implment double check pattern

volatile can be inconsist.

volatilse only work in java code.

---
monotir object.

---





question ?

atomic diffe vs volatile?


