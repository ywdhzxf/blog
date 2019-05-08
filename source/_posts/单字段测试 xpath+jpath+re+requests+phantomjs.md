
---
title: 单字段测试 xpath+jpath+re+requests+phantomjs
date: 2019-05-06 12:36:15
tags: Python爬虫,Python
---


### xpath+jpath+re单字段测试

最近测试发现这三个每次用都要重复写的东西太多了,然后封装了一下,做了一个单字段测试的类和接口,方便以后测试使用,只需要把类和包导入然后就可以直接使用了,简单方便

```
import re
import json,chardet
from lxml import etree
from jsonpath import jsonpath
import requests
class Spiders(object):
    def jpath(self, html,regex):
        body = str(html)  # 可能有乱码问题
        if isinstance(body, str) or isinstance(body, unicode):
            body = json.loads(body)
        try:
            result = jsonpath(body, regex)
        except Exception, e:
            result = []
            print e
        if not result:
            result = []
        return result

    def rpath(self, html,regex):
        try:
            body = html
            detector = chardet.detect(str(body))
            if detector.get("encoding") == "ascii":
                body = str(body).decode("unicode-escape")
        except Exception, e:
            body = str(html)
        result = re.findall(regex, body)
        return result

    def xpath(self, html,regex):
        parse_data = [""]
        if regex:
            regexs = regex.split("&")
            try:
                for i in range(len(regexs)):
                    xml = etree.HTML(html)
                    result = xml.xpath(regexs[i].strip())
                    if result:
                        return result
                return []
            except Exception, e:
                print e
        return parse_data
```

### 接口用的是post传参方式,根据困难度选择式调用requests或是phantomjs

```
def spider_xpath(request):
    result = {}
    # datas = []
    spider = Spiders()
    try:
        data = request.body
        data = json.loads(data)
        url = data['url']    #url
        rule = data['rule']  #抓取规则
        ru_type = data['type'] #xpath,re,jpath
        difficult = data['difficult'] #普通(a),特殊(b)
        if difficult == 'a':
            res = requests.get(url,headers={"User-Agent":"Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/64.0.3282.186 Safari/537.36"}).text
        else:
            browser = webdriver.PhantomJS(executable_path=r"../phantomjs_w/bin/phantomjs.exe")
            browser.get(url)
            time.sleep(2)
            res = browser.page_source
        if ru_type == 'xpath':
            datas = spider.xpath(res,rule)
        elif ru_type == 'rpath':
            datas = spider.rpath(res,rule)
        else:
            datas = spider.jpath(res,rule)
        detector = chardet.detect(str(datas))
        if detector.get("encoding") == "ascii":
            datas = str(datas).decode("unicode-escape")
        print datas

        result['page'] = datas
        result['message'] = '测试成功'
        result['code'] = 1
        print '成功'
    except Exception as e:
        print e
        result['message'] = '测试失败'
        result['code'] = -1
    return HttpResponse(json.dumps(result, cls=JSONEncoder), content_type="application/json")
```
    