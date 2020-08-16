---
title: 6、执行上下文与执行上下文栈
tags:
  - execution
  - 执行上下文
categories: JS高级
abbrlink: fc7eaee4
date: 2020-08-16 20:36:32
---
* 变量提升与函数提升
  * 变量提升: 在变量var定义(声明)语句之前, 就可以访问到这个变量(undefined)
  * 函数提升: 在函数定义语句之前, 就执行该函数
  * 先有变量提升, 再有函数提升
  <!-- more-->
* 理解
  * 执行上下文: 由js引擎自动创建的对象, 包含对应作用域中的所有变量属性
  * 执行上下文栈: 用来管理产生的多个执行上下文
* 分类:
  * 全局: window
  * 函数(局部): 对程序员来说是透明的
* 生命周期
  * 全局 : 准备执行全局代码前产生, 当页面刷新/关闭页面时死亡
  * 函数 : 调用函数时产生, 函数执行完时死亡
* 包含哪些属性:
  * 全局 :
    * 用var定义的全局变量  ==>undefined
    * 使用function声明的函数   ===>function
    * this   ===>window
  * 函数
    * 用var定义的局部变量  ==>undefined
    * 使用function声明的函数   ===>function
    * this   ===> 调用函数的对象, 如果没有指定就是window
    * 形参变量   ===>对应实参值
    * arguments ===>实参列表的伪数组
* 执行上下文创建和初始化的过程
  * 全局:
    * 在全局代码执行前最先创建一个全局执行上下文(window)
    * 收集一些全局变量, 并初始化
    * 将这些变量设置为window的属性
  * 函数:
    * 在调用函数时, 在执行函数体之前先创建一个函数执行上下文
    * 收集一些局部变量, 并初始化
    * 将这些变量设置为执行上下文的属性
* 执行上下文栈
    * 在全局代码执行前, JS引擎就会创建一个栈来存储管理所有的执行上下文对象
    * 在全局执行上下文(window)确定后, 将其添加到栈中(压栈)
    * 在函数执行上下文创建后, 将其添加到栈中(压栈)
    * 在当前函数执行完后,将栈顶的对象移除(出栈)
    * 当所有的代码执行完后, 栈中只剩下window
    ```js
    var a = 10
    var bar = function (x) {
        var b = 5
        foo(x + b)
    }
    var foo = function (y) {
        var c = 5
        console.log(a + c + y)
    }
    bar(10)
    // bar(10)
    ```
**************
* 测试题1
```js
console.log('gb: '+ i)
var i = 1
foo(1)
function foo(i) {
  if (i == 4) {
    return
  }
  console.log('fb:' + i)
  foo(i + 1) //递归调用: 在函数内部调用自己
  console.log('fe:' + i)
}
console.log('ge: ' + i)
  /*
  1. 依次输出什么?
    gb: undefined
    fb: 1
    fb: 2
    fb: 3
    fe: 3
    fe: 2
    fe: 1
    ge: 1
  2. 整个过程中产生了几个执行上下文?  5
  */
```
* 测试题2
```js
  /*
   1:先预处理变量, 后预处理函数
   */
  function a() {}
  var a
  console.log(typeof a) // 'function'

  /*
   2:变量预处理, in操作符
   */
  if (!(b in window)) {
    var b = 1
  }
  console.log(b) // undefined

  /*
   3:预处理, 顺序执行
   */
  var c = 1
  function c(c) {
    console.log(c)
    var c = 3
  }
  c(2) // 报错
```
