---
layout: post
title: 二叉树的层次遍历II#107
category: 算法
tags: C
description: 二叉树的层次遍历II#107
--- 

### 目标

给定一个二叉树，返回其节点值自底向上的层次遍历。 （即按从叶子节点所在层到根节点所在的层，逐层从左向右遍历）

例如：
给定二叉树 `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7

```	

返回其自底向上的层次遍历为：
	
	[
	  [15,7],
	  [9,20],
	  [3]
	]

实现：

`swift :`

	/**
	 * Definition for a binary tree node.
	 * public class TreeNode {
	 *     public var val: Int
	 *     public var left: TreeNode?
	 *     public var right: TreeNode?
	 *     public init(_ val: Int) {
	 *         self.val = val
	 *         self.left = nil
	 *         self.right = nil
	 *     }
	 * }
	 */
	class Solution {
	    func levelOrderBottom(_ root: TreeNode?) -> [[Int]] {
	         guard let root = root else {
	            return []
	        }
	        var result = [[TreeNode]]()
	        var level = [TreeNode]()
	
	        level.insert(root, at: 0)
	        while level.count != 0 {
	            result.insert(level, at: 0)
	            var nextLevel = [TreeNode]()
	            for node in level {
	                if let leftNode = node.left {
	                    nextLevel.append(leftNode)
	                }
	                if let rightNode = node.right {
	                    nextLevel.append(rightNode)
	                }
	            }
	            level = nextLevel
	        }
	        let ans = result.map { $0.map { $0.val }}
	        return ans
	    }
	}

`C :`
	
	/**
	 * Definition for a binary tree node.
	 * struct TreeNode {
	 *     int val;
	 *     struct TreeNode *left;
	 *     struct TreeNode *right;
	 * };
	 */
	/**
	 * Return an array of arrays of size *returnSize.
	 * The sizes of the arrays are returned as *columnSizes array.
	 * Note: Both returned array and *columnSizes array must be malloced, assume caller calls free().
	 */
	int maxDepth (struct TreeNode *root) {
	    if (root == NULL) {
	        return 0;
	    }
	    int ld = maxDepth(root->left);
	    int rd = maxDepth(root->right);
	    return (ld > rd ? ld : rd) + 1;
	}
	
	void every_nums(struct TreeNode *root, int k, int *arr) {
	    if (root == NULL) {
	        return ;
	    }
	    arr[k] += 1;
	    every_nums(root->left, k + 1, arr);
	    every_nums(root->right, k + 1, arr);
	}

	void fetch_result(struct TreeNode *root, int k, int **ret, int *size, int depth) {
	    if (root == NULL) {
	        return ;
	    }
	    ret[depth - k - 1][size[depth - k - 1]++] = root->val;
	    fetch_result(root->left, k + 1, ret, size, depth);
	    fetch_result(root->right, k + 1, ret, size, depth);
	    return ;
	}//在这个地方多传入了一个树的深度参数。
	
	int** levelOrderBottom(struct TreeNode* root, int** columnSizes, int* returnSize) {
	    int depth = maxDepth(root);
	    int *size = (int *)malloc(sizeof(int) * depth);
	    memset(size, 0, sizeof(int) * depth);
	    //刚开始我使用memset(size, 0, sizeof(size))报错了，因为size时动态申请的，这样是不合法的。
	    every_nums(root, 0, size);
	    int **ret = (int **)malloc(sizeof(int *) * depth);
	    for (int i = 0; i < depth; ++i) {
	        ret[i] = (int *)malloc(sizeof(int) * size[depth - i - 1]);
	        size[depth -i - 1] = 0;
	    }
	    fetch_result(root, 0, ret, size, depth);
	    *returnSize = depth;
	    *columnSizes = size;
	    return ret;
	}


输入:

	[3,9,20,null,null,15,7]
	
输出:

	[[15,7],[9,20],[3]]

