---
layout: post
title: 验证回文串#125
category: 算法
tags: C
description: 验证回文串#125
--- 

### 目标

给定一个字符串，验证它是否是回文串，只考虑字母和数字字符，可以忽略字母的大小写。

说明：本题中，我们将空字符串定义为有效的回文串。

示例 1:
	
	输入: "A man, a plan, a canal: Panama"
	输出: true
示例 2:

	输入: "race a car"
	输出: false

实现：

`C :`
	
	bool isPalindrome(char* s) {
	
	    int i = 0, j = strlen(s) - 1;  
	    while(i < j){  
	        char x = s[i];
	        char y = s[j];
	        if(x >='a' && x<='z' ||  x >='A' && x<='Z' || x >= '0' && x <= '9')  {
	            if( x >='A' && x<='Z') {
	              x=x+32; 
	            }
	            if(y >='a' && y<='z' ||  y >='A' && y<='Z'||y >= '0' && y <= '9')  {
	                if(y >='A' && y<='Z') {
	                    y = y+32;
	                }
	                if(x == y ){
	                    i++;
	                    j--;
	                } else {
	                    return false;
	                }
	           } else {
	               j--;
	           }
	       } else {
	           i++;
	       }
	    }  
	    return true;
	}
	
输入: 
	
	"A man, a plan, a canal: Panama"
	
输出:

	 true


