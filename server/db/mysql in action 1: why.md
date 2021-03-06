# 为什么程序员要精通mysql

这系列文章主要想和大家分享一下我作为一个普通程序员对mysql的认识。目标读者主要是对mysql不是很精通，但每天都在和mysql打交道的程序员们。

这个系列大概会讲解以下几个topic：

- 为什么做业务开发的程序员需要精通数据库
- mysql有哪些锁，在各种crud的场景中会加哪些锁
- mysql join命令是如何实现的，为什么DBA们总说不要用join
- mysql order by、limit、group等命令是如何实现的

根据我的个人经验，做业务开发的同学基本对数据库设计范式、索引的原理和最佳实践、锁的类型、事务等概念有比较清晰的认识。但如果稍微深入一下，比如说对某表执行一条select语句时会加哪些锁，大部分同学都是靠猜测给出自己的答案，并不清楚真实的情况。这样的话写出来的sql在并发比较高的情况下，很容易产生性能问题。

这系列的文章主要就是针对这些稍微深入一些的问题，讲解数据库的实现。希望通过这几篇文章的学习，能让大家对mysql的工作原理产生一些兴趣，帮助大家打开一扇新的知识大门，最终能够把这些知识应用到工作中，这样我写这些文章的目的就达到了。

话不多说，我们开始第一篇的分享：普通业务程序员为什么要精通数据库？

## 分享一些项目中遇到的数据库引发的案子

### 某次深夜发布，频繁出现系统启动后几十秒就失去响应

某个用户登陆相关的表，自动化发布时，建索引失败。

### 好好的系统，各方面流量和往常都一样，突然down机

某个导出数据的任务，调用了一条200多行的sproc

### 错误的where条件导致索引失效，进而导致接口服务失去响应

find_in_set是全表扫描

### 一条简单的insert语句，频繁报锁等待timeout

insert into ... select

### 没有任何慢查询，但数据库cpu一直100%，导致服务失去响应

应用没有做缓存

## 数据库是大部分性能问题的根因

- 数据库有状态，不好扩展
- 数据库处于应用底层，调用频繁，出错时影响范围广

## 性能优化要遵循阿姆达尔定律

## 总结
