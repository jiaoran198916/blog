---
title: jQuery数组的操作
tags: jQuery
abbrlink: 30266b9b
date: 2020-07-28 16:15:20
categories: JavaScript
---
*********
jQuery操作数组主要有两种方式：
## 普通数组
```js
$.each(array,function(k,v){
  //...
});
```
- 关联数组，{"id":10,"name":"tom"}
- 索引数组，[1,2,3,4,5,6,7,8,9]

k:如果是关联是键名，如果是索引是下标（从0开始;   
vo:是元素值;
  ********
## 对象数组
```js
$("p").each(function(k,v){
  //...
})
```
i 是数组元素的下标数字，索引下标   
v 是dom中的节点[子对象]

其中
v = this = `'<p>...</p>'` //字符串   
$(v) = $(this) = init... //dom节点对象
