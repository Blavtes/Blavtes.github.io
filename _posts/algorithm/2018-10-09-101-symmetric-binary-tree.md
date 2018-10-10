---
layout: post
title: 对称二叉树#101
category: 算法
tags: C
description: 相同的树#101
--- 

### 目标

给定一个二叉树，检查它是否是镜像对称的。

例如，二叉树 `[1,2,2,3,4,4,3]` 是对称的。

```
    1
   / \
  2   2
 / \ / \
3  4 4  3

```	

但是下面这个 `[1,2,2,null,3,null,3]` 则不是镜像对称的:

```
    1
   / \
  2   2
   \   \
   3    3
```
说明:

如果你可以运用递归和迭代两种方法解决这个问题，会很加分。

实现：

	//C style
	/**
	 * Definition for a binary tree node.
	 * struct TreeNode {
	 *     int val;
	 *     struct TreeNode *left;
	 *     struct TreeNode *right;
	 * };
	 */
	bool checkutSymmetric(struct TreeNode* q,struct TreeNode* p) {
	    if(!q && !p) return true;
	    if(!q || !p) return false;
	    return (q->val == p->val) && checkutSymmetric(q->left,p->right) &&checkutSymmetric(q->right,p->left);
	}
	
	bool isSymmetric(struct TreeNode* root) {
	    if(!root) return true;
	    
	    return checkutSymmetric(root->left,root->right);
	}



输入:

	[1,2,2,3,4,4,3]
	
输出:

	true

