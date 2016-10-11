---
title: Quartus软件安装要点记录
date: 2016-09-06 22:13:43
tags:
categories:
---

![](http://ww4.sinaimg.cn/large/a8fc9690gw1f7k8tzta2hj20hs0dcmy9.jpg)


>此文暂不更新

<!-- more -->

[quartus系列软件下载地址](https://www.altera.com.cn/downloads/download-center.html)
想要以前版本的可上[altera官方ftp](ftp://ftp.altera.com/outgoing/release/)

windows7系统装Quartus II 11.0sp1 (64-Bit)

RedHat系统可安装QuartusSetup-16.0.0.211-linux.run，注意16版本支持器件不同，要先看看自己用什么规格的芯片，否则还得重新装
因此这里也装和win7相同版本的软件
```
chmod 755 QuartusSetup-16.0.0.211-linux.run
./QuartusSetup-16.0.0.211-linux.run
```

11.0sp1
在安装./11.0sp1_acds_linux.sh时，如果是远程登录，没有图形界面，如果顺利会出现
“altera_installer_gui: cannot connect to X server”提示出现问题，此时输入
export DISPLAY=:0.0
再进行安装./11.0sp1_acds_linux.sh
在受控电脑上有图形界面出现，按提示安装
[Linux下解决cannot connect to X server :0.0 问题](http://www.tuicool.com/articles/QJruE3)





13.0sp1
安装过程会出现很多依赖文件或者冲突文件，在配置好yum源情况下，除libz.so.1外，基本都可通过以下命令解决
rpm -e 包名 --nodeps（卸载）（可能不应该删除）
rpm -ivh 包全名
yum install -y 包名（安装）




软件安装后还需要设置环境变量，否则quartus命令无效

vi /etc/profile最下方添加
export  PATH="$PATH:（后面为绝对路径）/disk1/altera/13.0sp1/quartus/bin"

source /etc/profile更新增加环境变量
echo $PATH查看环境变量是否加上
任意敲入命令看是否识别，如quartus_sh，下图所示
![](http://ww1.sinaimg.cn/large/a8fc9690gw1f7mbvypr2gj20pu0be43e.jpg)

[Linux 下三种方式设置环境变量](http://www.linuxidc.com/Linux/2015-01/111459.htm)
[Linux环境变量的设置和查看方法](http://soft.chinabyte.com/os/169/11412169.shtml)



安装后影响到桌面环境，无法登陆图形界面！！！


quartus命令行手册
https://yunpan.cn/cMaApyAJ3UzTN  访问密码 9b3c

