
---
title: pymysql.err.OperationalError(2013, 'Lost connection to MySQL server during query')
date: 2019-05-06 12:36:15
tags: 数据库
---


## 问题描述 
   在执行脚本插入操作的时候,  报了一个 mysql 连接断开的错误,  报错信息为    pymysql.err.OperationalError: (2013, 'Lost connection to MySQL server during query'),  原因是同时操作了太大的数据,  比如我就用 cursor.execute(sql) 执行了上千条插入语句,  然后再commit 一次,  这样同时数据量过大,  就会造成mysql连接断开,  但是数据还是会插进入,  不过有可能会丢数据;

## 解决办法
加一个全局变量计数器,  然后在执行语句达到一定数量后再commint 一次,  这个数据可以根据mysql的性能来设置,  我这边设置成100之后就没问题了 (别忘了commit之后把计数器变量清零)

    