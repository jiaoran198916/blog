---
title: strtotime关于在某个日期区间的优化
tags:
  - strtotime
  - date
categories: PHP
excerpt: 'strtotime("$info[''freedayend''] +1 day")'
abbrlink: 1cf0e13d
date: 2020-08-07 10:53:46
---
工作中，经常碰到需要判断某个当前时间是否在某个时间区间的情况，一般可通过使用 strtotime 将日期转换成时间戳，然后进行比较，比如：
```php
$freedaystart = strtotime($info['freedaystart'].' 00:00:00');
$freedayend = strtotime($info['freedayend'].' 23:59:59');
if(time() > $freedaystart &&  time() < $freedayend){
    //...
}
```
但时分秒拼接上去，感觉不够简洁优雅，可以将结束时间退后一天，时分秒仍默认为0点，像下面这样：
```php
$freedaystart = strtotime($info['freedaystart']);
$freedayend = strtotime("$info['freedayend'] +1 day");
```
是不是感觉清爽多了，strtotime 还支持其他时间格式，如 `strtotime("$date +1 month +2 day")`等，完整格式列表可参看官网对应页面。
******
经测试，这里 day 的单复数都没有影响，可能是为了更好的兼容，不过为了严谨也为了增强可读性，建议按规范写，该复数的加上复数。
********
日期数据也是可以直接比较的，但需要保持要比较的数据格式完全一致，否则容易出错，因为它们本质上还是当成字符串比较，所以最保险的还是转化成时间戳比较。
比如：
```
'2020-04-05' > '2020-03-05'//true
'2020-04-05' > '2020-3-5'//false
```
