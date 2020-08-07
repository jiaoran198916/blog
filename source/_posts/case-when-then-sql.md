---
title: 用case when优化Sql语句
tags: SQL
categories: MySQL
excerpt: 用case..when..then...结果优化SQL语句
abbrlink: 382ad94
date: 2020-08-07 10:44:12
---
有些时候想直接从数据库查询数据，并导出，但一些类型或状态存储的是01等数字，你想显示对应的文字，这个时候就可以使用case...when语句了。
## 结构
```
case...when...then...when...then...else...end
```
************
## 示例
```
SELECT id,title,CASE type WHEN 1 THEN '大学' WHEN 2 THEN '小学' ELSE '未知' END as 学历 FROM table;
```
另外还可以使用if实现简单的条件筛选

IF( expr1 , expr2 , expr3 )
expr1 的值为 TRUE，则返回值为 expr2
expr1 的值为 FALSE，则返回值为 expr3
