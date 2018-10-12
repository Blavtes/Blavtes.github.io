---
layout: post
title: 只出现一次的数字#136
category: 算法
tags: C
description: 只出现一次的数字#136
--- 

### 目标

给定一个非空整数数组，除了某个元素只出现一次以外，其余每个元素均出现两次。找出那个只出现了一次的元素。

说明：

你的算法应该具有线性时间复杂度。 你可以不使用额外空间来实现吗？

示例 1:

	输入: [2,2,1]
	输出: 1
	
示例 2:

	输入: [4,1,2,1,2]
	输出: 4

实现：

`C :`
	
	int singleNumber(int* nums, int numsSize) {
	    if(numsSize <= 1) {
	        return nums[0];
	    }
	    int x = 0;
	    
	    for (int i = 0; i < numsSize; i++) {
	        x ^=nums[i];
	    }
	    return x;
	}	
	
输入: 
	
	[4,1,2,3,2,3,1]
	
输出:

	 4


