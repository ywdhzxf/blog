
---
title: 将python程序打包成exe文件和播放mp3
date: 2019-05-06 12:36:15
tags: Python
---


##打包文件
###使用工具
	PyInstaller
	直接pip install 就可以
###简单使用
	进入文件目录 pyinstaller my.py
	出现    successful 则为成功
###注意事项
	1 如果有大的模块的话很有可能会失败,比如 pandas
	2 打包完会生成两个文件夹和一个文件,可执行的文件在dist目录下的exe;
	3 如果代码里有路径操作则都以当前exe目录为准;
	4 源码可以删除
###使用参考博客
		https://blog.csdn.net/zengxiantao1994/article/details/76578421?locationNum=9&fps=1

##使用python播放音乐
	import pygame
       file=r'text.mp3'
       pygame.mixer.init()
       track = pygame.mixer.music.load(file)

       pygame.mixer.music.play()
       time.sleep(30)
       pygame.mixer.music.stop()
    