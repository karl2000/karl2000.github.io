
---
title: LFS（linux from scratch）搭建手记
date: 2016-09-28 09:16:25
tags:
categories:
---

![](http://ww2.sinaimg.cn/large/a8fc9690jw1f8kzroan1uj21hc0zkh23.jpg)

>根据LFS-BOOK-7.7-systemd.pdf进行搭建

<!-- more -->




第二章 准备新分区
--------
创建新分区，格式化并挂载到/mnt/lfs

设置环境变量
export LFS=/mnt/lfs
确保一直设置了  LFS  变量的一个方法是，同时编辑你的主目录下的.bash_profile 和  /root/.bash_profile ，把上方的导出命令输入进去。

第三章 软件包与补丁
---------------
`mkdir -v $LFS/sources` 该文件夹保存软件包和补丁，同时作为工作目录

`chmod -v a+wt $LFS/sources`打开写权限和粘滞模式

下载所有软件包和补丁的一个简单方式:
`wget --input-file=wget-list --continue --directory-prefix=$LFS/sources`


下载所有软件包和补丁，将md5sums拷入source目录，校验下载的文件是否正确
```
pushd $LFS/sources
md5sum -c md5sums
popd
```


第四章 最后的准备工作
------------------------

创建tools文件夹
`mkdir -v $LFS/tools`

su命令和su -命令最大的本质区别就是：前者只是切换了root身份，但Shell环境仍然是普通用户的Shell；而后者连用户和Shell环境一起切换成root身份了。只有切换了Shell环境才不会出现PATH环境变量错误。su切换成root用户以后，pwd一下，发现工作目录仍然是普通用户的工作目录；而用su -命令切换以后，工作目录变成root的工作目录了。用echo $PATH命令看一下su和su -以后的环境变量有何不同。以此类推，要从当前用户切换到其它用户也一样，应该使用su -命令。


第五章 构建临时系统
--------------

安装前确认宿主系统需求软件已安装(在软件要求的版本较低的情况下，降低软件版本的方法是将源指定到之前的版本，然后重新卸载安装软件)
备份源列表
sudo cp /etc/apt/sources.list /etc/apt/sources.list_backup
修改源后更新sudo apt-get update
`dpkg -l binutils`查看binutils软件版本



Binutils 软件包包括了一个链接器、汇编器和其它处理目标文件的工具。

GCC 软件包是 GNU 编译器集合的一部分，其中包括 C 和 C++ 的编译器。
在编译GCC时如果出现“Makefile:xxx: recipe for target xxx failed”，可能是swap分区太小，需要增加其大小



Ubuntu下缺省使用的是shell是dash，而不是bash。从/bin/sh软连接的指向可以看出这点。
```
root@ubuntu:/# ls -l /bin/sh
lrwxrwxrwx 1 root root 4 Sep 25 12:30 /bin/sh -> dash
```
`ln -sf /bin/bash /bin/sh`：/bin/sh是指向/bin/bash的软链接


5.11后软件安装直接看PDF即可



第六章 安装基本的系统软件
------------------------

基本都是安装PDF直接进行安装操作，比较费时，一步步来即可，注意有些指令从PDF直接复制是有问题的。


第七章 基本系统配置
-------------------

7.2通用网络配置
cat > /etc/resolv.conf << "EOF"
# Begin /etc/resolv.conf
#domain <Your Domain Name>
nameserver  8.8.8.8
#nameserver 114.114.114.114
# End /etc/resolv.conf
EOF

7.7系统区域设置

`locale -a`获取本地字符集
`LC_ALL=zh_CN.utf8  locale charmap` 获取规范名称UTF-8
`LC_ALL=zh_CN.utf8 locale language`获取规范名称Chinese
`LC_ALL=zh_CN.utf8 locale int_curr_symbol`获取规范名称CNY
`LC_ALL=zh_CN.utf8 locale int_prefix`获取规范名称86






第八章 让LFS系统可引导
----------------------
cat > /etc/fstab << "EOF"
# Begin /etc/fstab
#  文件系统    挂载点    文件类型       挂载选项              dump  fsck
#                                                              order
/dev/sdb1     /mnt/lfs             ext4    defaults            1     1
#/dev/<yyy>     swap         swap     pri=1               0     0
# End /etc/fstab
EOF

8.3安装内核


输入`make LANG=zh_CN.utf8 LC_ALL= menuconfig`后出现设置界面
![](http://ww2.sinaimg.cn/large/a8fc9690jw1f8cm9yblcoj20tj0fpqan.jpg)
根据PDF进行设置，命令见图片上部，注意选择用'y'，取消用'n'

8.4创建grub配置文件（虚拟机sdb1）

cat > /boot/grub/grub.cfg << "EOF"
# Begin /boot/grub/grub.cfg
set default=0
set timeout=5
insmod ext2
set root=(hd1,1)
menuentry "GNU/Linux, Linux 3.19-lfs-7.7-systemd" {
        linux   /boot/vmlinuz-3.19-lfs-7.7-systemd root=/dev/sdb1 ro
}
EOF

要让系统可引导，可以在宿主机Ubuntu的grub.cfg中添加如下代码，启动时就会出现相应菜单：
```
### BEGIN /etc/grub.d/40_custom ###
# This file provides an easy way to add custom menu entries.  Simply type the
# menu entries you want to add after this comment.  Be careful not to change
# the 'exec tail' line above.
menuentry "LFS on (/dev/sdb1)" {
#       savedefault
#       gfxpayload=1280x1024x32,1280x1024
        set root=(hd1,1)
        linux  /boot/vmlinuz-3.19-lfs-7.7-systemd root=/dev/sdb1 ro
}
### END /etc/grub.d/40_custom ###

```



