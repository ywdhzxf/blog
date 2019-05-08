
---
title: 使用pyocr和tesseract 来解析数字图片
date: 2019-05-06 12:36:15
tags: Python爬虫,Python
---


##获取图片中的数字
因为最近要抓取的网站中有参数是在图片里面, 所以就需要来解析图片来获取参数, 图片清楚的话识别率是100%, 发出来工大家参考一下
	前期准备
	1  pip install  pyocr
	2  brew install  tesseract     安装参考博客  https://www.jianshu.com/p/719c053f170b
	3  pip3.6 install -i https://pypi.tuna.tsinghua.edu.cn/simple pillow    用镜像安装pillow

	##实现代码
	from urllib import request
	from PIL import Image
	import pyocr
	import pyocr.builders
	
	url = 'http://*******.png'
	#获取图片后10为作为图片名
	bug = url[-10:]
	path = f"/tmp/{bug}"
	#下载图片
	request.urlretrieve(url, path)
	#获取里面的数字
	nums = self.pic_num(pic=path)
	#删除图片
	os.remove(path)
	
	def pic_num(self, pic):
	    try:
	        tools = pyocr.get_available_tools()
	        print(tools)
	        if len(tools) == 0:
	            print("No OCR tool found")
	        tool = tools[0]
	        txt = tool.image_to_string(
	            Image.open(pic),
	            lang="eng",
	            builder=pyocr.builders.TextBuilder(tesseract_layout=6)
	        )
	        print(txt)
	        return txt
	    except Exception as e:
	        print('获取数字失败', e)
    