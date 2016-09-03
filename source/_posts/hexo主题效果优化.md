---
title: hexo主题效果优化
date: 2016-09-04 01:24:56
tags:
categories:
---



>为改善阅读体验，需对主题部分功能进行完善。

<!-- more -->


* 隐藏全文，增加阅读全文效果
在.md文件中需要隐藏部分前增加代码`<!-- more -->`
* 代码黑底白字，高亮显示
在主题_config.yml文件中设置highlight_theme: night，效果如下：
![](http://ww4.sinaimg.cn/large/a8fc9690gw1f7gx4ncjwej20kj06aaax.jpg)

* 添加背景图片
首先找到一个背景图片放到 hexo（hexo工程文件）-> themes -> next -> source -> images 的路径下；
hexo（hexo工程文件）-> themes -> next -> source -> css -> _schemes -> Pisces（Mist和Muse也行），找到路径下的index.styl文件，在文件的最上方加上一代码 body { background:url(/images/backGround.jpg（这是你之前加的背景图片的名字）);} 就完事了。