---
title: 常用MySQL日期时间处理函数
tags: date
categories: MySQL
excerpt: NOW() 与 UNIX_TIMESTAMP()
abbrlink: bcfc76f0
date: 2020-08-07 15:21:52
---
## FROM_UNIXTIME
```sql
FROM_UNIXTIME(unix_timestamp[,format])
```
将时间戳转换成日期时间表示。如'YYYY-MM-DD hh:mm:ss' 或 YYYYMMDDhhmmss
************
## NOW
```sql
NOW([fsp])
```
返回当前时间的日期时间表示，如'YYYY-MM-DD hh:mm:ss' 或 YYYYMMDDhhmmss，取决于执行时的上下文环境，如下
```sql
mysql> SELECT NOW();
-> '2007-12-15 23:50:26'
mysql> SELECT NOW() + 0;//此处+0，所以被当成数值处理
-> 20071215235026.000000
```
参数 fsp （fractional seconds precision），可指定返回秒的精度，取值 0-6
NOW()与CURRENT_TIMESTAMP(), CURRENT_TIMESTAMP是同义词。
************
## UNIX_TIMESTAMP
```sql
UNIX_TIMESTAMP([date])
```
返回当前时间或指定日期的时间戳，如
```
mysql> SELECT UNIX_TIMESTAMP('2015-11-13 10:20:19.012');
-> 1447431619.012
```
************
## DATE_FORMAT
```sql
DATE_FORMAT(date,format)
```
日期格式化
************
## TO_DAYS
```sql
TO_DAYS(date)
```
返回某一日期距离 0 年的总天数，如下面的近似计算应该是，2007*365 + 10*30 + 7 = 732862，有一些差距。
```sql
mysql> SELECT TO_DAYS('2007-10-07');
-> 733321
```
************
