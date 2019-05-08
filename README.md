博客搭建使用hexo, 官网地址
使用主题为 next, git地址:  https://github.com/theme-next/hexo-theme-next

## 配置记录
```
1 摘要模式(主题的config):
    auto_excerpt:
      enable: true
      length: 150    
      
2 背景随机图片  参考博客 https://blog.csdn.net/mango_haoming/article/details/78473243
    修改themes\next\source\css\ _custom\custom.styl 文件
    //http://lorempixel.com/1600/900
    //https://unsplash.it/1600/900?random（国内加载略慢）
    //https://uploadbeta.com/api/pictures/random/?key=BingEverydayWallpaperPicture【返回必应图片】
    //http://cn.bing.com/HPImageArchive.aspx?format=js&idx=0&n=1（必应返回JSON数据，具体百度
    
    body {
      background: url(https://uploadbeta.com/api/pictures/random/?key=BingEverydayWallpaperPicture);
      background-repeat: no-repeat;
      background-attachment: fixed;
      background-position: 50% 50%;
    }
    
    .main-inner {
      margin-top: 60px;
      padding: 60px 60px 60px 60px;
      //background: #fff;
      opacity: 0.9;
      min-height: 500px;
    }

```