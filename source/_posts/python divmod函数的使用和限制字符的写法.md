
---
title: python divmod函数的使用和限制字符的写法
date: 2019-05-06 12:36:15
tags: Python
---


###divmod
	python 的内置函数
		这个函数是实现 a除以b，然后返回商与余数的元组。如果两个参数a,b都是整数，那么会采用整数除法，结果相当于（a//b, a % b)。如果a或b是浮点数，相当于（math.floor(a/b), a%b)。
####例子
	print divmod(10,100)
	print divmod(100,10)
	值为:
	(0, 10)
	(10, 0)
###限定字串
	'%2d-%02d' % (5, 1)
	d是digit整数
	%02d是表示输出不小于两位数，不足两位前面填充0，
	f是float小数
	%.2f是保留2位小数，四舍五入，%.3f就是保留3位
####例子
	>>> '%2d-%02d' % (5, 1)
	' 5-01'
	>>> '%.2f' % 3.1415926
	'3.14'
##转换秒数格式
	seconds = 500
    m, s = divmod(seconds, 60)
    h, m = divmod(m, 60)
    print ("%02d:%02d:%02d" % (h, m, s))

    