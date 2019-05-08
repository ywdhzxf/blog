
---
title: git cherry-pick
date: 2019-05-06 12:36:15
tags: git
---


###git cherry-pick
	说一下我工作中常用的一条git 命令,简单高效
	工作分支一般是在 develop上,然后在工作分支修改的代码提交到线上时很容易出现错误.冲突 等之类的问题,然后有的时候提交的文件过于分散和量大,你又不想一个一个的checkout 添加,怎么办?git cherry-pick就是最好的方法:
	语法很简单,我们常用的提交就是 
		git  add   
		git commit
		git pull 
		git push
	然后提交线上就是
		git checkout develop a.txt
	很麻烦对吧,然后如果你会用git cherry-pick这条命令,就会发现很简单:
		git cherry-pick <commit id>
		git pull
		git push
	就OK了,是不是很简单,然后这个只会提交你的commit id 的修改情况,也极大程度的避免了冲突的问题. 
    