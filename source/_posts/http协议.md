
---
title: http协议
date: 2019-05-06 12:36:15
tags: Python爬虫
---


## http协议

```
http是一个属于应用层面的面向对象的协议，由于其简捷，快速的方式，适用于分布式超媒体信息系统。
主要特点：
1.支持客户／服务器模式
2.简捷快速：客户向服务器请求服务时，只需传送请求方法和路径。请求方法常用的有get,post,head.每种方法规定了客户与服务器联系的类型不同。由于http协议简单，使得http服务器的程序规模小，通信数度快。
3.灵活：http允许传输任意类型的数据对象，正在传输的类型由content-type加以标记
4.无连接：无连接的含义是限制每次链接只处理一个请求。服务器处理完客户的请求，并收到客户的应答后，即断开链接，这样可以节省传输时间。
5.无状态：http协议是无状态协议，无状态是指协议对于事务处理没有记忆能力。缺少状态意味着如果后续处理需要前面的信息，则它必须重传，这样可能导致每次连接传送的数据量增大。另一方面，在服务器不需要先前信息时它的应答就较快。
```

### 解释下Http请求头和常见响应状态码

#### 请求头：

```
Accept:指浏览器或其他客户可以接爱的MIME文件格式。可以根据它判断并返回适当的文件格式。
Accept-Charset：指出浏览器可以接受的字符编码。英文浏览器的默认值是ISO-8859-1.
Accept-Language：指出浏览器可以接受的语言种类，如en或en-us，指英语。
Accept-Encoding：指出浏览器可以接受的编码方式。编码方式不同于文件格式，它是为了压缩文件并加速文件传递速度。浏览器在接收到Web响应之后先解码，然后再检查文件格式。
Cache-Control：设置关于请求被代理服务器存储的相关选项。一般用不到。
Connection：用来告诉服务器是否可以维持固定的HTTP连接。HTTP/1.1使用Keep-Alive为默认值，这样，当浏览器需要多个文件时(比如一个HTML文件和相关的图形文件)，不需要每次都建立连接。
Content-Type：用来表名request的内容类型。可以用HttpServletRequest的getContentType()方法取得。
Cookie：浏览器用这个属性向服务器发送Cookie。Cookie是在浏览器中寄存的小型数据体，它可以记载和服务器相关的用户信息，也可以用来实现会话功能。
```

#### 状态码：

```
状态代码有三位数字组成，第一个数字定义了响应的类别，且有五种可能取值：
1xx：指示信息--表示请求已接收，继续处理
2xx：成功--表示请求已被成功接收、理解、接受
3xx：重定向--要完成请求必须进行更进一步的操作
4xx：客户端错误--请求有语法错误或请求无法实现
5xx：服务器端错误--服务器未能实现合法的请求
常见状态代码、状态描述、说明：
200 OK     //客户端请求成功
400 Bad Request  //客户端请求有语法错误，不能被服务器所理解
401 Unauthorized //请求未经授权，这个状态代码必须和WWW-Authenticate报头域一起使用
403 Forbidden  //服务器收到请求，但是拒绝提供服务
404 Not Found  //请求资源不存在，eg：输入了错误的URL
500 Internal Server Error //服务器发生不可预期的错误
503 Server Unavailable  //服务器当前不能处理客户端的请求，一段时间后可能恢复正常
eg：HTTP/1.1 200 OK （CRLF）
```

python多线程

```
http://python.jobbole.com/85050/  一篇比较详细的博文


class MyThread(threading.Thread):
    def init(self):
        threading.Thread.init(self)
def run(self):
    lock.acquire()
    print threading.currentThread().getName()
    lock.release()
 
def build_worker(num):
    workers = []
    for t in range(num):
        work = MyThread()
        work.start()
        workers.append(work)
    return workers
def producer():
    threads = build_worker(4)
    for w in threads:
        w.join()
    print 'Done'
```

```
pool = ThreadPool()创建了线程池，其默认值为当前机器 CPU 的核数，可以指定线程池大小，不是越多越好，因为越多的话，线程之间的切换也是很消耗资源的。
results = pool.map(urllib2.urlopen,urls) 该语句将不同的url传给各自的线程，并把执行后结果返回到results中。

import urllib2
 
from multiprocessing.dummy import Pool as ThreadPool
 
urls = ['http://www.baidu.com','http://www.sina.com','http://www.qq.com']
 
pool = ThreadPool()
 
results = pool.map(urllib2.urlopen,urls)
print results
pool.close()
pool.join()
 
print 'main ended'



http://www.doc88.com/p-0803296137106.html  这个是异步i／o及多线程
```

```
http://cuiqingcai.com/3335.html  静觅。多线程爬虫
```

### mongodb的常用语法。       http://www.cnblogs.com/leskang/p/6000852.html

### 什么是mongodb

```
MongoDB 是由C++语言编写的，是一个基于分布式文件存储的开源数据库系统。
在高负载的情况下，添加更多的节点，可以保证服务器性能。
MongoDB 旨在为WEB应用提供可扩展的高性能数据存储解决方案。
MongoDB 将数据存储为一个文档，数据结构由键值(key=>value)对组成。MongoDB 文档类似于 JSON 对象。字段值可以包含其他文档，数组及文档数组。

```



python操作数据库

```
import pymongo
con = pymongo.Connection('localhost', 27017)
mydb = con.mydb # new a database
mydb.add_user('test', 'test') # add a user
mydb.authenticate('test', 'test') # check auth
muser = mydb.user # new a table
muser.save({'id':1, 'name':'test'}) # add a record
muser.insert({'id':2, 'name':'hello'}) # add a record
muser.find_one() # find a record
muser.find_one({'id':2}) # find a record by query
muser.create_index('id')
muser.find().sort('id', pymongo.ASCENDING) # DESCENDING
# muser.drop() delete table
muser.find({'id':1}).count() # get records number
muser.find({'id':1}).limit(3).skip(2) # start index is 2 limit 3 records
muser.remove({'id':1}) # delet records where id = 1
muser.update({'id':2}, {'$set':{'name':'haha'}}) # update one recor
db.auth(usrename,password) 设置数据库连接验证
```



```
1.mongodb默认端口是27017，上面步骤mongod 命令是属于启动mongo服务端命令，启动后不能关闭，否则mongo就关闭了导致链接时出现10061错误，所以要新开启一个窗口执行：mongo localhost:27017，表示客户端连接
2.注：mongodb可以不设账号密码，通过IP地址和端口直接链接
3.退出输入：exit
4.在mongodb中基本的概念是文档、集合、数据库，下面介绍。
5.MongoDB的默认数据库为"db"，该数据库存储在data目录中。
6.MongoDB的单个实例可以容纳多个独立的数据库，每一个都有自己的集合和权限，不同的数据库也放置在不同的文件中。
 
```

|    SQL术语     |  mongodb术语   |          解释／说明          |
| :----------: | :----------: | :---------------------: |
|   Database   |   Database   |           数据库           |
|    table     |  Collection  |         数据库表／集合         |
|     Row      |   Document   |        数据记录行／文档         |
|    Column    |    Field     |         数据字段／域          |
|    Index     |    Index     |           索引            |
| Table joins  |              |     表链接，mongodb不支持      |
| Primary  key | Primary  key | 主键，mongodb自动将_id字段设置为主键 |

Mongoldb 数据库语法

```
show dbs;//查看所有的数据库
db;//查看当前窗口所在的数据库
use 数据库名；//如果数据库不存在，则创建数据库，否则切换到指定数据库。
注：show dbs执行结果没有看到test库，但是db查看当前库确是test库，因为test库中刚开始没有任何数据并且是在内存中的，有了数据后就会显示出来了（其他新创建的数据库也是如此）
db.dropDatabase();//删除当前数据库，默认为 test，故要切换到某个数据库下进行删除
```

集合

```
显式创建集合：db.createCollection("collectionName");//创建一个名为collectionName的集合，创建完成后会返回 {"ok",1} json串
隐式创建集合：db.collection2.insert({name:"xiaomu",age:20});//往collection2集合中添加数据来创建集合，如果集合不存在就自动创建集合，返回：WriteResult({"nInserted":1})
show collections;//查看集合
db.collection1.count();//统计集合collection1中的数据数量
db.collection1.drop();//删除集合collection1
注：mongo中支持js，可通过js操作实现批零处理，如：for(var i=0;i<1000;i++){db.collection2.insert({name:"xiaomu"+i,age:20+i});}
固定集合
固定集合指的是事先创建而且大小固定的集合。
固定集合特性：固定集合很想环形队列，如果空间不足，最早的文档就会被删除，为新的文档腾出空间。一般来说，固定集合适用于任何想要自动淘汰过期属性的场景，没有太多的操作限制.
db.createCollection("collectionName",{capped:true,size:10000,max:100});//size指定集合大小，单位为KB，max指定文档数量
当文档数量上限时必须同时指定大小。淘汰机制只有在容量还没满时才会依据数量来工作。要是容量满了则会依据容量来工作。
```


    