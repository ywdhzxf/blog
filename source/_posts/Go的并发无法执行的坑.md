
---
title: Go的并发无法执行的坑
date: 2019-05-06 12:36:15
tags: GoLang
---



## 前言
Go 语言本身支持并发, 只需要通过 Go来启动goroutine就可以了, 语法格式也很简单, 就直接在调用方法前加上go 关键字就可以了, 例如
```
    go hello(x)
```
## 遇到的问题
Go 允许使用go 语句开启一个goroutine (线程)去执行这个函数, 很简单, 但是有一个新手需要注意的地方(比如我), 那就是函数运行时间和进程的运行时间, 因为go语句是开启一个新的, 刚创建的goroutine去运行这个函数, 但是本身的主进程还会继续运行, 所以, 如果你只写一个go语句, 后面没有可以运行程序的话就会出现一个尴尬的问题, 主进程直接关闭, 对应goroutine也直接关闭,导致函数没有运行

可以参考一下下面的例子
```
package main

import (
	"fmt"
	"time"
)

func hello(aa string) {
	for a := 0; a < 3; a++ {
		fmt.Println(aa)
		time.Sleep(3 * time.Second)
	}
}
func main() {
	go hello("小飞")
	go hello("飞啊飞")
	// time.Sleep(100 * time.Second) 不加这行代码的话就会出现这种情况
}
```
运行良好的结果
```
飞啊飞
小飞
小飞
飞啊飞
小飞
飞啊飞
```
可以看到顺序不固定, 因为是多个goroutine执行的

    