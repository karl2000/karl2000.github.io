---
title: github+hexo搭建免费个人博客（Windows）正在更新……
date: 2016-09-01 21:14:34
tags:
---


## 前言

出于工作、兴趣、分享等各种原因，很多人想搭建自己的一个博客，本文将介绍如何利用github+hexo搭建免费的个人博客。


## 主要步骤

1.安装node.js，用于生成静态页面（node-v0.12.3-x64.msi）
2.安装git，将本地hexo内容提交到github上去（msysgit为windows版本，Git-2.5.1-64-bit.exe）
3.申请github账号，作为博客的远程仓库，免费挂在网上提供访问的，配置好SSH Keys之后提交不需再手动输入账号密码，检查是否有ssh keys（cd ~/.ssh若提示No such file or directory则要生成）
  设置用户信息命令
                   git config --global user.name "karl2000"//用户名
  				   git config --global user.name "karl2000@qq.com"//邮箱
4.安装hexo（npm install -g hexo-cli）
5.初始化文件夹（hexo init）

6.运行命令npm install hexo-deployer-git --save
避免出现如下错误提示
ERROR Deployer not found : github


7.清除缓存文件 (db.json) 和已生成的静态文件 (public)。（hexo clean，本机调试时可不用）
8.生成静态页面（hexo generate或者hexo g）
9.本地启动（hexo server或者hexo s）
10.部署（hexo deploy或者hexo d）

11.新建博客（hexo new 标题或者hexo n 标题）

步骤1-4只配置一次即可，以后操作只需后面的步骤。


更改主题，
可到https://hexo.io/themes/搜索合适的主题
复制下载主题git clone https://github.com/tufu9441/maupassant-hexo.git themes/maupassant
安装渲染器（==）
npm install hexo-renderer-jade --save
npm install hexo-renderer-sass --save

hexo使用参考官方教程https://hexo.io/zh-cn/


github下载他人的博客样本，git clone git@github.com:xhay1122/xhayblog-next.git BLOG/xhayblgo
直接下载似乎无法使用

经验：
1.如果修改_config.yml过程中出现一堆乱码，很有可能在冒号后面没有加空格引起
2.公益404网页无法显示解决办法：使用独立域名

## 绑定域名

