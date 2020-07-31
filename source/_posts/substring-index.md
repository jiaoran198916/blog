---
title: MySQL字符串函数：substring_index()的使用详解
date: 2020-07-31 16:36:15
tags: [MySQL,String]
---
## 定义
SUBSTRING_INDEX - 按分隔符截取字符串
## 语法
```
SUBSTRING_INDEX(str, delimiter, count)
```
返回一个 str 的子字符串，在 delimiter 出现 count 次的位置截取。
如果 count > 0，从则左边数起，且返回位置前的子串；
如果 count < 0，从则右边数起，且返回位置后的子串。

delimiter 是大小写敏感，且是多字节安全的。

## 示例
```
mysql> SELECT SUBSTRING_INDEX('www.mysql.com', '.', 2);
        -> 'www.mysql'
mysql> SELECT SUBSTRING_INDEX('www.mysql.com', '.', -2);
        -> 'mysql.com'
```
## 总结
这个函数很实用，PHP中都没有类似的函数，  
比如取一个以斜线分割的图片路径的名称，`201807/20180731181759_5b603757ea5e4.jpg`，这个函数可以一步到位，PHP中则需要explode成数组，然后取最后一个元素。

美中不足的是，我感觉可以再设置个可选参数，就是返回的时候是否保留分隔符，这个当然通过concat连接，但如果能直接返回就更好了。
