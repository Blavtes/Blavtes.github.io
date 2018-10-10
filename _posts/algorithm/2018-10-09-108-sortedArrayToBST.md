---
layout: post
title: 将有序数组转换为二叉搜索树#108
category: 算法
tags: C
description: 将有序数组转换为二叉搜索树#108
--- 

### 目标

将一个按照升序排列的有序数组，转换为一棵高度平衡二叉搜索树。

本题中，一个高度平衡二叉树是指一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过 `1`。

示例:

	给定有序数组: [-10,-3,0,5,9],
	
	一个可能的答案是：[0,-3,9,-10,null,5]，它可以表示下面这个高度平衡二叉搜索树：
	
	      0
	     / \
	   -3   9
	   /   /
	 -10  5

返回其自底向上的层次遍历为：
	
	[
	  [15,7],
	  [9,20],
	  [3]
	]

实现：

`C :`
	
	/**
	 * Definition for a binary tree node.
	 * struct TreeNode {
	 *     int val;
	 *     struct TreeNode *left;
	 *     struct TreeNode *right;
	 * };
	 */
	
	struct TreeNode *heper(int *nums,int l ,int r) {
	    if(l <= r) {
	        int mid = (l+r) /2;
	        struct TreeNode *node = (struct TreeNode*)malloc(mid * sizeof(struct TreeNode));
	        node->val = nums[mid];
	        node->left = heper(nums,l,mid-1);
	        node->right = heper(nums,mid+1,r);
	        return node;
	    }
	    return NULL;
	}
	
	struct TreeNode* sortedArrayToBST(int* nums, int numsSize) {
	    if (numsSize == 0 || nums == NULL) {
	         return NULL;
	    }
	    return heper(nums,0,numsSize - 1);
	}


输入:

	[-10,-3,0,5,9]
	
输出:

	[0,-10,5,null,-3,null,9]

