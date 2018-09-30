---
layout: post
title: 删除排序链表中的重复元素#83
category: 算法
tags: C
description: 删除排序链表中的重复元素#83
--- 

### 目标

给定一个排序链表，删除所有重复的元素，使得每个元素只出现一次。

示例 `1`:

	输入: 1->1->2
	输出: 1->2
示例 2:

	输入: 1->1->2->3->3
	输出: 1->2->3


实现：

	//C style
	/**
	 * Definition for singly-linked list.
	 * struct ListNode {
	 *     int val;
	 *     struct ListNode *next;
	 * };
	 */
	struct ListNode* deleteDuplicates(struct ListNode* head) {
	     // write your code here
	    if(head==NULL)
	        return 0;
	    if(head->next==NULL)
	        return head;
	    struct ListNode *cur=head;
	    struct ListNode *pre=NULL;
	    while(cur!=NULL)
	    {
	        if(pre!=NULL&&pre->val==cur->val)
	        {
	            pre->next=cur->next;
	        }
	        else
	        {
	            pre=cur;
	        }
	        cur=cur->next;
	    }
	    return head;
	}



输入:

	1->1->2->3->3
输出:

	1->2->3

