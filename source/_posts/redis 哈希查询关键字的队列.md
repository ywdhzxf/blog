
---
title: redis 哈希查询关键字的队列
date: 2019-05-06 12:36:15
tags: 数据库
---


# redis 在哈希里面查询带关键字的小key  hscan

## 问题
   比如说我现在有一个哈希队列, 做的是  用户id+行为编号: 时间 的一个缓存(随意举得例子,不要介意), 现在有一个用户注销了, 我现在需要把这个用户的所有信息缓存全部干掉, 你要怎么做? 获去该哈希队列所有的key然后再匹配? 太捞了, redis 提供了一种匹配机制, 类似 keys * 这种规则的匹配模式


## 解决

比如我现在有一个这样的哈希队列
![创建哈希队列](https://img-blog.csdnimg.cn/20181225182603440.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3l3ZGh6eGY=,size_16,color_FFFFFF,t_70)
	然后我现在想删除用户id 为617的所有信息, 调用命令
![模糊查询出来需要删除的小key](https://img-blog.csdnimg.cn/20181225182625211.png)
	这样就好了, 然后再把小key 用hdel命令批量干掉就可以了, 是不是很简单方便
## 他其实还有很多用法:
	SCAN 命令用于迭代当前数据库中的数据库键。
	SSCAN 命令用于迭代集合键中的元素。
	HSCAN 命令用于迭代哈希键中的键值对。
	ZSCAN 命令用于迭代有序集合中的元素（包括元素成员和元素分值）。
	具体用法可以参考  http://redisdoc.com/key/scan.html#scan


    