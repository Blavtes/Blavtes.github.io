---
layout: post
title: 搜索插入位置#35
category: 算法
tags: C
description: 简单
--- 

### 目标

给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。

你可以假设数组中无重复元素。

示例 `1`:

	输入: [1,3,5,6], 5
	输出: 2
示例 `2`:

	输入: [1,3,5,6], 2
	输出: 1
示例 `3`:

	输入: [1,3,5,6], 7
	输出: 4
示例 `4`:

	输入: [1,3,5,6], 0
	输出: 0


实现：

	//C style
	int searchInsert(int* nums, int numsSize, int target) {
	    
	    if (target < nums[0]) { 
	        return 0;
	    }
	    if (target > nums[numsSize -1]) {
	        return numsSize;
	    }
	    for(int i = 0; i <numsSize ; i++) {
	        if(target <= nums[i]) {
	            return i;
	        } 
	    }
	    return 0;
	}
输入：
	
	[1,3,5,6]
	5

输出：

	2
