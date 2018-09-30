---
layout: post
title: #9回文数 
category: 算法
tags: C
description: #9回文数 
--- 
### 目标

判断一个整数是否是回文数。回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。

示例 1:

	输入: 121
	输出: true

示例 2:

	输入: -121
	输出: false
	解释: 从左向右读, 为 -121 。 从右向左读, 为 121- 。因此它不是一个回文数。
示例 3:

	输入: 10
	输出: false
	解释: 从右向左读, 为 01 。因此它不是一个回文数。
	

进阶:
你能不将整数转为字符串来解决这个问题吗？

实现：

	//C style
	bool isPalindrome(int x) {
	    if(x<0){
	        return false;
	    }
	    int a = 0;
	    int tmp = x;
	    int sum = 0;
	    do {
	        a = tmp % 10;
	        tmp /= 10;
	        sum = a + sum * 10;
	        if(x == sum) {
	            return true;
	        }
	    } while(tmp>0);
    	return false;
	}

输入：
	
	121

输出：

	true
