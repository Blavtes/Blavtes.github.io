---
layout: post
title: 报数#38
category: 算法
tags: C
description: 报数#38
--- 

### 目标

报数序列是指一个整照其中的整数的顺序进数序列，按行报数，得到下一个数。其前五项如下：

	1.     1
	2.     11
	3.     21
	4.     1211
	5.     111221
`1` 被读作  `"one 1"`  ("一个一") , 即 `11`。
`11` 被读作 `"two 1s"` ("两个一"）, 即 `21`。
`21` 被读作 `"one 2",  "one 1"` （"一个二" ,  "一个一") , 即 `1211`。

给定一个正整数 `n（1 ≤ n ≤ 30）`，输出报数序列的第` n `项。

注意：整数顺序将表示为一个字符串。

 

示例 1:

输入: 1
输出: "1"
示例 2:

输入: 4
输出: "1211"


实现：

	//C style
	char* countAndSay(int n) {
	    if(n == 1) return "1";
	
	    char * cur = malloc(2);
	    char * temp;
	    cur[0] = '1';
	    cur[1] = 0;
	
	    int len, idx, j, count;
	    for(int i = 2; i <= n; i++) {
	
	        len = strlen(cur);
	        temp = malloc(3 * len);
	        memset(temp, 0, 3 * len);
	        count = 1;
	        for(idx = 1, j = 0; idx < len; idx++) {
	            if(cur[idx] == cur[idx - 1]) count++;
	            else {
	                temp[j++] = '0' + count;
	                temp[j++] = cur[idx - 1];
	                count = 1;
	            }
	        }
	        temp[j++] = '0' + count;
	        temp[j] = cur[len - 1];
	        free(cur);
	        cur = temp;
	    }
	    return cur;
	}
输入：
	
	5

输出：

	"111221"
