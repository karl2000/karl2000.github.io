---
title: Cpp深入详解学习总结
date: 2016-09-22 09:15:41
tags:
categories:
---

![](http://ww3.sinaimg.cn/large/a8fc9690jw1f8kzmqjshnj20zk0q7whz.jpg)

>本文为Cpp深入详解的学习笔记

<!-- more -->

第一章 Windows程序内部运行机制
------
主要介绍如何创建Win32的应用程序步骤：
1. 编写WinMain函数，可以在MSDN上查找并复制。
2. 设计窗口类（WNDCLASS）
3. 注册窗口类（RegisterClass）
4. 创建窗口（HWND，CreateWindow）
5. 显示并更新窗口（ShowWindow，UpdateWindow）
6. 编写消息循环（MSG，TranslateMessage，DispatchMessage）
7. 编写窗口过程函数，窗口过程函数的语法可通过MSDN查看WNDCLASS的lpfnWndProc成员变量解释中查到
```
LRESULT CALLBACK WindowProc(	//回调函数定义，WindowProc为自定义
	HWND hwnd,      // handle to window
	UINT uMsg,      // message identifier
	WPARAM wParam,  // first message parameter
	LPARAM lParam   // second message parameter
);

```
示例程序如下：
```
#include <windows.h>
#include <stdio.h>

LRESULT CALLBACK WinSunProc(
  HWND hwnd,      // handle to window
  UINT uMsg,      // message identifier
  WPARAM wParam,  // first message parameter
  LPARAM lParam   // second message parameter
);

int WINAPI WinMain(
  HINSTANCE hInstance,      // handle to current instance
  HINSTANCE hPrevInstance,  // handle to previous instance
  LPSTR lpCmdLine,          // command line
  int nCmdShow              // show state
)
{
	WNDCLASS wndcls;
	wndcls.cbClsExtra=0;
	wndcls.cbWndExtra=0;
	wndcls.hbrBackground=(HBRUSH)GetStockObject(BLACK_BRUSH);
	wndcls.hCursor=LoadCursor(NULL,IDC_CROSS);
	wndcls.hIcon=LoadIcon(NULL,IDI_ERROR);
	wndcls.hInstance=hInstance;
	wndcls.lpfnWndProc=WinSunProc;
	wndcls.lpszClassName="Weixin2003";
	wndcls.lpszMenuName=NULL;
	wndcls.style=CS_HREDRAW | CS_VREDRAW;
	RegisterClass(&wndcls);

	HWND hwnd;
	hwnd=CreateWindow("Weixin2003","北京维新科学技术培训中心",WS_OVERLAPPEDWINDOW,
		0,0,600,400,NULL,NULL,hInstance,NULL);

	ShowWindow(hwnd,SW_SHOWNORMAL);
	UpdateWindow(hwnd);

	MSG msg;
	while(GetMessage(&msg,NULL,0,0))
	{
		TranslateMessage(&msg);
		DispatchMessage(&msg);
	}
	return 0;
}

LRESULT CALLBACK WinSunProc(
  HWND hwnd,      // handle to window
  UINT uMsg,      // message identifier
  WPARAM wParam,  // first message parameter
  LPARAM lParam   // second message parameter
)
{
	switch(uMsg)
	{
	case WM_CHAR:
		char szChar[20];
		sprintf(szChar,"char is %d",wParam);
		MessageBox(hwnd,szChar,"weixin",0);
		break;
	case WM_LBUTTONDOWN:
		MessageBox(hwnd,"mouse clicked","weixin",0);
		HDC hdc;
		hdc=GetDC(hwnd);
		TextOut(hdc,0,50,"计算机编程语言培训",strlen("计算机编程语言培训"));
		ReleaseDC(hwnd,hdc);
		break;
	case WM_PAINT:
		HDC hDC;
		PAINTSTRUCT ps;
		hDC=BeginPaint(hwnd,&ps);
		TextOut(hDC,0,0,"维新培训",strlen("维新培训"));
		EndPaint(hwnd,&ps);
		break;
	case WM_CLOSE:
		if(IDYES==MessageBox(hwnd,"是否真的结束？","weixin",MB_YESNO))
		{
			DestroyWindow(hwnd);
		}
		break;
	case WM_DESTROY:
		PostQuitMessage(0);
		break;
	default:
		return DefWindowProc(hwnd,uMsg,wParam,lParam);
	}
	return 0;
}
```



第二章 掌握C++
------

封装性，继承性，多态性
基本输入输出头文件#include <iostream.h>(C语言为#include <stdio.h>)

结构体
c中结构体内不允许有函数，Cpp可以

构造函数：
1.自动调用
2.与类同名
3.没有返回值
4.有多个重载形式
5.无定义会自动生成，但不初始化

构造函数：带参数不带参数都可以，可以有多个
```
Point()
{
	x=0;
	y=0;
}
Point(int a,int b)
{
	x=a;
	y=b;
}
```
析构函数：不能带参数，没有返回值，只能有一个
```
~Point()
{
}
```
函数重载：发生在一个类中，不同参数类型或个数才能构成重载（区别于发生于父类和子类的函数覆盖）
函数覆盖的条件：
1. 父类函数必须是虚函数，用virtual关键字声明
2. 发生在父类与子类之间
3. 函数名与参数必须完全相同

函数隐藏的两种情况：
1. 子类与父类函数名和参数完全相同，只是父类没用virtual关键字
2. 子类与父类函数名相同，参数不同，不管有没有用virtual，都是隐藏

>覆盖就是看不见，隐藏就是通过类名::函数名可以访问到。如果基类被重写的函数是虚函数的话就是覆盖，否则就是隐藏。


this指针，指向对象本身，每个生成的对象都会有一个this指针指向本身

基类，派生类
```
class Fish : public Animal  //Animal基类，Fish派生类
{
public:
	
};
```
public:都可访问
protected:子类可访问
private:只能在类中访问


对函数参数进行初始化，可用如下方法：
```
Fish():Animal(300,400)    //子类向父类带参数的构造函数传递参数
point():x(0),y(0)    //常数初始化
```
双冒号为作用域标识符，表示函数属于哪个类，如果之前没有类名则为全局函数
```
Animal::sleep()
::ShowWindow();//全局函数
```

父类对象与子类对象的首地址是一样的
![](http://ww2.sinaimg.cn/large/a8fc9690gw1f82dntv0kbj20en07a74q.jpg)

多态性：子类有的调用子类，子类没有的调用父类
虚函数virtual：在h文件中加，当函数实现放到c文件中不加virtual
纯虚函数virtual void breathe()=0;必须要实现纯虚函数功能才能实例化对象

引用int &b=a;    //b为变量a的别名，引用必须初始化，指针则不一定要初始化

编译链接：编译单独的c文件生成.obj，然后链接生成.exe，h文件通过c文件中的包含直接加到c文件中（预处理）

第三章 MFC框架程序剖析
--------
按照第一章流程分析



第七章 对话框
----------

对话框创建
>模态对话框：需关闭才可执行其他任务
>非模态对话框

在MFC中，对资源的操作通常都是通过一个与资源相关的类来完成的


在resource选项卡中添加DIALOG，布置相应资源；
创建类，可以View->ClassWizard创建，也可以双击创建，类名一般C开头


if函数括号内可以逗号表达式，整个判断值为逗号后面的表达式值
`if(GetDlgItem(IDC_NUMBER1)->GetWindowText(str),str=="Number1:")`


七种访问对话框控件方式：
**GetDlgItem()->Get(Set)WindowText()**
GetDlgItemText()/SetDlgItemText()
GetDlgItemInt()/SetDlgItemInt()
**将控件和整型变量相关联**
**将控件和控件变量相关联**
SendMessage()
SendDlgItemMessage()

