
---
title: scrapyd的安装和部署
date: 2019-05-06 12:36:15
tags: Python爬虫
---


### windows下scrapyd的安装和部署

#### 1 安装

```
环境要求:
    python 2.6 以上
    Twisted  8.0 以上
    scrapy 
    setuptools
    scrapyd-client
 直接 pip install scrapyd 就可以
 在cmd输出scrapyd,然后在浏览器端访问  http://localhost:6800/   就可以成功访问
```

#### 2 部署scrapy项目

```
scrapy startproject 项目名
然后会有一个scrapy.cfg的文件
![文件](http://img.blog.csdn.net/20180303173818819?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXdkaHp4Zg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

好了之后在cmd项目目录直接启动scrapyd,然后再打开新的cmd进行项目部署
	![启动成功](http://img.blog.csdn.net/20180303173154636?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXdkaHp4Zg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
项目部署直接通过scrapyd-deploy进行部署即可,找到安装好的scrapyd-client文件夹,在site-packages里面,打开把 scrapyd-deploy 复制到 C:\Python27\Scripts(自己的python安装目录)下,然后新建文件 scrapyd-deploy.bat ,在里面输入
	@echo off 
	"C:\Python27\python.exe" "C:\Python27\Scripts\scrapyd-deploy" %1 %2 %3 %4 %5 %6 %7 %8 %9
里面的路径同样是你的python安装路径
```

#### 3 使用scrapyd-deploy进行部署

```
同样是cmd进入scrapy项目路径,指令格式为 scrapyd-deploy <target> -p <project> 
* target就是配置文件的deploy的名称，针对上面的配置就是demo 
* project如果不输就是配置文件中的project

本例部署的指令：scrapyd-deploy demo 
	![部署成功](http://img.blog.csdn.net/20180303173212409?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXdkaHp4Zg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
如果部署失败请参考  http://blog.csdn.net/ywdhzxf/article/details/79430378

部署成功后就可以在scrapy项目里看见一个eggs文件夹,里面所存放的就是scrapyd-deploy的工程打包成.egg的文件，可以看到version就是文件的名称，每当我们执行一次scrapyd-deploy就会生成一个新的egg
```

#### 4 运行Spider

```, 
我就随便写了一个进行测试,爬虫名叫 bai_spider,，现在就可以用API中的请求去调用或者执行爬虫了，这里以schedule.json为示例(详细参数http://scrapyd.readthedocs.io/en/stable/api.html#schedule-json)： 
	curl http://localhost:6800/schedule.json -d project=fei -d spider=bai_spider
	
curlwindows安装指南    http://blog.csdn.net/ywdhzxf/article/details/79431414
	
	返回OK就成功了,可以通过scrapyd的jobs目录查看爬虫的运行情况


参考博客:   http://blog.csdn.net/u013708440/article/details/53425655
```

    