---
title: "redis"
date: 2016-09-20 23:00
---
[TOC]


# ttl 

When use 'INCR, INCRBY, DECR' update value. They don't modify the TTL.

```
setex test 3600 13

incr test

ttl test
```



