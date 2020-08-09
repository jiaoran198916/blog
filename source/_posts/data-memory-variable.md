---
title: 2、数据、内存和变量
tags: 内存
categories: JS高级
excerpt: JS中数据、内存和变量的理解和相关问题
abbrlink: '95830350'
date: 2020-08-08 20:47:22
---
1. 什么是数据?
  * 存储在内存中代表特定信息的'东东', 本质上是0101...
  * 数据的特点: 可传递, 可运算
  * 一切皆数据, 函数也是数据
  * 内存中所有操作的目标: 数据
    * 算术运算
    * 逻辑运算
    * 赋值
    * 运行函数
*********************
2. 什么是内存?
  * 内存条通电后产生的可储存数据的空间(临时的)
  * 内存产生和死亡: 内存条(电路版)==>通电==>产生内存空间==>存储数据==>处理数据==>断电==>内存空间和数据都消失
  * 一块小内存的2个数据
     * 内部存储的数据(一般数据/地址数据)
     * 地址值数据
  * 内存空间的分类
    * 栈: 全局变量/局部变量
    * 堆: 对象(空间较大)
*********************
3. 什么是变量?
  * 在程序运行过程中值是允许改变的量, 由变量名和变量值组成
  * 每个变量都对应的一块小内存, 变量名用来查找对应的内存, 变量值就是内存中保存的数据

  * 数据, 内存和变量三者之间的关系
    * 内存是容器, 用来存储不同数据
    * 变量是内存的标识, 通过变量我们可以操作(读/写)内存中的数据
*********************
4. 相关问题
* 关于赋值和内存的问题  
    问题: var a = xxx, a内存中到底保存的是什么?
    * xxx是基本数据, 保存的就是这个数据
    * xxx是对象, 保存的是对象的地址值
    * xxx是一个变量, 保存的xxx的内存内容(可能是基本数据, 也可能是地址值)
* 关于引用变量赋值问题
  * 2个引用变量指向同一个对象, 通过一个变量修改对象内部数据, 另一个变量看到的是修改之后的数据
  ```js
  var obj1 = {name: 'Tom'}
  function fn (obj) {
    obj.name = 'A' //操作对象
  }
  fn(obj1)
  console.log(obj2.name) //A
  ```
  * 2个引用变量指向同一个对象, 让其中一个引用变量指向另一个对象, 另一引用变量依然指向前一个对象
  ```js
  a = {name: 'BOB', age: 13}
  function fn2 (obj) {
    obj = {age: 15} //重新赋值
  }
  fn2(a)
  console.log(a.age) // 13
  ```
* 关于数据传递问题   
问题: 在调用函数时传递变量参数时, 是值传递还是引用传递？
  * 理解1: 都是值(基本/地址值)传递
  * 理解2: 可能是值传递, 也可能是引用传递(地址值)
* 内存管理   
问题: JS引擎如何管理内存?
  1. 内存生命周期  
    * 分配小内存空间, 得到它的使用权
    * 存储数据, 可以反复进行操作
    * 不需要时将其释放/归还
  2. 释放内存
    * 为执行函数分配的栈空间内存: 函数执行完 **自动释放**
    * 存储对象的堆空间内存: 成为垃圾对象==> **垃圾回收器回收**