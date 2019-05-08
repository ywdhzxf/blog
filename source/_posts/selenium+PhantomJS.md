
---
title: selenium+PhantomJS
date: 2019-05-06 12:36:15
tags: Python爬虫
---


### selenium+PhantomJS

```
一直没时间写,今天有时间来写一下
selenium+phantomjs是一个非常强大的工具,requests,urllib2是模拟请求发送参数获取页面,这个是直接用浏览器获取页面,很硬很强大的,
不过他也有一个致命的bug,速度!速度贼慢,所以说他只适合爬取某些特别困难而且数据量不大的网站,然后浏览器我一般都用pahntomjds,毕竟无界面,感觉比谷歌火狐能快一点.
```

```
说一下基本语法吧

from selenium import webdriver
from selenium.webdriver.common.keys import Keys

browser1 = webdriver.PhantomJS(executable_path=r"C:\Users\Administrator\Desktop\phantomjs-2.1.1-windows\bin\phantomjs.exe", )  # //内核 
###第一步往往是初学者最头疼的一步,因为有的时候你设置好了环境变量然后也不好用,所以说我一般都是直接用executable_path来指定路径,在项目里面也可以用相对路径来指定.

browser1.get('www.baidu.com')  ##输入要获取的网址
browser1.save_screenshot('a.png')  
###把当前打开的浏览器保存成图片,可以查看当前到哪步,建议在前面time.sleep()个一两秒,因为有的网站打开较慢,有延迟

print browser1.page_source   ###打印出当前获取到页面的源码

#这个相当于是css选择器,by后面的可以为id,name,class等.
res = browser1.find_element_by_id('fei').text 

# 获取标签名值
res = browser1.find_elements_by_tag_name("input")

# 也可以通过XPath来匹配
res = browser1.find_element_by_xpath("//input[@id='passwd-id']")


 #可以定位输入框来往里面输入值,一般用于模拟登陆和查询
browser1.find_element_by_id("fei").send_keys(u"飞啊飞") 

#模拟点击
browser1.find_element_by_id("fei").click()  

# ctrl+a 全选输入框内容
browser1.find_element_by_id("fei").send_keys(Keys.CONTROL,'a')

# ctrl+x 剪切输入框内容
browser1.find_element_by_id("fei").send_keys(Keys.CONTROL,'x')

# 输入框重新输入内容
browser1.find_element_by_id("fei").send_keys("baidu")

# 模拟Enter回车键
browser1.find_element_by_id("fei").send_keys(Keys.RETURN)

# 清除输入框内容
browser1.find_element_by_id("fei").clear()

# 关闭浏览器
browser1.quit()




```

### 鼠标操作

```
#导入 ActionChains 类
from selenium.webdriver import ActionChains

# 鼠标移动到 ac 位置
ac = driver.find_element_by_xpath('element')
ActionChains(driver).move_to_element(ac).perform()


# 在 ac 位置单击
ac = driver.find_element_by_xpath("elementA")
ActionChains(driver).move_to_element(ac).click(ac).perform()

# 在 ac 位置双击
ac = driver.find_element_by_xpath("elementB")
ActionChains(driver).move_to_element(ac).double_click(ac).perform()

# 在 ac 位置右击
ac = driver.find_element_by_xpath("elementC")
ActionChains(driver).move_to_element(ac).context_click(ac).perform()

# 在 ac 位置左键单击hold住
ac = driver.find_element_by_xpath('elementF')
ActionChains(driver).move_to_element(ac).click_and_hold(ac).perform()

# 将 ac1 拖拽到 ac2 位置
ac1 = driver.find_element_by_xpath('elementD')
ac2 = driver.find_element_by_xpath('elementE')
ActionChains(driver).drag_and_drop(ac1, ac2).perform()

```
###通过模拟登陆获取cookie
	
	登录完成后可以通过get_cookies()开获取到通行cookie
	cookie = browser1.get_cookies()
	
### 更多内容:

```
参考链接,写的很详细,内容也很到位
	链接：https://www.jianshu.com/p/4b89c92ff9b4
```
    