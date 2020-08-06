---
title: thinkPHP模型调试之查看执行的SQL语句
tags:
  - thinkPHP
  - SQL
  - 调试
categories: PHP
excerpt: dd
abbrlink: 65fe8651
date: 2020-08-06 14:30:57
---

## 调试执行的SQL语句
在模型操作中 ，为了更好的查明错误，经常需要查看下最近使用的SQL语句，我们可以用 `getLastsql` 方法来输出上次执行的sql语句。例如：
```php
$User = M("User"); // 实例化User对象
$User->find(1);
echo $User->getLastSql();
// 3.2版本中可以使用简化的方法
echo $User->_sql();
```
并且每个模型都使用独立的最后SQL记录，互不干扰，但是可以用空模型的getLastSql方法获取全局的最后SQL语句。

```php
echo M()->getLastSql();
```
************
## fetchSql
模型连贯操作之一 `fetchSql` 用于直接返回SQL而不是执行查询，适用于任何的CURD操作方法。 例如：
```PHP
$result = M('User')->fetchSql(true)->find(1);
```
************
## 调试数据库错误信息
在模型操作中，还可以获取数据库的错误信息，例如：
```PHP
$User = M("User");
$result = $User->find(1);
if(false === $result){
  echo $User->getDbError();
}
```
> CURD操作如果返回值为false，表示数据库操作发生错误，这时就需要使用模型的getDbError方法来查看数据库返回的具体错误信息。
************
