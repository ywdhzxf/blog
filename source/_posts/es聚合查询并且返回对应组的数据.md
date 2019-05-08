
---
title: es聚合查询并且返回对应组的数据
date: 2019-05-06 12:36:15
tags: 数据库
---


# es 聚合查询并返回每个组的数据
## 需求
   我现在是有一个这样的需求, 我需要在es里面按照 cityarea 进行分组(group by), 并且每个 cityarea的组 需要展示 按照时间排序的前10条, 状态全部为1的数据
## 实现
```
  {
    "query": {
      "bool": {
        "must": [
          {
            "term": {
              "status": "1"         # 筛选条件, 状态为 1 的
            }
          }
        ]
      }
    },
    "from": 0,
    "size": 10,
    "aggs": {
      "top_score": {
        "terms": {
          "field": "cityarea",       ## 按照cityarea 进行分组
          "size": 30                 ## 注意: 这个size 是必填的, 因为不填默认是10, 也就是说如果我有 11个cityarea组的话, 在这只能分10个组, 最后一组不显示,
        },                                   个人建议根据分组情况写一个较大的值
        "aggs": {
          "top_score_hits": {
            "top_hits": {
              "_source": [
                "name"              ## 只展示name字段, 按照自己的需求来就行 
              ],
              "size": 10,           ## 这个size是每个组展示多少条数据, 默认是10
              "sort": {
                "first_time": {
                  "order": "desc"   ## 按照时间进行排序
                }
              }
            }
          }
        }
      }
    }
  }
```

    