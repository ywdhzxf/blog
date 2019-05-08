
---
title: 用flask完成mongo的增删改查
date: 2019-05-06 12:36:15
tags: 数据库,Python
---


### 用flask小小的写了一下mongo的增删改查,挺好用的

上代码

```
#coding:utf8
from bson.objectid import ObjectId
from pymongo import MongoClient
from flask import Flask,url_for
app = Flask(__name__)
client = MongoClient('127.0.0.1',27017)
db = client.spider_rules
coon = db.rules_template
# items =  coon.find_one({'source_name':'cdfgj'})
# print items
# print 2
@app.route("/select/<source_name>")
def select(source_name):
    print 1
    res = {}
    x = coon.find_one({'source_name':source_name})
    print type(x)
    for y in x:
        res[y] = x[y]
    print res
    return  str(res)

@app.route("/dele/<source_name>")
def dele(source_name):
    print source_name
    source_name = {'_id': ObjectId(source_name)}
    if coon.find(source_name):
        print type(source_name),source_name
        coon.remove(source_name)
        res = 'suessce'
    else:
        res = 'bad'
    return  str(res)

@app.route("/add/<source_name>")
def addd(source_name):
    coon.insert({'name':source_name})
    if coon.find({'name':source_name}):
        print source_name
        res = 'suessce'
    else:
        res = 'bad'
    return  str(res)

@app.route("/update/<source_name>/<sou>")
def up(source_name,sou):
    coon.update({'name':source_name},{'name':sou})
    if coon.find({'name':sou}):
        print sou
        res = 'suessce'
    else:
        res = 'bad'
    return  str(res)





@app.route("/xiaofei")
def yes():
    return "小飞"
if __name__ == '__main__':
    app.run(debug=True)
    # with app.test_request_context():
    #     print url_for('hello', source_name='cdfgj')
```

    