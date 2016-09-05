---
title: RedHat系统安装问题解决
date: 2016-09-05 09:59:32
tags:
categories:
---

![](http://ww1.sinaimg.cn/large/a8fc9690gw1f7ijg6946lj21hc0zkk1d.jpg)

>RedHat系列（包括CentOS）系统在使用实际电脑安装时，出现“dev/root does not exist”的解决办法。

<!-- more -->

在笔记本上安装纯Linux操作系统时出现如下错误：
![](http://ww1.sinaimg.cn/large/a8fc9690gw1f7iiwr0zkaj20zk0k078n.jpg)

经过上面的步骤，本应进入RedHat的安装界面。但实际上未能进入，而是出现了类似上图的
```
dracut-initqueue[624]:Warning: Could not boot.
dracut-initqueue[624]:Warning: /dev/root does not exist.Starting Dracut EmergencyShell…
Warning: /dev/root does not exist
```
该问题是由于安装程序未能找到安装文件所致。
可以在随后出现的 `dracut:/#` 输入命令 `find / -name RHEL*`(即在根目录下搜索RHEL开头的文件，本例装的是RedHat系统，CentOS可以搜CentOS*)，找到安装文件所在的位置，即`/dev/disk/by-labelRHEL-7.0\x20se`（即指向U盘的位置）,
重启后修改(在启动引导的地方输入 Tab（CentOS为输入e，界面有提示）进入编辑状态)启动配置，将
`vmlinuz initrd=initrd.imginst.stage2=hd:LABEL=RHEL-7.0\x20se****** quiet 改为：`
`vmlinuz initrd=initrd.imginst.stage2=hd:LABEL=RHEL-7.0\x20se       quiet`
这是由于文件名太长，导致识别错误，从而找不到文件。
