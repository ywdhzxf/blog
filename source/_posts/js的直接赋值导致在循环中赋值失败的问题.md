
---
title: js的直接赋值导致在循环中赋值失败的问题
date: 2019-05-06 12:36:15
tags: web前端
---


写js遇到了一个问题,就是说我在for循环值通过循环的值给一个对象赋值,但是的话每次赋值打印的结果都为最后一次赋的值,然后我就开始了debugger,发现我debug执行的话并没有问题,但是如果不debug就还会出现所有的赋值都是最后一个值得问题,这是我的代码

```
      var poster_name = this.More_Temp_count['posterity_name']
      var city = this.More_Temp_count['city']
      var blackwidow_task = this.More_Temp_count['blackwidow_task']
      var redis_key = blackwidow_task['redis_key']
      var task_id = blackwidow_task['task_id']
      var key_test = blackwidow_task['blackwidow_output']['db_config_test']['key']
      var key_db = blackwidow_task['blackwidow_output']['db_config']['key']

      this.loading = true
      for (var x in city_list){
        // 构造请求参数
        console.log('1')
        console.log(city_list[x])
        // 每次循环重新赋值
        var More_Temp_count_copy = this.More_Temp_count
        More_Temp_count_copy['city'] = city_list[x]
        console.log(More_Temp_count_copy['city'])
        More_Temp_count_copy['posterity_name'] = poster_name.replace(city,city_list[x])
        More_Temp_count_copy['blackwidow_task']['redis_key'] = redis_key.replace(city,city_list[x])
        More_Temp_count_copy['blackwidow_task']['task_id'] = task_id.replace(city,city_list[x])
        More_Temp_count_copy['blackwidow_task']['blackwidow_output']['db_config_test'] = key_test.replace(city,city_list[x])
        More_Temp_count_copy['blackwidow_task']['blackwidow_output']['db_config'] = key_db.replace(city,city_list[x])
        console.log('准备多次新增的复制模板信息',More_Temp_count_copy["city"])
        console.log('2')
      }
```

----------然后我以为是因为请求异步的问题,然后把每次的值添加到一个列表里,在通过索引进行获取,然而还是不对

---------最后公司大佬进行解决,是因为js的拷贝问题,js的=赋值会直接把对象的内存地址赋值过去,所以改More_Temp_count_copy这个参数就相当于改this.More_Temp_count,所以才导致问题出现,解决办法呢,就是用深拷贝,直接把对象转为字符串,然后将字符串拷贝过去,这样就不会有赋值失败的问题了,修改一行代码

```
        // 每次循环重新赋值
        var More_Temp_count_copy = JSON.parse(JSON.stringify(this.More_Temp_count))
```

问题解决!
    