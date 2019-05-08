
---
title: python 操作ES
date: 2019-05-06 12:36:15
tags: 数据库
---



## python 操作es 的基操

### 配置部分
```
    """
    @author xiaofei
    @email 
    @auth
    @desc 
    """
    import pymongo, json
    from elasticsearch import Elasticsearch
    from elasticsearch import helpers
    import math

    # mapping 定义你的es字段
    doc_mapping = {
        'properties': {
            "other_id": {"type": "long"},
            "city": {"type": "keyword"},
            "id": {"type": "keyword"},
        }
     }

    # 创建ES连接
    es_conn_test = Elasticsearch(["127.0.0.1:6666"], maxsize=25)

    # es的基础配置,  index_name, alias(别名可以创建多个), doc_type(表名)
    index_name = f'complex_test'
    online_alias = f'online_complex_test'
    type_name = f'complex_city'
```

### es的基操
```
    # es 创建库
    es_conn_test.indices.create(index=index_name, ignore=400)
    es_conn_test.indices.put_mapping(index=index_name, doc_type=type_name, body=doc_mapping)
    es_conn_test.indices.put_alias(index_name, online_alias)

    # 获取mapping
    res = es_conn_test.indices.get_mapping(index=index_name)
    print(json.dumps(res))

    # es查询
    res = es_conn_test.search(index=index_name, doc_type=type_name, body={})
    print(json.dumps(res))

    # 删除索引
    res = es_conn_test.indices.delete(index=index_name)
    print(res)
```


### mongo 数据批量插入es(注意, 如果需要插入的数据量太多的话要分批插入, 比如1000条一次, 根据性能自己调整)
```
    # 连接mongo
    mongo_spider = pymongo.MongoClient(host='')
    cli = mongo_spider.test.test_test
    # 统计mongo里面的数量, 计算分页
    nums = cli.count()
    print(nums)
    pages = math.ceil(nums/1000)
    print(pages)

    for page in range(pages):
        ls = page *1000
        # mongo分页查询
        datas = list(cli.find({}).limit(1000).skip(ls))
        data = []
        for x in datas:
            # 判断数据完整
            res = {}
            for k, v in doc_mapping['properties'].items():
                if k == 'id':
                    res['id'] = x['key']
                elif not x.get(k, ''):
                    if v['type'] in ['keyword', 'text']:
                        res[k] = ''
                    elif v['type'] == 'long':
                        res[k] = 0
                    elif v['type'] == 'float':
                        res[k] = 0.0
                else:
                    res[k] = x[k]

            # 下面注释这行是单条插入
            # es_conn_test.create(index=index_name, doc_type=type_name, id=1, body=x)
            action = {"_index": index_name, "_type": type_name, "_source": res, "_id": res['id']}
            print(action)
            data.append(action)
        helpers.bulk(es_conn_test, data)
        print(f'插入{ls}条')


    mongo_spider.close()
```

### es数据批量更新 (注意, 如果需要更新的数据量太多的话要分批更新, 比如1000条一次, 根据性能自己调整)
```
    for x in data:
        id = x['id']
        time_score = x['time_score']
        price_score = x['price_score']
        doc = {"time_score": time_score, "price_score": price_score}
        datas = {"_index": f"online_complex_test", "_op_type": "update", "_type": f"complex_city", "_id": id, 'doc': doc}
        print(datas)
        result.append(datas)

    helpers.bulk(es_conn, result)
    print('更新成功')
```

    