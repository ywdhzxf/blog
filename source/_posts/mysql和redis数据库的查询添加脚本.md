
---
title: mysql和redis数据库的查询添加脚本
date: 2019-05-06 12:36:15
tags: 数据库
---


### 从mysql查询数据导入redis

```
select_sql = "select A.source_id,A.pic_url,A.id from newhouse_%s.complex_pic as A LEFT JOIN newhouse_%s.complex as B ON A.complex_id=B.complex_id WHERE  A.source_id=%s AND B.weight >= 50;"

def mysql_select(city, source_id):
    #从sql查询数据
    cur_complex_r.execute(select_sql % (city, city, source_id))
    #获取全部数据
    row_1 = cur_complex_r.fetchall()
    #获取表名+sourceID 作为队列名
    source_name = SOURCES_DICT[source_id]
    reids_dui = "%s_%s" % (source_name, city)
    reids_dui_tmp = "%s_%s_tmp" % (source_name, city)
    redisdb.delete(reids_dui)
    redisdb.delete(reids_dui_tmp)
    for x in row_1:
        ##存入redis队列
        data = {'id': x.get('id', 0), 'pic_url': x.get('pic_url', '')}
        print reids_dui, x.get('pic_url', '')
        redisdb.lpush(reids_dui, x.get('pic_url', ''))
        redisdb.lpush(reids_dui_tmp, json.dumps(data))

```

### 用redis的数据来更新mysql数据

```
update_sql = "update newhouse_%s.complex_pic set noer_pic_url='%s' where id=%s;"

#---------------------------------------从redis数据更新mysql
def mysql_update(city):
    #获取城市信息
    #获取该城市所有的队列名
    redis_names = redisdb.keys("*_%s_update" % city)
    for redis_name in redis_names:
        #获取队列中所有的值
        i = 0
        while redisdb.llen(redis_name):
            x = redisdb.lpop(redis_name)
            if x:
                x = json.loads(x)
                nopic = x['nofinger_pic_url']
                pic_id = x['id']
                i += 1
                print i, update_sql % (city, nopic, pic_id)
                cur_complex_w.execute(update_sql % (city, nopic, pic_id))
            if i % 100 == 0:
                conn_complex_w.commit()
        else:
            conn_complex_w.commit()
            break


```
    