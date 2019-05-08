
---
title: supervisor的使用
date: 2019-05-06 12:36:15
tags: linux
---


	工作需要,学习一波

###常用
	supervisorctl status                   查看状态
	supervisorctl reload                   进程全部重启
	
	在查看状态中第一列就是进程名,可以根据进程名来对单个进程进行操作:
		supervisorctl stop app进程名   停止单个进程
		supervisorctl start app进程名   启动单个进程
	
	supervisorctl shutdown    关闭
	supervisorctl restart     重启
	
    