---
title: redis基础篇
date: 2022-06-29 16:12:54
tags:
- redis
categories:
- 数据库
---
redis中文文档：[请戳此](https://www.redis.net.cn/tutorial/3502.html)
## NoSql 简介
### 什么是关系型数据库
依赖关系模型而创建的数据库就是关系型数据库。关系模型就是 一对一，一对多，多对多这些模型。
### 关系型数据库遵循 ACIP原则
 1. A (Atomicity) 原子性:原子不可再分。在一次事务操作中，所有的操作要么全部成功，要么全部失败。
 2. C (Consistency) 一致性:事务的运行不会改变数据库原有的一致性约束。在一次购物操作前后，a+b 的账户余额是不变的。
 3. I (Isolation) 独立性:一个事务的操作不会影响到另一个事务的执行。
 4. D (Durability) 持久性:事务操作一旦提交，就永远保存在数据库中。
## Redis 简介
### 什么是Redis?
Redis 是目前运用较广的一款关系型数据库，遵守BSD协议，是一个高性能的key-value数据库。
redis 的特点有：
 1. 不仅仅支持key-value 数据格式，还支持 list，set，zset，hash 等数据结构
 2. 支持数据的持久化，可以把内存中的数据保存在磁盘中。重启后可以继续使用。
 3. 支持数据备份。
