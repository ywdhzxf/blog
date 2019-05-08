
---
title: go time常用方法
date: 2019-05-06 12:36:15
tags: GoLang
---


## 前言
最近开发项目经常用到go的time包, 照python的略微麻烦一些, 特别是那个layout被无数人吐槽(包括我), 这里整理了一些常用的方法, 有需要的可以了解一下

```
package main

import (
	"time"
	"fmt"
)

func main() {
	// time函数  layout  2006-01-02 15:04:05

	//生成时间
	time.Now()
	time.Now().Unix()

	//时间转换  time.Format  根据更改layout转成任何自己想要的格式化字段
	time.Now().Format("2006-01-02")
	time.Now().Format("200601")

	//格式时间转换为time类型
	a := "20190606"
	b, _ := time.Parse("20060102", a)
	fmt.Println(b.Unix())
	//时间戳转为time类型
	t := time.Unix(time.Now().Unix(), 0)
	fmt.Println(t)

	//time时间操作
	tomrrow := time.Now().AddDate(0, 0, 1) //明天
	time.Now().AddDate(0, -1, 0)           //上月
	//也可以是一段时间
	fmt.Println(t.Add(time.Duration(10) * time.Minute))

	//判断时间前后
	bol1 := t.After(tomrrow)
	bol2 := t.Before(tomrrow)
	fmt.Println(bol1, bol2)

	//计算日期时间差  一般都是跟 Add方法一块使用
	fmt.Println(t.Sub(tomrrow))
	
	//计算日期离今天间隔几天
	aaa, _ := time.Parse("20060102", a)
	fmt.Println(int64(aaa.Sub(time.Now()).Hours() / 24))
	
	//获取明天凌晨的时间戳
	t = time.Now()
	zero := time.Date(t.Year(), t.Month(), t.Day()+1, 0, 0, 0, 0, t.Location()).Unix()
	fmt.Println(zero)
}

```

    