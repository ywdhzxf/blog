
---
title: python常用的一些方法
date: 2019-05-06 12:36:15
tags: Python
---


###列表分组
	根据每个列表的最大数进行分组，返回多个列
	def list_of_groups（init_list，childern_list_len）：
	    list_of_groups = zip（*（iter（init_list），）* childern_list_len）
	    end_list = [list（i）for our here_of_groups] 
	    count = len（init_list）％childern_list_len 
	    end_list.append（ini​​ t_list [-count：]）if count！= 0 else end_list 
	    return end_list 
	list_of_groups（列表，10）

### 生成时间列表
	import datetime,time
	##生成时间列表
	def create_assist_date(self, datestart=None, dateend=None):
	    # 创建日期辅助表
	    if dateend is None:
	        dateend = datetime.datetime.now().strftime('%Y%m%d')
	    # 转为日期格式`
	    datestart = datetime.datetime.strptime(datestart, '%Y%m%d')
	    dateend = datetime.datetime.strptime(dateend, '%Y%m%d')
	    date_list = []
	    date_list.append(datestart.strftime('%Y%m%d'))
	    while datestart < dateend:
	        # 日期叠加一天
	        datestart += datetime.timedelta(days=+1)
	        # 日期转字符串存入列表
	        date_list.append(datestart.strftime('%Y%m%d'))
	    return date_list


	##时间转换  + -
	datestart = datetime.datetime.strptime('20170715', '%Y%m%d')
	datestart += datetime.timedelta(days=-36)
	start = datestart.strftime('%Y%m%d')
	date_list = create_assist_date(start, '20170715')

###获取列表的值的索引
    知道列表的元素但不知道索引，可以用索引方法来进行查取，不过最好先设定一下，避免列表里有重复数据
	list.index（ '想要查索引的元素'）

## 获取当前机器的cpu和内存使用率
	import psutil
	memory_now = psutil.virtual_memory().percent
    cpu_now = psutil.cpu_percent(interval=1)


###获取当前的Python脚本运行的PID和机器IP
	
	import platform
	import socket
	pids = os.getpid()
    addrs = socket.getaddrinfo(socket.gethostname(), None)
	ip = [item[4][0] for item in addrs if ':' not in item[4][0]][0]
    pid = re.findall("\d+", str(pids))[0]
  
### 列表排序
```
按照a倒叙排列, 当a相同时, 按b倒叙排列
all_list = [{"a": 10, "b": 22}, {"a": 11, "b": 23}, {"a": 11, "b": 12}]
all_list.sort(key=lambda x: (-x["a"], -x["b"]))
```



    