
---
title: pycurl的学习之路
date: 2019-05-06 12:36:15
tags: Python
---


### pycurl的模块用法

```
c = pycurl.Curl()    #创建一个curl对象 

c.setopt(pycurl.CONNECTTIMEOUT, 5)    #连接的等待时间，设置为0则不等待  

c.setopt(pycurl.TIMEOUT, 5)           #请求超时时间  

c.setopt(pycurl.NOPROGRESS, 0)        #是否屏蔽下载进度条，非0则屏蔽  

c.setopt(pycurl.MAXREDIRS, 5)         #指定HTTP重定向的最大数  

c.setopt(pycurl.FORBID_REUSE, 1)      #完成交互后强制断开连接，不重用  

c.setopt(pycurl.FRESH_CONNECT,1)      #强制获取新的连接，即替代缓存中的连接  

c.setopt(pycurl.DNS_CACHE_TIMEOUT,60) #设置保存DNS信息的时间，默认为120秒  

c.setopt(pycurl.URL,"http://www.baidu.com")      #指定请求的URL  

c.setopt(pycurl.USERAGENT,"Mozilla/5.2 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322; .NET CLR 2.0.50324)")    #配置请求HTTP头的User-Agent

c.setopt(pycurl.HEADERFUNCTION, getheader)   #将返回的HTTP HEADER定向到回调函数getheader

c.setopt(pycurl.WRITEFUNCTION, getbody)      #将返回的内容定向到回调函数getbody

c.setopt(pycurl.WRITEHEADER, fileobj)        #将返回的HTTP HEADER定向到fileobj文件对象

c.setopt(pycurl.WRITEDATA, fileobj)          #将返回的HTML内容定向到fileobj文件对象

c.getinfo(pycurl.HTTP_CODE)         #返回的HTTP状态码

c.getinfo(pycurl.TOTAL_TIME)        #传输结束所消耗的总时间

c.getinfo(pycurl.NAMELOOKUP_TIME)   #DNS解析所消耗的时间

c.getinfo(pycurl.CONNECT_TIME)      #建立连接所消耗的时间

c.getinfo(pycurl.PRETRANSFER_TIME)  #从建立连接到准备传输所消耗的时间

c.getinfo(pycurl.STARTTRANSFER_TIME)    #从建立连接到传输开始消耗的时间

c.getinfo(pycurl.REDIRECT_TIME)     #重定向所消耗的时间

c.getinfo(pycurl.SIZE_UPLOAD)       #上传数据包大小

c.getinfo(pycurl.SIZE_DOWNLOAD)     #下载数据包大小 

c.getinfo(pycurl.SPEED_DOWNLOAD)    #平均下载速度

c.getinfo(pycurl.SPEED_UPLOAD)      #平均上传速度

c.getinfo(pycurl.HEADER_SIZE)       #HTTP头部大小 
```

### 发送post请求

```
#coding:utf8
import pycurl
import StringIO 
import urllib 
url ="http://www.baidu.com"
post_data_dic = {"project":"test"}
crl = pycurl.Curl() 
crl.setopt(pycurl.VERBOSE,1) 
crl.setopt(pycurl.FOLLOWLOCATION, 1) 
crl.setopt(pycurl.MAXREDIRS, 5)
crl.setopt(pycurl.CONNECTTIMEOUT, 60) 
crl.setopt(pycurl.TIMEOUT, 300)
crl.setopt(pycurl.HTTPPROXYTUNNEL,1)
crl.fp = StringIO.StringIO() 
crl.setopt(pycurl.USERAGENT,"dhgu hoho")
crl.setopt(crl.POSTFIELDS, urllib.urlencode(post_data_dic)) 
crl.setopt(pycurl.URL, url) 
crl.setopt(crl.WRITEFUNCTION, crl.fp.write) 
crl.perform() 
print crl.fp.getvalue() 
```
    