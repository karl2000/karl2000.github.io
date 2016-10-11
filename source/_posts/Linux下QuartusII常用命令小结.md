---
title: Linux下QuartusII常用命令小结
date: 2016-09-07 18:36:42
tags:
categories:
---

图片链接

>说明

<!-- more -->


Quartus II 命令行模式常用命令：

使用JTAG模式下载到FPGA上，使用命令：

quartus_pgm -c USB-Blaster -m jtag -o p;xxx.sof



单独打开GUI图形下载界面，使用命令：

quartus_pgmw



分析和综合（analysis & synthsis项目，使用命令：

quartus_map 项目名