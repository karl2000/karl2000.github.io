---
title: SourceInsight常用技巧整理
date: 2016-10-09 07:12:29
tags:
categories:
---

图片链接

>说明

<!-- more -->


恢复ctrl+a的全选功能
Options -> Key Assignments:通过关键词save 找到save all，更改为ctrl+shift+a，通过关键词select找到select all，更改为ctrl +a

设置背景色：	
Options->preference->color->windows background设置背景色（护眼色：“色调”的参数设置为85，“饱和度”参数设置为90，“亮度”参数设置为205）
附：豆沙绿的参数 RGB颜色 199；237；204 
十六位颜色代码 #C7EDCC 
色调：85；饱和度：123；亮度：205 




加载.s汇编文件并高亮显示
SourceInsight默认不识别.s文件，添加文件时会被忽略，一种方法是取消“show only known document types”,另一种是添加.s文件到C源文件中，让SourceInsight识别.s文件为C文件格式
![](http://ww2.sinaimg.cn/large/a8fc9690jw1f8mx75lnwej20g80e6mzx.jpg)
第二种方法操作：在Options->Document Options里面，点左上的Document Type下拉菜单，选择C Source File，然后在右边的File filter里补上*.s,*.S就可以像看C一样看汇编。





Source Insight常用快捷键
1. Ctrl + 鼠标单击 进入定义

2. Alt + F12可以切换，让字符宽度变得一致，或者是大小不同地显示

3. Shift + F8 标亮文本中光标所在的单词

4. Ctrl + G (或者F5) 跳转到某一行

5. Ctrl + O 搜索文件，找到回车打开，找不到ESC退出

6. Alt + G (或者F7) 打开Symbol Window

7. Alt +, 后退；Alt+.前进

8. Ctrl + F 查找关键字

9. Ctrl + Shift + F 工程内查找关键字
F3　：本文件查找结果的上一个
F4　：本文件查找结果的下一个
Ctrl+M　：创建或查找书签，方便下次找回此位置

Alt + , 返回上一窗口
Alt + . 前进到下一窗口