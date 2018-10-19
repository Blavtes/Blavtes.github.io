---
layout: post
title: 从不订购的客户#183
category: 算法
tags: SQL
description: 从不订购的客户#183
---

SQL 架构

	Create table If Not Exists Customers (Id int, Name varchar(255))
	Create table If Not Exists Orders (Id int, CustomerId int)
	Truncate table Customers
	insert into Customers (Id, Name) values ('1', 'Joe')
	insert into Customers (Id, Name) values ('2', 'Henry')
	insert into Customers (Id, Name) values ('3', 'Sam')
	insert into Customers (Id, Name) values ('4', 'Max')
	Truncate table Orders
	insert into Orders (Id, CustomerId) values ('1', '3')
	insert into Orders (Id, CustomerId) values ('2', '1')

某网站包含两个表，`Customers` 表和 `Orders` 表。编写一个 `SQL` 查询，找出所有从不订购任何东西的客户。

`Customers` 表：

	+----+-------+
	| Id | Name  |
	+----+-------+
	| 1  | Joe   |
	| 2  | Henry |
	| 3  | Sam   |
	| 4  | Max   |
	+----+-------+
`Orders` 表：

	+----+------------+
	| Id | CustomerId |
	+----+------------+
	| 1  | 3          |
	| 2  | 1          |
	+----+------------+
	
例如给定上述表格，你的查询应返回：

	+-----------+
	| Customers |
	+-----------+
	| Henry     |
	| Max       |
	+-----------+

MySQL:
	
	# Write your MySQL query statement below
	select Name as Customers from Customers where Id  not in (select CustomerId from Orders)
	
我的输入

	{"headers": {"Customers": ["Id", "Name"], "Orders": ["Id", "CustomerId"]}, "rows": {"Customers": [[1, "Joe"], [2, "Henry"], [3, "Sam"], [4, "Max"]], "Orders": [[1, 3], [2, 1]]}}
	
我的答案

	{"headers":["Customers"],"values":[["Henry"],["Max"]]}