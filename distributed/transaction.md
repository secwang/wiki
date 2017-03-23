---
title: "distributed transaction"
date: 2016-07-11 10:00
---
[TOC]

### 分布式事务实现对比问题
#### 问题
上面一份文档中，我们限于 mysql 和业务场景对分布式事务更多采取绕过去的做法，但是现在随着时间发展，实际上，有一部分数据库已经号称解决了分布式事务的问题。我们可能并不会选择这些解决办法，对这些数据库解决办法的调研应该可以加深我们对这个问题的理解。

分布式事务很难解决的问题在于，2pc 默认是要引入外部协调者的，在需要跨节点的情况下，引入外部协调者的成本过大。

于是问题可以更新描述为，如何在不引入外部协调者的情况下，完成多节点两段式提交。

##### oceanbase

基于 oceanbase 早期版本 0.4,0.5 , 1.0 号称完成了多点写入的功能，但在网上找不到更多的资料。

下文中以 oceanbase 来代指 oceanbase 的早期版本。


服务架构介绍

RootServer,UpdateServer,ChunkServer,MergeServer。

看上去复杂，其实我们可以用简单的几句话勾勒出 oceanbase 的架构。

oceanbase 和 mysql 在我看来基本上是没有什么关系的，本质上是个 sql over nosql 的数据库系统。底层使用 nosql 做存储，支持 sql 语法。

在描述之前我们需要引入几个概念。
sstable sstable 可以理解成固定的kv对。
memtable memtable 可以理解成可以改变的kv对
tablet 实际上是指子表.

oceanbase 实际上是以单点写入，规避了跨节点事务。


事务实现



##### cockroachdb

##### tidb

##### lealone

##### 总结

---
reference:
1. http://xblk.ecnu.edu.cn/CN/article/downloadArticleFile.do?attachType=PDF&id=25015
