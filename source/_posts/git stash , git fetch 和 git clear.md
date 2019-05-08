
---
title: git stash , git fetch 和 git clear
date: 2019-05-06 12:36:15
tags: git
---


### git stash 		网上关于git stash的教程已经很多了，但是这个用多了确实很容易乱，所以除了特殊情况一般不推荐大家用这个	    特殊情况是什么呢？	    就是当你改变了本地的代码，但你不想提交，同时又想拉取最新的代码时，就可以用这个命令在进行暂存。	    具体用法也很简单：	    git stash将目前工作的修改保存到一个新的存储条，并且回滚到头; 	    git pop取出最新的一个存储条。	    git list查看所有的存储条的版本号	    git stash apply stash @ {1}取出版本号为1的工作存储条	    git stash clear清空所有的存储条	    相关的用法还有很多，这是最常用的几个。	    最后还是提醒一句，不要太常用这个，容易乱... 













### git fetch 
	放弃本地修改，强制更新
	git fetch --all 
	git reset --hard origin / master

###代码冲突
	git clean -d -fx ""

	x -----删除忽略文件已经对git来说不识别的文件
	d -----删除未被添加到git的路径中的文件
	f -----强制运行
    