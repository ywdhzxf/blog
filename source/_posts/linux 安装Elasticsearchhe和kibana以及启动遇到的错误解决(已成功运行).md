
---
title: linux 安装Elasticsearchhe和kibana以及启动遇到的错误解决(已成功运行)
date: 2019-05-06 12:36:15
tags: linux,数据库
---


## linux安装es和kibana
参考博文  https://blog.csdn.net/han12398766/article/details/88373869

### 启动报错1
```
Exception elasticsearch.keystore
```
这个错是因为先用root用户启动的es创建的文件, 所以删除就好了


### 启动报错2
```
2019-05-01 19:50:28,655 main ERROR Null object returned for RollingFile in Appenders.
2019-05-01 19:50:28,656 main ERROR Null object returned for RollingFile in Appenders.
2019-05-01 19:50:28,656 main ERROR Null object returned for RollingFile in Appenders.
2019-05-01 19:50:28,656 main ERROR Null object returned for RollingFile in Appenders.
2019-05-01 19:50:28,657 main ERROR Null object returned for RollingFile in Appenders.
2019-05-01 19:50:28,657 main ERROR Null object returned for RollingFile in Appenders.
2019-05-01 19:50:28,658 main ERROR Unable to locate appender "rolling" for logger config "root"
2019-05-01 19:50:28,660 main ERROR Unable to locate appender "index_indexing_slowlog_rolling" for logger config "index.indexing.slowlog.index"
2019-05-01 19:50:28,660 main ERROR Unable to locate appender "audit_rolling" for logger config "org.elasticsearch.xpack.security.audit.logfile.LoggingAuditTrail"
```

需要修改config配置里的log4j2.properties 文件, 将 logger.deprecation.level =  warn 改为 error

### 启动错误3
```
ERROR: [1] bootstrap checks failed
[1]: max file descriptors [65535] for elasticsearch process is too low, increase to at least [65536]
```

修改 /etc/security/limits.conf 文件, 添加“* - nofile 65536 * - memlock unlimited”


    