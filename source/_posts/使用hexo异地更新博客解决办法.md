---
title: 使用hexo异地更新博客解决办法（Windows）
date: 2016-09-03 11:58:38
tags: hexo
categories: 技术
---
![](http://ww4.sinaimg.cn/large/a8fc9690gw1f7he0wwox9j21hc0zk4qp.jpg)

>本文为解决hexo异地更新博客问题，处理如何将文档托管于github上，要求有通过hexo+github搭建的个人博客。
适用于已经通过hexo搭建好博客，希望通过git对版本进行控制的。

<!-- more -->

## 流程

在已有的github远程库上创建branch分支hexo，该仓库创建时提示由master上复制过来
![](http://ww4.sinaimg.cn/large/a8fc9690gw1f7g9sros1ij20be0cdmyj.jpg)

---

在博客文件夹git操作：git init;git add .;git commit -m "说明";实现文件夹的版本控制

关联远程库：git remote add origin + 远程库地址

创建分支hexo，分支名字与远程库分支名相同，两者是一一对应的：git branch hexo

将本地hexo分支push到远程，确保博客源文件正确：git push origin master

---

在另一台电脑上对文件夹进行hexo初始化：hexo init（过程中有问题请参考本博客其他博文）



对该文件夹进行git初始化：git init

关联远程库：git remote add origin + 远程库地址

在该文件夹下执行git add .;git commit -m "说明";目的在于确定一个master分支的版本

在该文件夹下创建并切换hexo分支：git checkout -b hexo
pull远程库hexo到本地分支hexo：git pull origin hexo
对冲突文件进行修改，主要修改_config.yml，package.json，删除hello-world.md，然后commit提交hexo版本：git add .;git commit -m "说明" 

---

于是，在新的文件夹下也可以更新博客了。
