---
title: Linux教程笔记
date: 2016-09-07 10:17:40
tags:
categories:
---

![](http://ww2.sinaimg.cn/large/a8fc9690jw1f8kztqud1jj21hc0zk492.jpg)

>对兄弟连视频教程的一个归纳

<!-- more -->



9. 文件系统管理
9.1
分区：主分区总共4个，扩展分区1个（占用主分区数量），逻辑分区不限（在扩展分区中）
硬盘硬件接口：
IDE（淘汰hda）
SCSI(sda1,sda2,sda5（扩展分区）等)
9.2
df -h；查看分区情况
du -sh 目录名：统计目录大小
dumpe2fs /dev/sda1：看详细信息
挂载
建立挂载点 mkdir /mnt/cdrom
挂载命令`mount [-t 文件系统（iso9660/vfat）] [-o 特殊选项] 设备文件名（dev/cdrom） 挂载点（mnt/cdrom)`
卸载 umount 设备文件名或挂载点（/mnt/cdrom或/dev/cdrom）

fdisk -l :查看有多少可被识别的硬盘或优盘
lsblk:查看系统硬盘结构，更直观


9.3
fdisk /dev/sdb(对新硬盘进行分区)
(参数n新建,d删除,t更改分区，l查看类型83为linux，5为extended，82为swap，最后记得w)
partprobe重新读取分区表信息
mkfs -t ext4 /dev/sdb1(格式化，格式化swap分区用mkswap /dev/sdb1,swapon /dev/sdb1加入，swapoff /dev/sdb1取消  )
分区自动挂载要修改/etc/fstab
（swap要这么写：/dev/sdb1    swap    swap  defaults  0  0）
(编写过程可能用到的指令dumpe2fs -h /dev/sdb1，fdisk -l，mount，df)
修改好文件后需测试文件是否错误(一定不能错)
mount -a

实例：
1. VMware新建虚拟盘（实际电脑直接挂载新硬盘），基本按照默认设置，磁盘大小自定义，这里设置为10G
![](http://ww2.sinaimg.cn/large/a8fc9690gw1f88yt247frj20nx0idq6e.jpg)
2. `fdisk -l`查看新挂载磁盘，这里为/dev/sdb
![](http://ww4.sinaimg.cn/large/a8fc9690gw1f88yvoo2jhj20n405ugov.jpg)
3. `fdisk /dev/sdb`对新磁盘进行分区（命令见上文，这里n->p->一直enter->最后w，新建一个10G主分区）
![](http://ww3.sinaimg.cn/large/a8fc9690gw1f88yzzp29hj20o605mad3.jpg)
![](http://ww1.sinaimg.cn/large/a8fc9690gw1f88z0jkiqdj20fo02p0tg.jpg)
4. `partprobe`重新读取分区表信息
5. `mkfs -t ext4 /dev/sdb1`格式化新分区
![](http://ww2.sinaimg.cn/large/a8fc9690gw1f88z1s4lavj20lr062tc8.jpg)
6. 自动加载
`dumpe2fs -h /dev/sdb1`:查看sdb1的UUID
![](http://ww3.sinaimg.cn/large/a8fc9690gw1f88zqdqpg5j20kr03l0uu.jpg)
`vi /etc/fstab`修改启动配置文件
`UUID=a63472f7-55d3-4ab1-92cb-159872bb81b3 /               ext4    defaults        0       0`
![](http://ww3.sinaimg.cn/large/a8fc9690gw1f88zs2jvk6j20tv07dn2o.jpg)
7. 检查修改是否有问题
`mount -a`
9.4
free -m 查询swap分区使用情况