<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [ttl](#ttl)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

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



