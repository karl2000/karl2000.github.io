---
title: Ubuntu使用问题解决
date: 2016-09-25 09:15:41
tags:
categories:
---

![](http://ww2.sinaimg.cn/large/a8fc9690gw1f8kzx4iykpj21hc0zk1i4.jpg)

>使用过程中遇到的问题

<!-- more -->



SSH远程登录
-----------

1. 更新源列表`sudo apt-get update`
2. 安装SSH`sudo apt-get install openssh-server`
3. 查看SSH是否启动：打开"终端窗口"，输入"sudo ps -e |grep ssh"-->回车-->有sshd,说明ssh服务已经启动，如果没有启动，输入"sudo service ssh start"-->回车-->ssh服务就会启动
4. 使用gedit修改配置文件"/etc/ssh/sshd_config"
打开"终端窗口"，输入"sudo gedit /etc/ssh/sshd_config"-->回车-->把配置文件中的"PermitRootLogin without-password"改为“PermitRootLogin yes”,把它注释掉-->再增加一句"PermitRootLogin yes"-->保存，修改成功。
