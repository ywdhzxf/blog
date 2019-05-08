
---
title: Scrapy中加入selenium+PhantomJS
date: 2019-05-06 12:36:15
tags: Python爬虫
---


## 人生不如意之事十有八九,最近遇到了一个棘手的网站,防爬贼硬,所以喽,就想到了把phantomjs加入到公司的框架中,然后种子利用框架进行爬取,详情一就用scrapy;

​	不说废话,直接上代码,不多

在中间键中,加入一个phantomjs的类

```
from selenium import webdriver
from scrapy.http import HtmlResponse


class PhantomJSMiddleware(object):
    @classmethod
    def process_request(cls, request, spider):
        driver = webdriver.PhantomJS(
            executable_path=r"../phantomjs_w/bin/phantomjs")#路径自己定义
        driver.get(request.url)
        content = driver.page_source.encode('utf-8')
        driver.quit()
        print 'success'
        return HtmlResponse(request.url, encoding='utf-8', body=content, request=request)
#将phantomjs得到的数据返回到scrapy的处理器进行处理
```
然后在settings里加入中间键权重

```
#可以写个判断,传入固定的某个值才会触发这个中间件,毕竟phantomjs确实是慢,很影响效率,我只用它爬这个网站的种子

'ceshi.middlewares.PhantomJSMiddleware':500,  #权重自己定义,看自己框架规则
```

这就就OK了,可以放心大胆地写爬虫了,友情提醒,少用这个,毕竟效率真的是慢,遇到反爬严重的可以用这个,还有注意自己公司的框架中间件,改好权重值,不然可能顺序错乱,一般用最后就好
    