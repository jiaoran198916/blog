---
title: 1、数据类型的分类与判断
tags: 数据类型
categories: JS高级
excerpt: 5种基本类型+3种对象类型
abbrlink: f0517a0b
date: 2020-08-08 20:44:42
---
## 分类
  * 基本(值)类型
    * String: 任意字符串
    * Number: 任意的数值，三个特殊值: `Infinity`, `-Infinity`, `NaN`.
    * Boolean: true/false
    * undefined: undefined, 变量声明未赋值，` is reserved as a default initial value for unassigned things.`
    * null: null，表示“nothing”, “empty”, “value unknown”.
  * 对象(引用)类型
    * Object: 任意对象
    * Function: 一种特殊的对象(可执行)
    * Array: 一种特殊的对象(数值下标, 内部数据有序)
*************
## 判断
### typeof
  返回数据类型的字符串表达形式（小写），支持两种语法：
  - 作为操作符: `typeof x`
  - 作为函数: `typeof(x)`

```
typeof undefined // "undefined"
typeof 0 // "number"
typeof 10n // "bigint"
typeof true // "boolean"
typeof "foo" // "string"
typeof Symbol("id") // "symbol" ？
typeof Math // "object"

typeof null // "object", 无法区分 null 与 object 类型
typeof [1,2] // "object", 无法区分 array 与 object 类型
typeof alert // "function"，可以区分 function 与 object 类型
```
### instanceof
专门用来判断对象数据的类型: Object, Array 与 Function
### ===
只能判断具有唯一值的类型，即: undefined, null
*************
## 相关问题
### 1、什么时候给变量赋值为null？
* var a = null //初始赋值, 表明将要赋值为对象
* a = null //结束前, 让对象成为垃圾对象(被垃圾回收器回收)

### 2、严格区别变量类型与数据类型?
变量本身是没有类型的, 变量的类型实际上是变量内存中数据的类型
* 变量的类型(变量内存值的类型)
  * 基本类型: 保存就是基本类型的数据
  * 引用类型: 保存的是对象的地址值
* 数据的类型
  * 基本类型
  * 对象类型
