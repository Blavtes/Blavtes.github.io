---
layout: post
title: 求众数#169
category: 算法
tags: ios
description: 求众数#169
--- 
给定一个大小为` n` 的数组，找到其中的众数。众数是指在数组中出现次数大于 `⌊ n/2 ⌋` 的元素。

你可以假设数组是非空的，并且给定的数组总是存在众数。

示例 1:

	输入: [3,2,3]
	输出: 3
示例 2:

	输入: [2,2,1,1,1,2,2]
	输出: 2

解法：

	//C style
	
	int majorityElement(int* nums, int numsSize) {
	    int candidate;
	    int count=0;
	    for(int i=0;i<numsSize;i++)
	    {
	        if(count==0)
	            candidate=nums[i];
	        if(nums[i]==candidate)
	            count++;
	        else
	            count--;
	    }
	    return candidate;
	}
	
输入：

	[2,2,1,1,1,3,0]
	
输出：

	1