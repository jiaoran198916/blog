---
title: JS中 Number()方法的两种用法
date: 2020-08-13 13:47:36
tags: [Number, 数据类型]
categories: JavaScript
---
JS中，调用Number()主要有两种方式，一是作为一个 function 将任意类型的数据转换成数值，二是作为一个类，通过new 生成一个数值对象。  
<!--more -->
其中第一种方式更常用。
*********
## 用法一：function
```
Number(value)
```
将一个任意类型的数据转换成数值，无法转换的则返回 NaN，转换规则类似于类型隐式转换，与 `parseFloat` 略有差异。

转换规则如下：

|  值 Value | 结果 Result |
| ------------ | ------------ |
| undefined  | NaN  |
| null  | 0  |
| false  | 0  |
| true  | 1  |
| number  | 原样输出  |
| string  | 忽略前后空格，碰到第一个非数字字符为止，空字符串返回 0  |
| object  | 调用内部 ToPrimitive(value, Number)，如果是 Date 对象，返回从 1970年1月1日至Date的毫秒数  |

*******
## 用法二：constructor
```
new Number(num)
```
作为一个构造器，生成一个 Number 实例， wraps num (after converting it to a number).

如：
```
> typeof new Number(3)
'object'
```
既然是对象，肯定有相关的属性和方法，Number也不例外。
### 属性 Properties
- Number.MAX_VALUE 表示的最大正数值  
```
  > Number.MAX_VALUE
  1.7976931348623157e+308
```
- Number.MIN_VALUE 表示的最小正数值
```
> Number.MIN_VALUE
5e-324
```
- Number.NaN 与全局 NaN 等同
- Number.NEGATIVE_INFINITY 与 -Infinity 等同
- Number.POSITIVE_INFINITY 与 Infinity 等同

### 方法 Methods
所有原生的数值相关函数均被保存在对象原型（ Number.prototype ）里，可以直接调用。
- Number.prototype.toFixed(fractionDigits?)
```
> 0.0000003.toFixed(10)
'0.0000003000'
```
- Number.prototype.toPrecision(precision?)
```
> 1234..toPrecision(3)
'1.23e+3'
```
- Number.prototype.toString(radix?)
```
> 15..toString(2)
'1111'
> 65535..toString(16)
'ffff'
```
- Number.prototype.toExponential(fractionDigits?)
**********
## 参考资料
- [http://speakingjs.com/Chapter 11. Numbers](http://speakingjs.com/es5/ch11.html)
