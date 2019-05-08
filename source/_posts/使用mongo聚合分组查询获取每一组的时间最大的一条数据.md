
---
title: 使用mongo聚合分组查询获取每一组的时间最大的一条数据
date: 2019-05-06 12:36:15
tags: 数据库
---


### mongo聚合
使用mongo的.aggregate方法, 类似一个聚合流水线的一个过程, 可以理解为文档经过多次管道阶段最后生成的结果, 可以直接看[mongo aggregate官方文档](https://docs.mongodb.com/manual/aggregation/) 的一张图![管道](https://docs.mongodb.com/manual/_images/aggregation-pipeline.bakedsvg.svg)
将整体文档经过多次管道最后生成想要的文档这个原理

官方也提供了很多 [聚合管道运算符](https://docs.mongodb.com/manual/reference/operator/aggregation/), 用到的朋友可以直接查询

讲一下我自己解决问题写的一条语句
```
db.getCollection('city').aggregate([
    {"$match": {"date": {"$lte":20190313}}}, 
    {"$sort": {"date": -1}},
    {"$group": {_id: "$city_id",     
        firstDate: { $first: "$$ROOT" }}
    }]
)
```
简单解释一下, 就是我需要求出按城市id聚合分组求日期小于 20190313的组内数据并按照日期进行倒序求第一条的所有数据, 过程就是
```
    1 先找出日期小于 20190313的所有文档;
    2 按照日期倒序进行排序
    3 按照city_id进行聚合并求出第一个文档的所有内容, 内容会放入 firstDate 里面
```


    