---
layout: post
title: 组合两个表#175
category: 算法
tags: SQL
description: 组合两个表#175
--- 

SQL架构

	Create table Person (PersonId int, FirstName varchar(255), LastName varchar(255))
	Create table Address (AddressId int, PersonId int, City varchar(255), State varchar(255))
	Truncate table Person
	insert into Person (PersonId, LastName, FirstName) values ('1', 'Wang', 'Allen')
	Truncate table Address
	insert into Address (AddressId, PersonId, City, State) values ('1', '2', 'New York City', 'New York')
	
表1: `Person`

	+-------------+---------+
	| 列名         | 类型     |
	+-------------+---------+
	| PersonId    | int     |
	| FirstName   | varchar |
	| LastName    | varchar |
	+-------------+---------+
	PersonId 是上表主键
表2: `Address`

	+-------------+---------+
	| 列名         | 类型    |
	+-------------+---------+
	| AddressId   | int     |
	| PersonId    | int     |
	| City        | varchar |
	| State       | varchar |
	+-------------+---------+
	AddressId 是上表主键
 

编写一个 `SQL` 查询，满足条件：无论 `person `是否有地址信息，都需要基于上述两表提供 `person` 的以下信息：

	FirstName, LastName, City, State

MySQL:

	# Write your MySQL query statement below
	select FirstName, LastName, City, State from Person left join Address on Person.PersonId=Address.PersonId;
	
我的输入:

	{"headers": {"Person": ["PersonId", "LastName", "FirstName"], "Address": ["AddressId", "PersonId", "City", "State"]}, "rows": {"Person": [[1, "Wang", "Allen"]], "Address": [[1, 2, "New York City", "New York"]]}}
	
我的答案:

	{"headers":["FirstName","LastName","City","State"],"values":[["Allen","Wang",null,null]]}