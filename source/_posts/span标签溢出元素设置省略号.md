
---
title: span标签溢出元素设置省略号
date: 2019-05-06 12:36:15
tags: web前端
---


###span
	    我一个写爬虫的也开始搞前端了,工作需要吗.
	    然后这次的遇到问题是我想把span标签的文本限定一下,让他到一定程度就展示省略号,然后就写了元素溢出的属性:
	    overflow: hidden; 
        text-overflow: ellipsis; 
    但是不成功,然后找原因,原来span标签为行内元素,必须要让他显示为块级元素才可以,加上属性:
        display: inline-block;
    后成功解决.

	贴一下  完美人生级代码:
	    style="overflow:hidden;
	    text-overflow:ellipsis;
	    white-space:nowrap;
		-webkit-line-clamp: 1;
		-webkit-box-orient: vertical;
		word-break: break-all;width:100%;"
   写的是有点复杂了,其实我是不需要换行的,保险起见嘛,稳妥.
   参考的博客文章也贴一下: 
   http://blog.csdn.net/u010688587/article/details/53672793
   
    