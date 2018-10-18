---
layout: post
title: 按奇偶排序数组II#922
category: 算法
tags: ios
description: 按奇偶排序数组II#922
--- 

给定一个非负整数数组 `A`， `A` 中一半整数是奇数，一半整数是偶数。

对数组进行排序，以便当 `A[i]` 为奇数时，`i` 也是奇数；当 `A[i]` 为偶数时， `i` 也是偶数。

你可以返回任何满足上述条件的数组作为答案。

 

示例：

	输入：[4,2,5,7]
	输出：[4,5,2,7]
	解释：[4,7,2,5]，[2,5,4,7]，[2,7,4,5] 也会被接受。
 

提示：

	2 <= A.length <= 20000
	A.length % 2 == 0
	0 <= A[i] <= 1000
	
	/**
	 * Return an array of size *returnSize.
	 * Note: The returned array must be malloced, assume caller calls free().
	 */
	int* sortArrayByParityII(int* A, int ASize, int* returnSize) {
	    int *B = NULL;
	    B = malloc(sizeof(int) * ASize);
	    int n = 0, m = ASize - 1;
	    for(int i = 0; i < ASize;i++) {
	       
	        if(A[i] % 2 == 0) {
	            B[n] = A[i];
	            n+=2;
	        } else {
	            B[m] = A[i];
	            m-=2;
	        }
	    }
	    returnSize[0] = ASize;
	    return B;
	}
	
输入：
	
	[4,2,5,7]

输出：

	[4,7,2,5]