
---
title: Requests 和 Scrapy 添加动态IP代理
date: 2019-05-06 12:36:15
tags: Python爬虫
---


###Requests
	import requests
	
	# 要访问的目标页面
	targetUrl = "http://test.abuyun.com/proxy.php"
	#targetUrl = "http://proxy.abuyun.com/switch-ip"
	#targetUrl = "http://proxy.abuyun.com/current-ip"
	
	# 代理服务器
	proxyHost = "proxy.abuyun.com"
	proxyPort = "9000"
	
	# 代理隧道验证信息
	proxyUser = "H225506235A2NG0p"
	proxyPass = "123456"
	
	proxyMeta = "http://%(user)s:%(pass)s@%(host)s:%(port)s" % {
	    "host" : proxyHost,
	    "port" : proxyPort,
	    "user" : proxyUser,
	    "pass" : proxyPass,
	}
	
	proxies = {
	    "http"  : proxyMeta,
	    "https" : proxyMeta,
	}
	
	res = requests.get(targetUrl, proxies=proxies).text
	
	print(res.text)

#####scrapy

	import base64
	from scrapy.downloadermiddlewares.httpproxy import HttpProxyMiddleware
	
	# 代理服务器
	proxyServer = "http://proxy.abuyun.com:9010"
	
	# 隧道身份信息
	proxyUser = "H225506235A2NG0p"
	proxyPass = "123456"
	proxyAuth = "Basic " + str(base64.b64encode(str(proxyUser + ":" + proxyPass).encode('utf-8')), encoding='utf-8')
	
	class ProxyMiddleware(HttpProxyMiddleware):
	    proxies = {}
	
	    def __init__(self, auth_encoding='latin-1'):
	        self.auth_encoding = auth_encoding
	
	        self.proxies[proxyServer] = proxyUser + proxyPass
	
	    def process_request(self, request, spider):
	        request.meta["proxy"] = proxyServer
	
	        request.headers["Proxy-Authorization"] = proxyAuth


   

    