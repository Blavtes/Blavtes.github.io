---
layout: post
title: 合并两个有序链表#21
category: 算法
tags: C
description: 合并两个有序链表#21
--- 
### 目标
将两个有序链表合并为一个新的有序链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 

示例：

	输入：1->2->4, 1->3->4
	输出：1->1->2->3->4->4

实现：

	//C style
	/**
	 * Definition for singly-linked list.
	 * struct ListNode {
	 *     int val;
	 *     struct ListNode *next;
	 * };
	 */
	struct ListNode* mergeTwoLists(struct ListNode* l1, struct ListNode* l2) {
	
	    if (l1 == NULL) {
	        return l2;
	    } else if (l2 == NULL) {
	        return l1;
	    }
	  
	    struct ListNode *p = NULL;  
	    if (l1->val <= l2->val) {  
	        p = l1;  
	        p->next = mergeTwoLists(l1->next, l2);  
	    } else {  
	        p = l2;  
	        p->next = mergeTwoLists(l1, l2->next);  
	    }  
	    return p;  
	}

输入：
	
	1->2->4, 1->3->4

输出：

	1->1->2->3->4->4
