
---
title: go语言基础数据结构学习---- 数组, 列表(list)和切片(slice)
date: 2019-05-06 12:36:15
tags: GoLang
---


### go语言基础数据结构学习--> 数组, 列表(list)和切片(slice)
    go 语言中的  数组是类型相同的元素的集合, 
                列表是双链表的容器, 可以添加不同类型的数据
                切片是对现有数组的引用, 比数组更方便灵活, 还可以追加数据

```
package main

import (
    "container/list"
    "fmt"
)

func main() {
    // 切片 slice  比较常用, 很灵活
    list1 := [6]int{1,2,3,4}   //6是总数, 后面是值, 如果不够会自动补0
    list6 := []string{"a", "b"}
    var list2 [3]int
    // 声明列表, 下面两种为初始化, 生成内存地址, 双链表 ----容器
    var list3 = list.List{}
    list4 := list.New()
    //多维数组
    list5 := [3][2]string{
        {"飞", "小"},
        {"祥", "泰"},
        {"德", "丙"},
    }


    //列表插入方法
    a1 := list3.PushFront(2) //从左插入
    a2 :=list3.PushBack(1)  //从右插入
    list3.InsertAfter("after", a2)   //在 a2之后
    list3.InsertBefore("before", a1) //在 a1之前

    //列表删除
    list3.Remove(a2)

    //列表(容器)遍历
    for x := list3.Front(); x != nil; x = x.Next() {
        if x.Value == "after" {
            fmt.Println(x.Value)
        }
        fmt.Print(x.Value, " , ")
    }
    //切片遍历
    for _,x := range list1{
        if x == 1{
            fmt.Println(x)
        }
    }
    //切片追加
    list6 = append(list6, "c")
    //也可以和python一样根据索引覆盖值
    list1[5] = 9
    list2[2] = 9

    
    fmt.Println(list1)
    fmt.Println(list2)
    printlist(list3)
    fmt.Println(list4)
    fmt.Println(list5)
    fmt.Println(list6)
}

func printlist(lists list.List)  {
    for x := lists.Front(); x != nil; x = x.Next() {
        fmt.Println(x.Value)
    }
}
```

参考学习文档:
    https://www.cnblogs.com/liuzhongchao/p/9159896.html
    http://c.biancheng.net/view/35.html

    