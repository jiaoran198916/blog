---
title: 4、JS中的函数
tags: Function
categories: JS高级
excerpt: 什么是函数，如何调用函数，回调函数，匿名函数自调用，this的理解
abbrlink: a7b6368c
date: 2020-08-09 19:24:00
---
## JS中的函数
1. 什么是函数?
  * 具有特定功能的n条语句的封装体
  * 只有函数是可执行的, 其它类型的数据是不可执行的
  * 函数也是对象
2. 为什么要用函数?
  * 提高代码复用
  * 便于阅读和交流
3. 如何定义函数?
  * 函数声明 `function f(){}`
  * 表达式 `var f = function(){}`
4. 如何调用(执行)函数?
  * test(): 直接调用
  * obj.test(): 通过对象调用
  * new test(): new调用
  * test.call/apply(obj): 临时让test成为obj的方法进行调用
**************
## 回调函数
1. 什么函数才是回调函数?
  * 你定义的
  * 没有直接调用
  * 但最终它执行了(在特定条件或时刻)
2. 常见的回调函数?
  * DOM事件函数 ==>发生事件的dom元素
  * 定时器函数 ===>window, setInterval、setTimeout
  * ajax回调函数
  * 生命周期回调函数

**************
## 匿名函数自调用 (IIFE)
1. 理解
  * 全称: Immediately-Invoked Function Expression 立即调用函数表达式
  * 别名: 匿名函数自调用
2. 作用
  * 隐藏内部实现
  * 不污染外部命名空间
  * 用来编码js模块
```js
;(function () {
   var a = 1
   function test () {
     console.log(++a)
   }
   window.$ = function () { // 向外暴露一个全局函数
     return {
       test: test
     }
   }
  })()
$().test() // 1. $是一个函数 2. $执行后返回的是一个对象
```
**************
## 函数中的this
1. this是什么?
  * 任何函数本质上都是通过某个对象来调用的, 如果没有直接指定就是window
  * 所有函数内部都有一个变量this，可以直接使用
  * 它的值是调用函数的当前对象
  * 一个关键字, 一个内置的引用变量
  * 在定义函数时, this还没有确定, 只有在执行时才动态确定(绑定)的
2. 如何确定this的值?
  * test(): window
  * p.test(): p
  * new test(): 新创建的对象
  * p.call(obj): obj
