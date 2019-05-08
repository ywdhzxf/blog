
---
title: python脚本,从mongo取数据发送html格式表格邮件
date: 2019-05-06 12:36:15
tags: Python,数据库
---




####工作需要,我要把我的工作成果每隔三天发送邮件,展示三天的工作情况,所以在linux上写了个脚本,每三天发一次邮件,下面是源代码
```

coding: utf-8
import sys
reload(sys)
sys.setdefaultencoding('utf8')
from config import *
from mongo_db import MongoDB
import time,datetime
import random
import json
import arrow
import smtplib
from email.mime.multipart import MIMEMultipart
from email.mime.application import MIMEApplication
from email.mime.text import MIMEText
from email.header import Header
from email import encoders
#我是用当天日期作为表名存入mongo
#链接mongo进行查询
def select_mongo(data):
    pic_mongo = MongoDB(config = mongo_config).getClient().get_database('pic_db').get_collection(data)
    #查询值
    record = pic_mongo.find_one({"name": "log"})
    return record

def querydata():
    res = []
    records = []
    #获取现在的时间  "2018-01-20"
    qq = time.strftime("%Y-%m-%d")
    res.append(qq)
    #获取前两天的时间
    for x in range(1,3):
        now = arrow.get(qq)
        tomorrow = now.replace(days=-x)
        res.append(tomorrow.strftime("%Y-%m-%d"))
    print res
    sendhead = ['上传信息<br>']
    for tim in res:
        record =select_mongo(tim)
        records.append(record)
        sendhead.append('%s<br>' % tim)
    #print records
    tablecontent = '<table border="1" class="imagetable"><caption><h4>数据展示</h4></caption>'
    tablecontent += "<tr>"
    for title in sendhead:
        tablecontent += '<th>'+title+'</th>'
    tablecontent += "</tr>"
    for city_name in records[1]:
        if city_name == '_id' or city_name == 'name':
            pass
        else:
            tablecontent += '<tr>'
            tablecontent += '<td>%s</td>' % city_name
            #print city_name
            for record in records:
                count_sum = record[city_name]
                tablecontent += '<td>%s</td>' % count_sum
            tablecontent += '</tr>'

    tablecontent += '</table>'
    return tablecontent

head='''
<!DOCTYPE html>
<html>
 <head>
     <meta charset="utf-8"> 
     <title>数据展示</title>
     <meta name="viewport" content="width=device-width, initial-scale=1">
     <!-- <meta http-equiv="refresh" content="3600">  -->

  <style type="text/css">
            table.imagetable {
            font-family: verdana,arial,sans-serif;
          font-size:11px;
          color:#333333;
          border-width: 1px;
          border-color: #999999;
          border-collapse: collapse;
            width: 800px;
        }
        table.imagetable th {
            background:#b5cfd2 url('cell-white.jpg');
            border-width: 1px;
          padding: 8px;
          border-style: solid;
          border-color: #999999;
        }
        table.imagetable td {
            background:#dcddc0 url('cell-grey.jpg');
            border-width: 1px;
          padding: 8px;
          border-style: solid;
          border-color: #999999;
            width:150px;
        }
        table.imagetable td.tou {
            background:#dcddc0 url('cell-grey.jpg');
            border-width: 1px;
          padding: 8px;
          border-style: solid;
          border-color: #999999;
            width:800px;
        }
  </style>

 </head>
 <body>
'''
tail='''
 </body>
</html>
'''
res = querydata()
msg = MIMEMultipart()
content=head+res+tail
msgtitle = '【图片展示】'
text=MIMEText(content,'html','utf-8')
msg.attach(text)
msg['from'] = 'me'
msg['to'] = '小'
msg['Subject'] = msgtitle
s = smtplib.SMTP('smtp.exmail.qq.com')
s.login('邮箱', 'smtp码')
s.sendmail('邮箱', ['收件人邮箱'], msg.as_string())
print('success')
s.close()
if __name__ == "__main__":
    content = head+res+tail
    print content

```
    