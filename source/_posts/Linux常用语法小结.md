---
title: Linux常用语法小结
date: 2016-09-05 22:47:00
tags:
categories:
---

![](http://ww1.sinaimg.cn/large/a8fc9690gw1f7k8vkx117j20zk0nj7i1.jpg)

>比较常用的linux命令

<!-- more -->


软件安装git(redhat)
yum install -y git 

rpm安装
rpm -ivh *.rpm



软件安装与卸载
-------------
apt-get
安装软件 apt-get install softname1 softname2 softname3……
卸载软件 apt-get remove softname1 softname2 softname3……
卸载并清除配置 apt-get remove -purge softname1
更新软件信息数据库 apt-get update
进行系统升级 apt-get upgrade
搜索软件包 apt-cache search softname1 softname2 softname3……
 
如果使用 apt-get 遇到速度慢或者源不存在等错误，可能需要更换源
dpkg 
安装deb软件包          dpkg -i xxx.deb
删除软件包             dpkg -r xxx.deb
连同配置文件一起删除   dpkg -r -purge xxx.deb
查看软件包信息         dpkg -info xxx.deb
查看文件拷贝详情       dpkg -L xxx.deb
查看系统中已安装软件包信息     dpkg -l
重新配置软件包         dpkg-reconfigure xxx

常用命令
apt-cache search         # ------(package 搜索包)
apt-cache show           #------(package 获取包的相关信息，如说明、大小、版本等)
sudo apt-get install     # ------(package 安装包)
sudo apt-get reinstall     # -----(package - - reinstall 重新安装包)
sudo apt-get -f install  # -----(强制安装?#"-f = --fix-missing"当是修复安装吧...)
sudo apt-get remove      #-----(package 删除包)
sudo apt-get remove --purge # ------(package 删除包，包括删除配置文件等)
sudo apt-get autoremove --purge # ----(package 删除包及其依赖的软件包+配置文件等（只对6.10有效，强烈推荐）)
 
sudo apt-get update      #------更新源信息数据库
sudo apt-get upgrade     #------更新已安装的包
sudo apt-get dist-upgrade # ---------升级系统
 
sudo apt-get dselect-upgrade #------使用 dselect 升级
apt-cache depends #-------(package 了解使用依赖)
apt-cache rdepends # ------(package 了解某个具体的依赖?#当是查看该包被哪些包依赖吧...)
sudo apt-get build-dep # ------(package 安装相关的编译环境)
apt-get source #------(package 下载该包的源代码)
sudo apt-get clean && sudo apt-get autoclean # --------清理下载文件的存档 && 只清理过时的包
sudo apt-get check #-------检查是否有损坏的依赖



tar压缩解压缩
tar -zcvf a.tar.gz a
tar -zxvf a.tar.gz

.tar.gz    格式解压为          tar   -zxvf   xx.tar.gz
.tar.bz2   格式解压为          tar   -jxvf    xx.tar.bz2
.tar.xz      xz -dk *.tar.xz  ->   tar -xvf  *.tar


tar -xf 可以解压.tar.xz和.tar.gz文件


删除文件
rm -rf 文件名



Linux的五个查找命令
------------
find <指定目录> <指定条件> <指定动作>
find . -name 'my*'

locate /etc/sh

whereis grep

which grep

type -p grep