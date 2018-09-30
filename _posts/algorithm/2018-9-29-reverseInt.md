---
layout: post
title: #7反转整数 
category: 算法
tags: C
description: #7反转整数 
--- 
### 目标

给定一个 32 位有符号整数，将整数中的数字进行反转。

示例 1:

	输入: 123
	输出: 321

示例 2:

	输入: -123
	输出: -321
示例 3:

	输入: 120
	输出: 21
	
注意:
假设我们的环境只能存储 32 位有符号整数，其数值范围是 [−231,  231 − 1]。根据这个假设，如果反转后的整数溢出，则返回 0。

实现：

	//C style
	int reverse(int x) {
	    if(x >= 2147483648 - 1 || x <=-2147483648){
	        return 0;
	    }
	    int a = 0;
	    int c = x;
	    if(c < 0) {
	        c = -c;
	    }
	    int sum = 0;
	    do {
	        a = c%10;
	        c = c/10;
	        if(sum > 214748364 || c > 214748364){
	            return 0;
	        }
	        sum = a  + sum *10;
	    } while (c>0);
	    
	    if (x < 0) {
	        sum = -sum;
	    }
    return sum;
}

输入：
	
	123

输出：

	321
