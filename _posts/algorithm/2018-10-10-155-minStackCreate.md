---
layout: post
title: 最小栈#155
category: 算法
tags: C
description: 最小栈#155
--- 

### 目标

设计一个支持 `push，pop，top` 操作，并能在常数时间内检索到最小元素的栈。

	push(x) -- 将元素 x 推入栈中。
	pop() -- 删除栈顶的元素。
	top() -- 获取栈顶元素。
	getMin() -- 检索栈中的最小元素。
示例:
	
	MinStack minStack = new MinStack();
	minStack.push(-2);
	minStack.push(0);
	minStack.push(-3);
	minStack.getMin();   --> 返回 -3.
	minStack.pop();
	minStack.top();      --> 返回 0.
	minStack.getMin();   --> 返回 -2.
	
实现：

`C :`
	
	typedef struct {
	   
	    int top;
	    int minTop;
	    int *data;
	    int *min;
	} MinStack;
	
	/** initialize your data structure here. */
	MinStack* minStackCreate(int maxSize) {
	    MinStack *stack = (MinStack*)malloc(maxSize*sizeof(MinStack));
	    stack->data = (int*)malloc(maxSize *sizeof(int));
	    stack->min = (int*)malloc(maxSize *sizeof(int));
	    // memset(stack->data,0,maxSize);
	    // memset(stack->min,0,maxSize);
	    stack->top = -1;
	    stack->minTop = -1;
	    return stack;
	}
	
	void minStackPush(MinStack* obj, int x) {
	    obj->top++;
	    obj->data[obj->top] = x;
	    if(obj->minTop == -1 || obj->min[obj->minTop] >= x) {
	        obj->minTop++;
	        obj->min[obj->minTop] = x;
	    }
	}
	
	void minStackPop(MinStack* obj) {
	    int temp, temp1;
	    if(obj->top == -1){
	        return;
	    }
	    temp = obj->data[obj->top];
	    obj->top--;
	    if(temp == obj->min[obj->minTop]){
	       temp1 = obj->min[obj->minTop];
	       obj->minTop--;
	    }
	}
	
	int minStackTop(MinStack* obj) {
	   return obj->data[obj->top];
	}
	
	int minStackGetMin(MinStack* obj) {
	    return obj->min[obj->minTop];
	}
	
	void minStackFree(MinStack* obj) {
	
	}
	
	/**
	 * Your MinStack struct will be instantiated and called as such:
	 * struct MinStack* obj = minStackCreate(maxSize);
	 * minStackPush(obj, x);
	 * minStackPop(obj);
	 * int param_3 = minStackTop(obj);
	 * int param_4 = minStackGetMin(obj);
	 * minStackFree(obj);
	 */


