---
title: markdown常用语法小结
date: 2016-09-02 22:17:32
tags: hexo
categories: 技术
---

## 前言
本文对常用markdown语法进行小结，按使用频率排序，持续更新中。

## 语法
### 1.设置标题
文字下方放置若干“=”：一级标题
=================
文字下方放置若干“-”：二级标题
-----------------
### 文字前方放置1-6个“#+空格”：1-6级标题（该示例为三级标题）
![](http://ww3.sinaimg.cn/mw690/a8fc9690gw1f7fp15hlyej20dj034t9f.jpg)

### 2.添加列表
“*+空格”或“-+空格”放于列表前，同一列表使用符号应统一，效果如下：
* 列表1
* 列表2
* 列表3

![](http://ww2.sinaimg.cn/mw690/a8fc9690gw1f7fp21twtnj20en02pgm1.jpg)

### 3.添加引用
“>”放于引用文字前，效果如下：
>引用1
>引用2
>引用3

![](http://ww2.sinaimg.cn/mw690/a8fc9690gw1f7fp4j23ngj206r02pglr.jpg)

### 4.文字加粗：在文字前后加符号“**”
**粗体**
### 5.文字斜体：在文字前后加符号“*”
*斜体*


### 插入链接:[显示的字] (对应的网址)
[百度](http://baidu.com)
![](http://ww4.sinaimg.cn/mw690/a8fc9690gw1f7fpdwjzb9j208k01caa7.jpg)

### 插入图片:![] (图片地址+空格+“图片标题”)
![](http://ww4.sinaimg.cn/mw690/a8fc9690gw1f7fpikdwlfj20fo01ejru.jpg)
这里直接用谷歌扩展程序微博图床生成

### 添加代码
添加一行代码：在代码前后添加符号“`”
添加多行代码：在每一行代码前都添加Tab或4个空格

	while(1){
		for(i=0;i<10;i++);
	}

### 引用方式
### 脚注
编辑.md文件可用sublime text3，安装Markdown Editing和Markdown Preview插件

本文参考：Markdown 语法说明(简体中文版).pdf
https://yunpan.cn/cMGfkIUtwmjV4  访问密码 581f