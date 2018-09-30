---
layout: post
title: 最长公共前缀#14
category: 算法
tags: C
description: 最长公共前缀#14
--- 
### 目标

编写一个函数来查找字符串数组中的最长公共前缀。

如果不存在公共前缀，返回空字符串 `""`。

示例 1:

	输入: ["flower","flow","flight"]
	输出: "fl"
示例 2:

	输入: ["dog","racecar","car"]
	输出: ""
	解释: 输入不存在公共前缀。
说明:

	所有输入只包含小写字母 a-z 。

实现：

	//C style
	
	char* longestCommonPrefix(char** strs, int strsSize) {
	    char *p = *strs;
	    if (strsSize == 1) {
	        return p;
	    }
	    if (p == NULL) {
	        return "";
	    }
	    int j = 0;
	    while(p[j] != '\0') {
	        for(int i = 1; i < strsSize; i++) {
	            if(p[j] != strs[i][j]) {
	                p[j] = '\0';
	                return p;
	            }
	        }
	        j++;
	    }
	    return p;
	}

输入：
	
	["flower","flow","flight"]

输出：

	"fl"
