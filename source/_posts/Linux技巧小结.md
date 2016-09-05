---
title: Linux技巧小结
date: 2016-09-05 14:08:56
tags:
categories:
---

图片链接

>主要记录Linux使用过程遇到的需要处理的问题

<!-- more -->


* 修改IP永久生效
1. 切换到以下目录并打开编辑
vi /etc/sysconfig/network-scripts/ifcfg-eth0（eth0，第一块网卡，如果是第二块则为eth1）
2. 按如下修改ip
DEVICE=eth0（如果是第二块刚为eth1）
BOOTPROTO=static
IPADDR=192.168.0.11(改成要设置的IP)
NETMASK=255.255.255.0 (子网掩码)
GATEWAY=192.168.0.1(网关)
ONBOO=yes
3. 重启服务，通过ifconfig进行验证
service network restart

注：如果是临时修改IP重启系统后恢复原始IP则用以下命令
ifconfig IP地址 netmask 子网掩码



局域网内远程登录Linux系统
-------------------------
1. 安装SecureCRT软件
![](http://ww1.sinaimg.cn/large/a8fc9690gw1f7ippub25vj20g408jtas.jpg)
2. 查询本机正在使用的网卡IP地址
`win+R;cmd;ipconfig`
结果为“192.168.1.100”
![](http://ww1.sinaimg.cn/large/a8fc9690gw1f7ipryt5yyj20ff03mdgb.jpg)
3. 查询远端Linux系统IP地址
`ifconfig`
结果一定也在同一网段内，示例的结果是“192.168.1.108”
4. 通过SecureCRT新建连接并设置
![](http://ww3.sinaimg.cn/large/a8fc9690gw1f7ipx8k56gj20f40bw0v1.jpg)

注：同一台电脑通过VMware设置介绍，网络设置界面说明如下；
![](http://ww3.sinaimg.cn/large/a8fc9690gw1f7ipzjlxmyj20jy0bndid.jpg)
>桥接模式：直接用真实网卡与虚拟机通信，需占用局域网内的IP地址
>NAT模式：通过虚拟网卡VMnet8通信，只能与当前电脑通信，可以访问互联网
>仅主机模式：通过虚拟网卡VMnet8通信，只能与当前电脑通信，不能访问互联网

[Redhat 7.0使用CentOS 7 的Yum 网络源](http://www.centoscn.com/CentOS/config/2015/0328/5030.html)
-----------------------------------

