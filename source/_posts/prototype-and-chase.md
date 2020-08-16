---
title: 5、原型与原型链
tags: prototype
categories: JS高级
excerpt: '每个函数都有一个 `prototype` 属性, 默认指向一个Object空对象, 即原型对象'
abbrlink: e8f85541
date: 2020-08-16 10:57:20
---
* 显式原型与隐式原型
  * 每个函数都有一个 `prototype` 属性, 称为显式原型属性，默认指向一个 Object空对象, 即原型对象
  * 原型对象中有一个属性 constructor, 它指向函数对象
  * 所有实例对象都有一个特别的属性，`__proto__`，称为隐式原型属性
* 显式原型与隐式原型的关系
  * 函数的prototype: 定义函数时被自动赋值, 值默认为{}, 即用为原型对象
  * 实例对象的__proto__: 在创建实例对象时被自动添加, 并赋值为构造函数的prototype值
  * 原型对象即为当前实例对象的父对象
  * 给原型对象添加属性(一般是方法), 实例对象可以访问
* 原型链
  * 所有的实例对象都有__proto__属性, 它指向的就是原型对象
  * 这样通过__proto__属性就形成了一个链的结构---->原型链
  * 当查找对象内部的属性/方法时, js引擎自动沿着这个原型链查找,如果最终没找到, 返回undefined
  * 当给对象属性赋值时不会使用原型链, 而只是在当前对象中进行操作
* 注意
  * 函数的显示原型指向的对象默认是空Object实例对象(但Object不满足)
  * 所有函数都是Function的实例(包含Function) ，Function是通过new自己产生的实例
  `Function = new Function()`
  * Object的原型对象是原型链尽头  
  `Object.prototype.__proto__ === null`
* 探索 instanceof
  * 表达式: A instanceof B
  * 如果B函数的显式原型对象在A对象的原型链上, 返回true, 否则返回false
    ```js
    console.log(Object instanceof Function) // true
    console.log(Object instanceof Object) // true
    console.log(Function instanceof Function) // true
    console.log(Function instanceof Object) // true
    ```
*************
* 测试题1.
  ```js
  function A () {
  }
  A.prototype.n = 1
  var b = new A()
  A.prototype = {
    n: 2,
    m: 3
  }
  var c = new A()
  console.log(b.n, b.m, c.n, c.m)
  ```
* 测试题2.
  ```js
   function F (){}
   Object.prototype.a = function(){
     console.log('a()')
   }
   Function.prototype.b = function(){
     console.log('b()')
   }
   var f = new F()
   f.a()
   // f.b()
   F.a()
   F.b()
   console.log(f)
   console.log(Object.prototype)
   console.log(Function.prototype)
   ```
