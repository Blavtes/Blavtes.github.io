---
layout: post
title: 最大子序和#53
category: 算法
tags: C
description: 最大子序和#53
--- 

### 目标

给定一个整数数组 `nums` ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

示例:

	输入: [-2,1,-3,4,-1,2,1,-5,4],
	输出: 6
	解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。
进阶:

如果你已经实现复杂度为 `O(n)` 的解法，尝试使用更为精妙的分治法求解。


实现：

a:

	//C style
	int max(int a,int b){
	    return a>b?a:b;
	}
	
	int maxSubArray(int* nums, int numsSize) {
	    int sum=0;
	    int m=-2147483647;
	    
	    for(int i=0;i<numsSize;i++){
	       sum=max(sum+nums[i],nums[i]);
	       m=max(sum,m);
	    }
	    return m;
	}

b:

	int maxSubArray(int* nums, int numsSize) {
	    int maxsum=nums[0],subsum=nums[0],i;
	    for(i=1;i<numsSize;i++)
	    {
	        if(subsum<0)
	            subsum=nums[i];
	        else
	            subsum+=nums[i];
	        if(subsum>maxsum)
	            maxsum=subsum;
	    }
	    return maxsum;
	}
输入：
	
	5

输出：

	"111221"
