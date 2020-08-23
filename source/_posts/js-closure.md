---
title: 8、JS中的闭包
tags: 闭包
categories: JS高级
excerpt: '闭包本质是内部函数中的一个对象, 这个对象中包含引用的变量属性'
abbrlink: 33819c82
date: 2020-08-22 16:58:19
---
## JS中的闭包
* 引入  
需求: 点击某个按钮, 提示"点击的是第 n 个按钮"
```js
var btns = document.getElementsByTagName('button')
for (var i = 0,length=btns.length; i < length; i++) {
    var btn = btns[i]
    //将btn所对应的下标保存在btn上
    btn.index = i
    btn.onclick = function () {
      alert('第'+(this.index+1)+'个')
    }
  }

  //利用闭包
  for (var i = 0,length=btns.length; i < length; i++) {
    (function (j) {
      var btn = btns[j]
      btn.onclick = function () {
        alert('第'+(j+1)+'个')
      }
    })(i)
  }
  ```
* 如何产生闭包?
  * 当一个嵌套的内部(子)函数引用了嵌套的外部(父)函数的变量(函数)时, 就产生了闭包
    * 函数嵌套
    * 内部函数引用了外部函数的数据(变量/函数)
* 闭包到底是什么?
  * 理解一: 闭包是嵌套的内部函数(绝大部分人)
  * 理解二: 包含被引用变量(函数)的对象(极少数人)
  * 注意: 闭包存在于嵌套的内部函数中
  * 闭包本质是内部函数中的一个对象, 这个对象中包含引用的变量属性
* 常见闭包
  * 1. 将函数作为另一个函数的返回值
  ```
  function fn1() {
    var a = 2;
    function fn2() {
      a++;
      console.log(a);
    }
    return fn2;
  }
  var f = fn1();
  f();
  f();
  ```
  * 2. 将函数作为实参传递给另一个函数调用
  ```
  function showDelay(msg, time) {
    setTimeout(function () {
      alert(msg)
    }, time)
  }
  showDelay('atguigu', 2000)
  ```
* 闭包的作用:
  * 使用函数内部的变量在函数执行完后, 仍然存活在内存中(延长了局部变量的生命周期)
  * 让函数外部可以操作(读写)到函数内部的数据(变量/函数)
  * 函数执行完后, 函数内部声明的局部变量是否还存在?  //一般是不存在, 存在于闭中的变量才可能存在
  * 在函数外部能直接访问函数内部的局部变量吗? //不能, 但我们可以通过闭包让外部操作它
* 闭包的生命周期
  * 产生: 在嵌套内部函数定义执行完时就产生了(不是在调用)
  * 死亡: 在嵌套的内部函数成为垃圾对象时，`f = null`
* 闭包应用:
  * 模块化: 封装一些数据以及操作数据的函数, 向外暴露一些行为
  ```js
  (function (window) {
  //私有的数据
  var msg = 'atguigu'
  var names = ['I', 'Love', 'you']
  //操作数据的函数
  function a() {
      console.log(msg.toUpperCase())
  }
  function b() {
      console.log(names.join(' '))
  }
  window.coolModule2 =  {
      doSomething: a,
      doOtherthing: b
  }
})(window)
  ```
  * 循环遍历加监听
  * JS框架(jQuery)大量使用了闭包
* 缺点:
  * 变量占用内存的时间可能会过长
  * 可能导致内存泄露
  * 解决:
    * 及时释放 : f = null; //让内部函数对象成为垃圾对象
*************
## 面试题
  * 1.
  ```js
  //代码片段一
var name = "The Window";
var object = {
  name : "My Object",
  getNameFunc : function(){
    return function(){
      return this.name;
    };
  }
};
alert(object.getNameFunc()());  //?  the window
//代码片段二
var name2 = "The Window";
var object2 = {
  name2 : "My Object",
  getNameFunc : function(){
    var that = this;
    return function(){
      return that.name2;
    };
  }
};
alert(object2.getNameFunc()()); //?  my object
  ```
  * 2.
  ```js
  function fun(n,o) {
  console.log(o)
  return {
    fun:function(m){
      return fun(m,n)
    }
  }
}
var a = fun(0)
a.fun(1)
a.fun(2)
a.fun(3)//undefined,0,0,0
var b = fun(0).fun(1).fun(2).fun(3)//undefined,0,1,2
var c = fun(0).fun(1)
c.fun(2)
c.fun(3)//undefined,0,1,1
  ```
***********
## 内存溢出与内存泄露
1. 内存溢出
  * 一种程序运行出现的错误
  * 当程序运行需要的内存超过了剩余的内存时, 就出抛出内存溢出的错误
2. 内存泄露
  * 占用的内存没有及时释放
  * 内存泄露积累多了就容易导致内存溢出
  * 常见的内存泄露:
    * 意外的全局变量
    * 没有及时清理的计时器或回调函数
    * 闭包
```js
// 1. 内存溢出
  var obj = {}
  for (var i = 0; i < 10000; i++) {
    obj[i] = new Array(10000000)
    console.log('-----')
  }
  // 2. 内存泄露
    // 意外的全局变量
  function fn() {
    a = new Array(10000000)
    console.log(a)
  }
  fn()
   // 没有及时清理的计时器或回调函数
  var intervalId = setInterval(function () { //启动循环定时器后不清理
    console.log('----')
  }, 1000)
  // clearInterval(intervalId)
    // 闭包
  function fn1() {
    var a = 4
    function fn2() {
      console.log(++a)
    }
    return fn2
  }
  var f = fn1()
  f()
  // f = null
```
