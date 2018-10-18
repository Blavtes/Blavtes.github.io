---
layout: post
title: Excel表列名称#168
category: 算法
tags: ios
description: Excel表列名称#168
--- 

给定一个正整数，返回它在 Excel 表中相对应的列名称。

例如，

    1 -> A
    2 -> B
    3 -> C
    ...
    26 -> Z
    27 -> AA
    28 -> AB 
    ...
示例 1:

	输入: 1
	输出: "A"
示例 2:

	输入: 28
	输出: "AB"
示例 3:

	输入: 701
	输出: "ZY"

解法：
	
	//C style
	//65->A
	char* convertToTitle(int n) {
	
	    char *d = (char*)malloc(sizeof(char*) * 10);
	    
	    int i = 0;
	    while(n > 0){
	        int x = (n-1)%26;
	        n = (n-1) / 26;
	        d[i++] = x+'A';
	    }
	    char *a =  (char*)malloc(sizeof(char*) * 10);
	    i = 0;
	    int j = strlen(d) -1;
	    while(j>=0) {
	        a[i++] = d[j--];
	    }
	    return a;
	}

输入:

	 701
输出: 

	"ZY"