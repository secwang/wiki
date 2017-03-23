---
title: "message based transaction"
date: 2016-07-11 10:00
---
[TOC]
###分布式事务调研
#####定义问题
我们更需要的是在不同的数据库实例里使用到事务的语义(估计更多的是交易,其他场景对事务需求并不强)，比分布式事务的语义要小很多。   

#####数据库如何实现事务
- row lock
- version row(根据事务隔离级别)

#### java 如何实现事务
1. close auto-commit in sqlSession
2. if(nested) 不同的orm事务扩散级别  
	2.1. spring deal with nested transaction with one physical transaction and many savepoint.
3. commit or rollback
4. reset SqlSession autoCommit

#### 回顾理论和问题  
- ACID
	  - Atomic 事务成功或者不成功
	  - Consistency 始终保持一致性
	  - Isolation 事务之间，相互隔离
	  - Durability 事务完成，持久化。
- BASE
	  - Basic Available 基本可用
	  - Soft state 状态可以有一段时间不同步
	  - Eventually consistent(最终一致性)
 
#### 两个例子  
- 跨行转账(不追求始终的一致性，追求最终的一致性)
- 余额支付，在支付过程中可能会需要先冻结部分余额(double spending)

#### 重新审视问题
- 追求最终一致性，规避分布式事务

#### 来看可能的方案
##### mysql XA(eXtended Architecture) 
- 介绍
	  - 引入单点决定多部分事务状态
	  - ACID 模型
	  - mysql XA use 2PC
		- 2 pc 事务
- 好处
	  - 强一致性
- 问题
	  - 性能差距10倍 [^1]
	  - 2PC 处理服务失败 
		- 准备后，提交前
	  - mysql 5.7 之下 对 XA 并不完善[^2]
	  - 水平扩展有限制
	  - 业界很难看到在事务型数据库中使用XA
- 结论
	  - 可以考虑绕开分布式事务
	  - 或者想办法减少开销

##### 水平拆分
- 和史腾飞讨论得出
- 介绍
	  - 水平分库
	  － 按水平拆分，确保拆分后始终处于可编辑状态，将分布式事务转化为单机事务
- 优点
	- 用单机事务解决问题
	- 水平扩展不受单点限制
- 缺点
	- 和 SOA 有背离
- 结论
	- 可能还需要讨论
 
##### TCC(try confirm cancel)
- 本质上是 1pc with best effort , 通过事务补偿机制来确保最终一致性，因为是一次提交
效率会提高不少
- 介绍
	- try 完成所有业务的检查（一致性）；预留必须的业务资源（准隔离）
	- confirm 真正的执行操作，只使用Try阶段预留的资源
	- concel 释放Try阶段预留的资源
	- a 先提交 ，b提交或回滚，如果 a 已提交，b 补偿
	- 库存为一的商品，冻结库存，此时用户付款，付款成功，成功，如果付款不成功，回滚库存
 - 优点
	- 相比于 xa 效率高
	- 有使用先例。
  - 缺点
	- 可能会侵入业务
	- 要求确认和取消幂等
##### 基于消息（事务消息和非事务消息，下面暂时以非事务消息为例）
- 本质把分布式事务转化为本地事务，并且确保最终一致性
- 介绍
	- 业务数据和消息数据在一个事务作用域里，业务事务成功，消息事务也随之提交
	- 消息根据写入消息推送及重试
	- 消息接受方接受消息之后，检查消息有效性和消息处理在一个事务作用域里
	- 处理完成后移除消息
	- 本质是处理消息需要幂等
  - 优点
	- 对业务侵入小
	- 支付系统可能需要以是否出金为准而不是系统状态为准，可重试
	- 消息可以携带状态，适应状态机
	- 电商通用方案
	- 性能和水平扩展问题都不大
 - 缺点
	- 需要确保消息可靠性，高可用且一致
	- 需要实现成本

#### 个人偏好
消息，待讨论

#### 可能需要继续关注的问题
- 最终一致性方案在，准同步一致性要求场景的使用 (可以利用回滚，细节还要研究)
- 中间件对嵌套事务的处理方式
- 事务中间 rpc 调用
- 消息处理顺序

####reference

- https://www.percona.com/live/mysql-conference-2013/sites/default/files/slides/XA_final.pdf    
- http://dev.mysql.com/doc/refman/5.6/en/xa.html
- http://hedengcheng.com/?p=136
- http://queue.acm.org/detail.cfm?id=1394128
- http://www.slideshare.net/Fenng/soa-dtp-by-alipay-cheng-li-presentation
