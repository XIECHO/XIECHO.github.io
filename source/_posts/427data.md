--- 
title: SQL入门 
date: 2018-04-27 15:37:21
tags: [SQL]
categories: 
---
# 数据操作语言（DML）
- select: 从数据库中获取数据
- update： 更新数据库表中的数据 
- delete： 从数据库中删除数据
- insert into : 向数据库中插入数据

# 数据定义语言（DDL）
用于创建和删除表格，也可以定义索引（键），规定表之间的链接，以及施加表间的约束。

- create database : 创建新数据库
- alter database : 修改数据库
- create table ： 创建新表
- alter table : 变更（改变）数据库表
- drop table : 删除表
- create index ： 创建索引（搜索键）
- drop index : 删除索引

# 语句
## select语句
- select 列名称 from 表名称
- select * from 表名称

## select distinct
去重复
- select distinct 列名称 from 表名称

## where子句
如需有条件地从表中选取数据，可将where子句添加到select语句。
- select 列名称 from 表名称 where 列 运算符 值
运算符： =, <>, >, <, >=, <=, between, like

## AND和OR运算符
可在where子语句中把两个或多个条件结合起来。

- select * from Persons where FirstName='Thomas' and LastName='Carter'

## order by语句
order by 语句用于根据指定的列对结果集进行排序。
默认升序，降序用desc。

- select Company，OrderNumber from Orders order by Company desc
- select Company, ORderNumber from orders order by Company desc, orderNumber asc

desc: descend; asc: ascend

## insert into语句
插入新的行。
- insert into 表名称 values(值1， 值2， ...)
- insert into table_name(列1，列2，...) values(值1，值2，...)

- insert into Persons(lastName, Address) values ('Wilson', 'Chapms-Elysees')

## update语句
- update 表名称 set 列名称 = '新值' where 列名称 = 某值

## delete语句
删除表中的行
- delect from 表名称 where 列名称 = 值
删除所有行
- delect from table_name

## limit语句
返回表中头几行
- select * from table_name limit number

## like操作符
like操作符用于在where子句中搜索列中的指定模式。
- select * from Persons where city like 'N%'
%可用于定义通配符（模式中缺少的字母）， NOT指代不包含
- select * from Persons where city not like '%lon%'

## SQL通配符
通配符必须与Like运算符一起使用

通配符 | 描述
% | 代替一个或多个字符
- | 仅代替一个字符

## in
- select * from table_name where 列 in (值1，值2)
