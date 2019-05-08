
---
title: mysql普通索引和联合索引测试
date: 2019-05-06 12:36:15
tags: 数据库
---


## 索引就用空间来换取时间
#### explain学习和参数代表的意思请参考  https://blog.csdn.net/ywdhzxf/article/details/84316712
下面我会用explain 来测试联合索引和普通索引的作用项, 只测两个字段, source和name
有兴趣的可以看下我下面的测试, 并不繁琐, 没兴趣的直接看结论吧

1  联合索引的第一个字段可以当普通索引来用(没有普通索引快, 但确实可以提高查询效率, 可以看下面只有联合索引的测试结果), 即比如我的联合索引是name+source, 那么我只拿name当where当条件也会命中索引, 但是用source就不会了, 查询全部的数据;

2  如果只是两个字段联合查询的话, 两个字段单个查询的次数也比较高, 那么就不如直接建立两个普通索引了(我的测试用的都是等于, 如果有其他条件的命中rows较多的话还是建议联合索引, 毕竟联合索引的type优先级较高);

3  如果几个字段经常联合查询的话, 很有必要建一个联合索引, 但可以把某个单个查询应用较高的字段放在第一位, 这样也比较省索引了;

4  相同rows的情况下, type的优先级越高(type的优先级查看explain学习那篇), 查的越快;

做的简单测试, 如果不对请大神评论指导, 谢谢.


###	联合索引(name+source), 普通索引(source, name)
	select * from db where source=1 and name=1
	explain 测试:
		三个索引全部命中
		type     ref
		rows     21行

	select * from db where name=1
	eplain 测试:
		命中两个索引
		type     ref
		rows     30行


### 联合索引(name+source)
	select * from db where source=1 and name=1
	explain 测试:
		联合索引命中
		type     ref
		rows     21行

	select * from db where name=1
	eplain 测试:
		命中索引
		type     ref
		rows     30行

	select * from db where source=1
	explain 测试:
		没有命中索引
		type     all
		rows     10W+(所有的数据)


### 普通索引(source, name)
	select * from db where source=1 and name=1
	explain 测试:
		命中两个索引
		type     index_merge
		rows     2

	select * from db where name=1
	eplain 测试:
		命中索引
		type     ref
		rows     30

	



    