---
title: Linux技巧小结
date: 2016-09-05 14:08:56
tags:
categories:
---

![](http://ww1.sinaimg.cn/large/a8fc9690gw1f7k8uyjhqrj20hs0dxgoy.jpg)

>主要记录Linux使用过程遇到的需要处理的问题

<!-- more -->


修改IP永久生效
--------------
1. 切换到以下目录并打开编辑
vi /etc/sysconfig/network-scripts/ifcfg-eth0（eth0，第一块网卡，如果是第二块则为eth1）
2. 按如下修改ip
DEVICE=eth0（如果是第二块刚为eth1）
BOOTPROTO=static
IPADDR=192.168.1.115(改成要设置的IP)
NETMASK=255.255.255.0 (子网掩码)
GATEWAY=192.168.1.1(网关)
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
1. 删除原yum包
`rpm -qa|grep yum|xargs rpm -e --nodeps`删除软件用该命令
2. 电脑可上网
3. 下载CentOS可用yum包并安装
4. 修改repo文件
>注：要将下载的repo文件内"$releasever"替换为相应版本号，去yum源核对路径，否则还会提示“This system is not registered to Red Hat Subscription Management”错误。
5. 测试，yum install -y gcc;yum install -y gcc-c++


[linux查看内核版本、系统版本、系统位数（32or64）](http://nameyjj.blog.51cto.com/788669/557424)





[安装linux下的ShadowSocks](https://github.com/shadowsocks/shadowsocks-qt5/wiki)
-------------------------------------------------------------------------------
以下方法可安装成功，但是桌面系统受影响，进不了图形界面（正在处理）:
```
如果使用传统的yum包管理工具的话，需要从Copr下载相应版本的repo文件放到/etc/yum.repos.d/下，然后通过yum安装：
sudo yum update

sudo yum install shadowsocks-qt5
RHEL/CentOS请确认已经添加了EPEL源。
```

[chrome浏览器安装](https://www.google.com/chrome/browser/desktop/index.html)
-------------------------------------------------------------------------------

[chromium浏览器安装](https://pkgs.org/centos-7/epel-testing-x86_64/chromium-52.0.2743.116-11.el7.x86_64.rpm.html)
-------------------------------------------------------------------------------





RedHat软件安装小结
------------------
1. 安装包名.rpm
rpm -ivh 安装包名.rpm
yum install -y 安装包名(安装yum源有的软件)
2. 安装包名.run
```
chmod 755 安装包名.run
./安装包名.run(直接安装)
```
>在终端中转到run文件所在的文件夹，执行  chmod +x ./文件.run  以赋予其可执行权限，最后输入  ./文件.run  执行文件，按所给的提示进行安装。
如果遇到赋予可执行权限后依旧无法执行的情况，可能是因为该run文件处于FAT或NTFS格式的磁盘分区中，不可直接对其赋值，最好的办法是将其移动至ext4的Linux分区中再赋值执行。FAT不支持POSIX权限，在NTFS分区中可使用  ntfs-config  软件赋予其可执行权限。

3. iso文件

>如果拷贝到本地，可以使用mount 
mount fileName mountPoint -o loop，fileName是镜像文件名(*.iso,*.img)， 
用例：如我有一个/home/rhel5.2.iso光盘镜像文件， 
mkdir /mnt/b 
mount /home/rhel5.2.iso /mnt/b -o loop，这样进入目录/mnt/b 你就能浏览rhel5.2.iso的内容了，*.img文件的用法一样。 



4. 源码包
```
./configure
make
make install
```
5.脚本安装包

`./*.sh`



Ctrl+Alt+F?(?为数字)：linux切换tty






Ubuntu增加SWAP分区大小【转】
----------------------
Swap分区，即交换区
    Swap空间的作用可简单描述为：当系统的物理内存不够用的时候，就需要将物理内存中的一部分空间释放出来，以供当前运行的程序使用，那些被释放的空间可能来自一些很长时间没有什么操作的程序，这些被释放的空间被临时保存到Swap空间中，等到那些程序要运行时，再从Swap中恢复保存的数据到内存中。这样，系统总是在物理内存不够时，才进行Swap交换。 
    通常情况下，Swap空间应大于或等于物理内存的大小，最小不应小于64M，通常Swap空间的大小应是物理内存的2-2.5倍，Swap的调整对Linux服务器，特别是Web服务器的性能至关重要，通过调整Swap，有时可以越过系统性能瓶颈，节省系统升级费用。

一、查看已有swap空间
[root@test ~]# free -m
             total       used       free     shared    buffers     cached
Mem:          3949        244       3704          0         18        157
-/+ buffers/cache:         69       3880
Swap:         4275          0       4275

二、新增swap分区空间
1、使用dd创建swapfile，bs单位bytes，也可以手动指定单位为M或者G，count为计数，例子为增加1M*1024=1G空间
[root@test swap]#pwd
/swap
[root@test swap]# dd if=/dev/zero of=swapfile bs=1M count=1024
1024+0 records in
1024+0 records out
1073741824 bytes (1.1 GB) copied, 2.27273 seconds, 472 MB/s
[root@test swap]# ll
total 1049604
-rw-r--r-- 1 root root 1073741824 Sep 16 20:48 swapfile

2、mkswap创建交换文件
[root@test swap]# mkswap swapfile 
Setting up swapspace version 1, size = 1073737 kB

3、swapon激活
[root@test swap]# swapon swapfile 

4、查看增加后swap空间
[root@test swap]# free -m
             total       used       free     shared    buffers     cached
Mem:          3949       1293       2655          0         17       1181
-/+ buffers/cache:         95       3854
Swap:         5299          0       5299

5、开机启动
vim /etc/fstab 添加
/swap/swapfile         swap                    swap    defaults        0 0

6、去掉增加swap
# 查看
[root@test swap]# free -m
# 停用
[root@test swap]# swapoff swapfile
# 删除
[root@test swap]# rm swapfile -rf
# 确定
[root@test swap]# free -m
# 删除随即启动swap
[root@test swap]# vim /etc/fstab


扩展阅读（来自百度百科）：
    需要说明一点，并不是所有从物理内存中交换出来的数据都会被放到Swap中（如果这样的话，Swap就会不堪重负），有相当一部分数据被直接交换到文件系统。例如，有的程序会打开一些文件，对文件进行读写（其实每个程序都至少要打开一个文件，那就是运行程序本身），当需要将这些程序的内存空间交换出去时，就没有必要将文件部分的数据放到Swap空间中了，而可以直接将其放到文件里去。如果是读文件操作，那么内存数据被直接释放，不需要交换出来，因为下次需要时，可直接从文件系统恢复；如果是写文件，只需要将变化的数据保存到文件中，以便恢复。但是那些用malloc和new函数生成的对象的数据则不同，它们需要Swap空间，因为它们在文件系统中没有相应的“储备”文件，因此被称作“匿名”(Anonymous)内存数据。这类数据还包括堆栈中的一些状态和变量数据等。所以说，Swap空间是“匿名”数据的交换空间。


如何查找Linux内核代码【转】
-----------------
先登录网站  http://lxr.linux.no/
选择你需要查看的内核版本，LINUX 可以通过“uname -r”来获得这个版本号。 

然后就是找你需要的东东啦，如果你知道目录结构可以直接去打开目录，个人觉得还是根据函数名称搜索来的比较靠谱。 

比如要寻找SK_BUFF定义，直接输入，然后找STRUCTURE 
就可以找到 
http://lxr.linux.no/linux+v2.6.32.20/include/linux/skbuff.h#L313



bash快捷键
----
ctrl键组合
ctrl+a:光标移到行首。
ctrl+b:光标左移一个字母
ctrl+c:杀死当前进程。
ctrl+d:退出当前 Shell。
ctrl+e:光标移到行尾。
ctrl+h:删除光标前一个字符，同 backspace 键相同。
ctrl+k:清除光标后至行尾的内容。
ctrl+l:清屏，相当于clear。
ctrl+r:搜索之前打过的命令。会有一个提示，根据你输入的关键字进行搜索bash的history
ctrl+u: 清除光标前至行首间的所有内容。
ctrl+w: 移除光标前的一个单词
ctrl+t: 交换光标位置前的两个字符
ctrl+y: 粘贴或者恢复上次的删除
ctrl+d: 删除光标所在字母;注意和backspace以及ctrl+h的区别，这2个是删除光标前的字符
ctrl+f: 光标右移
ctrl+z : 把当前进程转到后台运行，使用’ fg ‘命令恢复。比如top -d1 然后ctrl+z ，到后台，然后fg,重新恢复
esc组合
esc+d: 删除光标后的一个词
esc+f: 往右跳一个词
esc+b: 往左跳一个词
esc+t: 交换光标位置前的两个单词。









