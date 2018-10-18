---
layout: post
title: Excel表列序号#171
category: 算法
tags: ios
description: Excel表列序号#171
--- 

给定一个Excel表格中的列名称，返回其相应的列序号。

例如，

    A -> 1
    B -> 2
    C -> 3
    ...
    Z -> 26
    AA -> 27
    AB -> 28 
    ...
示例 1:

	输入: "A"
	输出: 1
示例 2:

	输入: "AB"
	输出: 28
示例 3:

	输入: "ZY"
	输出: 701

解法：

	//C style
	int heper(int x)
	{
	    if(x == 0) {
	        return 1;
	    }
	    if(x <= 1) {
	        return x*26;
	    }
	    return 26 * heper(x-1);
	}
	
	int titleToNumber(char* s) {
	    int l = strlen(s);
	    int sum = 0;
	    for(int i = l - 1 ;i >= 0;i--) {
	
	        int x =  (s[i] -'A' +1) *heper(l - i - 1);
	        sum += x ;
	    }
	
	    return sum;
	}
	
输入: 
	
	"ZY"
输出:
	
	701