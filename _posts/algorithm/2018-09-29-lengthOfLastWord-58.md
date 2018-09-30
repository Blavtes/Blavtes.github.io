---
layout: post
title: 最后一个单词的长度#58
category: 算法
tags: C
description: 最后一个单词的长度#58
--- 

### 目标

给定一个仅包含大小写字母和空格 `' '` 的字符串，返回其最后一个单词的长度。

如果不存在最后一个单词，请返回 `0` 。

说明：一个单词是指由字母组成，但不包含任何空格的字符串。

示例:

	输入: "Hello World"
	输出: 5


实现：


	//C style
	int lengthOfLastWord(char* s) {
	    int n = 0;
	    for (int i = 0; i < strlen(s);i++) {
	        char a = s[i];
	        if (a != ' ') {
	            n++;
	        } else {
	            if  (i < strlen(s)-1 && s[i+1]!=' ') {
	                n=0;
	            }
	        }
	    }
	    return n;
	}
	
输入：
	
	 "Hello World"

输出:

	 5

