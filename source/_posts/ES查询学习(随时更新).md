
---
title: ES查询学习(随时更新)
date: 2019-05-06 12:36:15
tags: 数据库
---


## ES查询学习

#### 常用查询
    match_all       查询所有
	match    	分词匹配查询, 模糊查询
	term     	精确查找, 单个字段等值匹配
	terms		多个字段等值匹配

#### 基础查询
	{
		"query": {"match": {}}     			        # 编写查询条件
		"size": 1				   		# 返回数量, 默认为10
		"from": 10					        # 索引下标, 从第几条开始, 默认为0
		"sort": {"length": {"order": "desc"}}		        # 按length进行降序排序
		"_source": ["id", "length"] 				# 返回多个字段
	}

#### 布尔查询
	{
		"query": {
			"bool": {
				"must": [
					{"term": {'id': 110}},    	    ### must == and  必须两个都为真才会返回
					{"term": {'id': 111}}
				],
				"should": [
					{"match":  {'borough': "黑龙国际"}}, ### should == or  两个有一个为真才会返回
					{"match":  {'borough': "天下国际"}}
				],
				"must_not": [
					{"match": {'name': "国美花园"}},     ### must_not == not 全部为假才会返回
					{"match": {'name': "天坛公园"}},
				]
			}
		}
	}
	gt  大于		gte  大于等于		lt  小于		lte  小于等于


#### 过滤查询(filter过滤条件)
	{
		"query": {
			"bool": {
				"must": {"match_all": {}}, 
				"filter": {
					"range": {
						"price": {
							"gte": 1000,     ### 查询price字段在1000到2000之内的所有数据
							"lte": 2000 
						}
					}
				}
			}
		}
	}
	相当于  select * from complex where 1000 <= price and price <= 2000

#### 聚合查询(Aggregations)
	{
		"aggs": {
			"group_by_state": {
				"terms": {
					"field": "borough_name"   ### 所有数据按照小区名进行分组, 然后按照分组记录数从大到小排序
				}
			}
		},
		"size": 0   	### 只返回聚合结果
	}
	相当于  select borough_name, count(*) from complex group by borough_name order by count(*) desc

##### 聚合查询里面执行求平均操作
	{
		"aggs": {
			"group_by_state": {
				"terms": {
					"field": "borough_name"   ### 所有数据按照小区名进行分组, 然后按照分组记录数从大到小排序
				}
			},
			"aggs": {
				"average_balance": {
					"avg": {
						"field": "price"
					}
				}
			}
		},
		"size": 0   	### 只返回聚合结果
	}
	select borough_name, avg(price) ,count(*) from complex group by borough_name order by count(*) desc

    