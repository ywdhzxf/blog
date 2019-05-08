
---
title: python jpath的使用
date: 2019-05-06 12:36:15
tags: Python爬虫
---


### jsonpath

一种跟xpath语法差不多的,专门用来解析json格式的提取方法

```
from jsonpath_rw import jsonpath, parse

html = {"rating":{"max":10,"numRaters":79,"average":"9.1","min":0},"subtitle":"","author":["野夫"],"pubdate":"2013-9","tags":[{"count":313,"name":"野夫","title":"野夫"},{"count":151,"name":"散文随笔","title":"散文随笔"},{"count":83,"name":"身边的江湖","title":"身边的江湖"},{"count":82,"name":"土家野夫","title":"土家野夫"},{"count":70,"name":"散文","title":"散文"},{"count":44,"name":"中国文学","title":"中国文学"},{"count":43,"name":"随笔","title":"随笔"},{"count":38,"name":"中国现当代文学","title":"中国现当代文学"}],"origin_title":"","image":"http://img5.douban.com/mpic/s27008269.jpg","binding":"","translator":[],"catalog":"自序 让记忆抵抗n001 掌瓢黎爷n024 遗民老谭n039 乱世游击：表哥的故事n058 绑赴刑场的青春n076 风住尘香花已尽n083 “酷客”李斯n100 散材毛喻原n113 颓世华筵忆黄门n122 球球外传：n一个时代和一只小狗的际遇n141 童年的恐惧与仇恨n151 残忍教育n167 湖山一梦系平生n174 香格里拉散记n208 民国屐痕","pages":"256","images":{"small":"http://img5.douban.com/spic/s27008269.jpg","large":"http://img5.douban.com/lpic/s27008269.jpg","medium":"http://img5.douban.com/mpic/s27008269.jpg"},"alt":"http://book.douban.com/subject/25639223/","id":"25639223","publisher":"广东人民出版社","isbn10":"7218087353","isbn13":"9787218087351","title":"身边的江湖","url":"http://api.douban.com/v2/book/25639223","alt_title":"","author_intro":"郑世平，笔名野夫，，以其特有的韵律表达世间的欢笑和悲苦。","price":"32元"}
res = parse("$.rating.average")
cont = res.find(html)
for x in cont:
	print x.value
```
    