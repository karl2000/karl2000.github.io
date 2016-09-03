---
title: git常用语法小结
date: 2016-09-03 02:48:04
tags:
categories:
---

![](http://ww4.sinaimg.cn/large/a8fc9690gw1f7gvpotmqmj21kw16oe2m.jpg)


>本文对git常用语法进行小结，持续更新中。

<!-- more -->

## 概念
工作区
暂存区
本地仓库
远程仓库


## 语法

### 基本操作
* 初始化文件夹
git init
* 保存到暂存区
git add .（保存文件夹所有文件，也可以指定特定文件）
* 提交到本地仓库master
git commit -m "提交说明"
* 查看本地仓库与工作区是否有更改
git status
* 查看更改内容
git diff
* 查看历史记录
git log （--pretty=oneline可加）
* 记录每一次操作
git reflog
* 退回上一版本
git reset --hard HEAD^（HEAD表示当前版本）
* 退回某一版本
git reset --hard b97fa9d（版本编号）
* 关联远程库
git remote add origin + (github上复制的地址)
* 把当前分支master推送到远程库origin（origin为上面关联的库）
git push （-u首次推送） origin master
* 复制远程库，拷贝项目文件夹，不需要另外新建文件夹，后续cd到该文件夹进行操作
git clone + (github上复制的地址)

### 分支操作
* 查看当前分支情况
git branch
* 创建dev分支
git branch dev
* 切换到dev分支
git checkout dev
* 创建并切换到dev分支
git checkout -b dev
* 合并dev分支到当前分支(fast-forward)
git merge dev
* 删除dev分支
git branch -d dev




---

* 查看分支合并情况
git log --graph --pretty=oneline --abbrev-commit
* 比较工作区和版本的区别
git diff HEAD -- readme.txt
* 撤销工作区的修改
git checkout -- readme.txt
* 撤销暂存区的修改
git reset (--hard可有) HEAD readme.txt
* 删除暂存区和工作区文件
git rm test.txt

参考文件：
https://yunpan.cn/cMbGQdJpfmRvc  访问密码 b04e
https://yunpan.cn/cMbGdpRMmCSdt  访问密码 6823





