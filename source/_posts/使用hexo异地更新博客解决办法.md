---
title: 使用hexo异地更新博客解决办法
date: 2016-09-03 11:58:38
tags: hexo
categories: 技术
---


>本文为解决异地更新博客问题，处理如何将文档托管于github上。

<!-- more -->

## 流程

1. 在github工程上创建branch分支hexo，该仓库创建时提示由master上复制过来
![](http://ww4.sinaimg.cn/large/a8fc9690gw1f7g9sros1ij20be0cdmyj.jpg)
2. 将默认分支设置成hexo，此处为git clone做准备
![](http://ww4.sinaimg.cn/large/a8fc9690gw1f7g9yjzanxj20rx0brjt5.jpg)
3. 在电脑上执行git clone命令，生成karl2000.github.io文件夹
`git clone git@github.com:karl2000/karl2000.github.io.git`
4. 删除文件夹所有内容，执行git add;git commit -m "说明";git push origin hexo命令（其中origin指代远程仓库，hexo为本地分支），将本地hexo分支（空文件夹）推送到远程origin，使得远程origin（默认分支hexo）更新为空目录。
5. 将之前的hexo工程文件夹的内容复制到karl2000.github.io文件夹
6. 在karl2000.github.io文件夹尝试使用hexo命令，出现提示输入npm install hexo --save
![](http://ww1.sinaimg.cn/large/a8fc9690gw1f7gaatsrbbj20ew01ldgd.jpg)
7. 运行命令npm install hexo-deployer-git --save，并使用hexo s命令检验工程是否完善
8. 执行git add .;git commit -m "说明";git push origin hexo命令，将工程文件推送到远程仓库origin/hexo下保存。