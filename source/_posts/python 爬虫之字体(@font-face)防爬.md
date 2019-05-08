
---
title: python 爬虫之字体(@font-face)防爬
date: 2019-05-06 12:36:15
tags: Python爬虫
---


### python 爬虫 字体(@font-face)防爬
 
字体防爬就是该网站在源码上的字体不是正常字体编码, 可能是自定义的一种字体, 然后通过对应关系在页面上进行展示, 这就是所谓的字体防爬, 但是他们想要在页面上进行展示的话还是需要导入字体包的, 所以咱们只需要把字体包下载下来进行对应关系转换就可以获得正确的内容了

#### 一  主要是找到该网站导入的字体包的路径
 这就是一般网站的字体路径, 后面的那个url在新页面打开就可以自动下载字体![在这里插入图片描述](https://img-blog.csdnimg.cn/20181105191830583.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3l3ZGh6eGY=,size_16,color_FFFFFF,t_70)
	如果直接在源码找不见的话, 那就打开开发者调试工具, 在network里面搜索font 字体, 找到字体的url地址, 进行下载

#### 二 就是解析字体了
	需要下载  fontTools 包, 然后下面直接上代码
	from fontTools.ttLib import TTFont
	#解析字体文件，获取字体映射关系
	def parse_font():
	    font1 = TTFont('/Users/admin/Downloads/b.ttf')
	    keys, values = [], []
	    for k, v in font1.getBestCmap().items():
	        if v.startswith('uni'):
	            keys.append(eval("u'\\u{:x}".format(k) + "'"))
	            values.append(chr(int(v[3:], 16)))
	        else:
	            keys.append("&#x{:x}".format(k))
	            values.append(v)
	    print(keys, values)
	    return dict(zip(keys, values))
	这样就可以获取到 字体和编码的对应关系, 然后直接把抓取的乱码在对应关系里面进行转换就可以了
需要注意的是, 可能有的网站防爬可能会在编码上再给你加点难度, 比如数字的话:  你编码解出来是 5, 但实际是3, 遇到这种不要慌, 很有可能就是减法而已, 自己多测几次知道公式就好了

###参考链接
   https://blog.csdn.net/weixin_40214188/article/details/82596478

    