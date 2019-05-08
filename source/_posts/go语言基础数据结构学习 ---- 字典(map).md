
---
title: go语言基础数据结构学习 ---- 字典(map)
date: 2019-05-06 12:36:15
tags: GoLang
---


### go语言基础数据结构学习--> 字典(map)
    go 语言中的字典和python 中的字典特性差不多 
        相同: 键值对, 无序集合, 每个键都是唯一的, 对一个键多次赋值会更新当前键的值;
        不同: go语言的字典里面的类型是定好的, 不可变更, python可以随意写类型.

```
    package main
    import "fmt"

    //字典和python是一样, 无序的

    //声明新的类型
    type Fei struct {
        id   int
        name string
    }
    type Dic map[string]int

    func main()  {
        //声明字典
        dict := make(map[string]string)
        dicts := map[string]int{ "age": 10, "丙总": 2}
        //新类型
        result := make(map[int]*Fei)
        result[0] = &Fei{ id: 6300, name: "刀妹"}
        letter := []string{"a", "b", "c", "d", "e", "f", "g", "h"} //数组

        //用 dict[name] = value 来设置值和修改
        dict["name"] = "薇恩"
        dict["age"] = "18"
        dict["label"] = "小飞"
        //新类型的值修改
        ss := result[0]
        ss.id = 4800

        //打印字典的值
        name := dict["name"]
        res := dict["res"]
        fmt.Println(name)
        fmt.Println(res)

        //打印字典元素个数
        fmt.Println("lens", len(dict))

        //删除字典元素,  有则删除, 无则不删
        delete(dict, "label")
        delete(dict, "ask")
        //删除全部需要循环
        for k := range dict{
            delete(dict, k)
        }
        //批量添加字典
        for k,v := range letter{
            fmt.Println("还可以", k, v)
            dicts[v] = k
        }


        fmt.Println(dict)
        fmt.Println(dicts)
        fmt.Println(result[0])


        //字典的嵌套操作
        respon := make(map[string]Dic)
        DicNum := make(Dic)     //make 初始化, 分配内存地址, 不为 nil
        DicNum["id"] = 1
        DicNum["age"] = 2
        respon["ids"] = DicNum
        respon["type"]  = Dic{"id": 11, "age": 22}


        fmt.Println(respon)

}
```

    