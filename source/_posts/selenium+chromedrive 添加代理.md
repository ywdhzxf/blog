
---
title: selenium+chromedrive 添加代理
date: 2019-05-06 12:36:15
tags: Python爬虫
---


## selenium+chromedrive 添加代理, 有一个问题就是说不能在无头模式下使用,也就是说只能在本地使用, 我感觉应该是因为谷歌插件的问题, 在网上也没有找到比较好的方法,  下面是一套可以使用的代码, 其实本来phantomjs对代理的兼容性是最好的, 可惜不更新维护了, 所以只能等谷歌那边插件更新了

```
from selenium import webdriver
import string, time
import zipfile
# 代理服务器
proxyHost = "http-proxy-sg1.dobel.cn"
proxyPort = "9180"

# 代理隧道验证信息
proxyUser = "********"
proxyPass = "********"


def create_proxy_auth_extension(proxy_host, proxy_port,
                                proxy_username, proxy_password,
                                scheme='http', plugin_path=None):
    if plugin_path is None:
        plugin_path = r'{}_{}@http-dyn.dobel.com_9020.zip'.format(proxy_username, proxy_password)

    manifest_json = """
    {
        "version": "1.0.0",
        "manifest_version": 2,
        "name": "Dobel Proxy",
        "permissions": [
            "proxy",
            "tabs",
            "unlimitedStorage",
            "storage",
            "<all_urls>",
            "webRequest",
            "webRequestBlocking"
        ],
        "background": {
            "scripts": ["background.js"]
        },
        "minimum_chrome_version":"22.0.0"
    }
    """

    background_js = string.Template(
        """
        var config = {
            mode: "fixed_servers",
            rules: {
                singleProxy: {
                    scheme: "${scheme}",
                    host: "${host}",
                    port: parseInt(${port})
                },
                bypassList: ["foobar.com"]
            }
          };

        chrome.proxy.settings.set({value: config, scope: "regular"}, function() {});

        function callbackFn(details) {
            return {
                authCredentials: {
                    username: "${username}",
                    password: "${password}"
                }
            };
        }

        chrome.webRequest.onAuthRequired.addListener(
            callbackFn,
            {urls: ["<all_urls>"]},
            ['blocking']
        );
        """
    ).substitute(
        host=proxy_host,
        port=proxy_port,
        username=proxy_username,
        password=proxy_password,
        scheme=scheme,
    )

    with zipfile.ZipFile(plugin_path, 'w') as zp:
        zp.writestr("manifest.json", manifest_json)
        zp.writestr("background.js", background_js)

    return plugin_path


proxy_auth_plugin_path = create_proxy_auth_extension(
    proxy_host=proxyHost,
    proxy_port=proxyPort,
    proxy_username=proxyUser,
    proxy_password=proxyPass)

option = webdriver.ChromeOptions()
# option.add_argument('--no-sandbox')
# option.add_argument('--disable-gpu')
# option.add_argument("--start-maximized")
option.add_extension(proxy_auth_plugin_path)

drive = webdriver.Chrome(executable_path="../../config/chromedriver_mac",chrome_options=option)

drive.get("http://httpbin.org/ip")
print(drive.page_source)

drive.close()
```


    