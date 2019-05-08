
---
title: 关于scrapyd-deploy项目部署时出现environment can only contain strings的解决方法
date: 2019-05-06 12:36:15
tags: Python爬虫
---


   在进行scrapyd学习的时候,用scrapyd-deploy进行项目部署,出现了一个错误![这里写图片描述](http://img.blog.csdn.net/2018030314480491?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXdkaHp4Zg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
	显示是环境只能包含字符串,然后我就在网上进行搜索,发现好多人都碰到过这个问题,没什么有效答案,然后我就找大神进行一波问题解决
    根据错误找原因,在scrapyd源码中有一个utils.py文件,打开这个文件
在126行和130行进行一点改动
![这里写图片描述](http://img.blog.csdn.net/20180303145420627?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXdkaHp4Zg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
    将这两个参数改为str类型,问题解决![这里写图片描述](http://img.blog.csdn.net/20180303145540535?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXdkaHp4Zg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)


    

    