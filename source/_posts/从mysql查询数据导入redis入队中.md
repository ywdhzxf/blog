
---
title: 从mysql查询数据导入redis入队中
date: 2019-05-06 12:36:15
tags: 数据库
---


俩篇对mysql和redis用法解释很详细的博客:
	mysql:
		http://www.jb51.net/article/117330.htm
	redis:
		https://www.cnblogs.com/xuchunlin/p/7067154.html

	
	import pymysql
	建立mysql连接,ip、端口、用户名、密码(passwd,不能写成其他，例如：pwd或者p，否则报错)、库名
	
	conn = pymysql.connect(host='127.0.0.1', user='root', passwd='123456', db='szz', port=3306, charset='utf8')
	#创建游标
	cur = conn.cursor(cursor=pymysql.cursors.DictCursor) 
	#指定cursor的类型为字典，返回结果类型是字典，不再是元组
	#执行sql，返回值是int，查询出来的结果有几条
	cur.execute(''select source_id,pic_url from pic_%s.pic WHERE  source_id=%s'')
	#获取全部数据
	row_1 = cur.fetchall()
	#游标移到起始位置
	cur_complex_r.scroll(0)

	for x in row_1:
	    ##存入redis队列
	    redisdb.lpush(reids_dui,x)
	    redisdb.lpush(reids_dui_tmp,x)

###反向插入也简单
	import redis
	db = 0
	#连接redis,password不简写(否则或报错)，db若不写，则默认操作db0
	conn_redis = redis.Redis(host='127.0.0.1', port=6379, password='123456', db=db)
	sql = "update pic_'%s'.pic set finpic_url='%s' where pic_url='%s';
	#获取队列中所有的值
	zhi_1 = conn_redis.lrange(redis_dui_tmp,0,-1)
	for x in zhi_1:
	    db = mysql.get('db', '')
	    ct = re.search(r'_(\s+)', db).group()
	    cur_complex_w.execute( sql % (a,b,c))
    