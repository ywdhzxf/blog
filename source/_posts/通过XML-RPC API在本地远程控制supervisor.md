
---
title: 通过XML-RPC API在本地远程控制supervisor
date: 2019-05-06 12:36:15
tags: linux
---


### 通过XML-RPC API在本地远程控制supervisor

xml-rpc都已经把所有都封装好了,只需要根据文档选择自己需要调用的接口即可

下面是我写的两个测试代码

```
#coding:utf8
import xmlrpclib
server = xmlrpclib.Server('http://127.0.0.1:9001/RPC2')

#api方法 (官网参数: http://supervisord.org/api.html)
methods = server.system.listMethods()
print methods

#停止进程
# res = server.supervisor.stopProcess('text')
#开始进程
# res = server.supervisor.startProcess('text')
#获取进程信息
res = server.supervisor.getProcessInfo ('text')

print res
```

友情提示: 如果实在外网进行连接,记得把 配置文件(/etc/supervisord.conf)中的port端口开为 0.0.0.0:9001



关于supervisor的学习和部署  https://www.cnblogs.com/smail-bao/p/5673434.html

以及另外一种通过代码来连接服务器进行操作    http://blog.csdn.net/ywdhzxf/article/details/79461976
    