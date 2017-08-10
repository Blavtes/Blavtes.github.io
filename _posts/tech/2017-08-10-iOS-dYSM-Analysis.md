---
layout: post
title: iOS异常捕获-堆栈信息的解析
category: 技术
tags: 异常捕获
description: iOS异常捕获-堆栈信息的解析
--- 

### 最近使用NSSetUncaughtExceptionHandler和signal方法捕获异常，并传到服务器，用来追踪线上app的异常信息。

但是捕获到的都是堆栈信息： 
异常堆栈信息

```
	test 		0x0000000100289a3c test + 2333244
	test 		0x0000000100219d5c test + 1875292
	test 	 	0x000000010022ae0c test + 1945100
	test		0x000000010022ad64 test + 1944932
	test		0x00000001002e3278 test + 2699896
	test		0x000000010022db80 test + 1956736 
```
如何利用这些堆栈信息查看报错方法名和行数？

# 异常信息

异常信息有三种类型：

1.已标记错误位置的:

	test 0x00000001002e3278 -[ViewController viewDidLoad] + 98

这种信息已经很明确了，不用解析

2.有模块地址的情况：

	test 0x000000010022db80 0x100064000 + 234234


以上面为例子，从左到右依次是： 
	
	二进制库名（test），调用方法的地址（0x000000010022db80），模块地址（0x100050000）+偏移地址（234234）

3.无模块地址的情况：
	test 0x000000010022db80 test + 234234

## dSYM符号表获取

	xcode->window->organizer->右键你的应用 show finder->右键.xcarchive 显示包内容->dSYMs->test.app.dYSM

## atos命令

atos命令来符号化某个特定模块加载地址

	atos [-arch 架构名] [-o 符号表] [-l 模块地址] [方法地址]

解析

# 使用终端，进到test.app.dYSM所在目录

### 一.如果是有模块地址的情况，运行：

	atos -arch arm64 -o test.app.dSYM/Contents/Resources/DWARF/test -l 0x100050000 0x000000010022db80

### 二.如果是无模块地址的情况

1.先将偏移地址转为16进制：

	2333244 = 0x239A3C

2.然后用方法的地址-偏移地址，得到的就是模块地址
	
	0x0000000100289a3c - 0x239A3C = 0x100050000

3.最后运行：

	atos -arch arm64 -o test.app.dSYM/Contents/Resources/DWARF/test -l 0x100050000 0x0000000100289a3c
	
	#main (in test) (main.m:38)