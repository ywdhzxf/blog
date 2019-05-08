
---
title: mongo中'dict' object has no attribute '_txn_read_preference'和 Sort exceeded memory limit
date: 2019-05-06 12:36:15
tags: 数据库,Python
---


## 前言
  今天遇到了mongo 的一条语句两个问题, 在这里分享一下留个记录
## 问题一
```
Sort exceeded memory limit of 104857600 bytes, but did not opt in to external sorting. Aborting operation. Pass allowDiskUse:true to opt in.
```
这个问题是我使用mongo的aggregate聚合语句时出现的, 意思就是说排序超过了100M的限制, 没有进行外部缓存, 需要添加allowDiskUse 这个参数, 来做一个磁盘缓存, 我的语句
```
db.getCollection('price').aggregate([
                        {"$match": {"date": {"$lte": 20190326}}},
                        {"$sort": {"date": -1}},                                                 
                        {"$group": {"_id": "$city", "dat": {"$first": "$$ROOT"}}}
                        ], 
                        {"allowDiskUse": true}
                        )
```
这样就ok了

## 问题二
因为上面在mongo可视化工具里面执行成功了, 所以我就放到程序中, 然后报了一个错
```
{AttributeError}'dict' object has no attribute '_txn_read_preference'
```
这就比较懵了,  解决办法就是把  {"allowDiskUse": true} 换成 allowDiskUse=true 就可以了, 但是一般来说mongo的后续参数在可视化工具里面也可以这样写, 比如 multi=True之类的, 这个就不行, 可能是因为参数使用范围的问题吧..

    