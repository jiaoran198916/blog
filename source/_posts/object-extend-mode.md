---
title: 10、对象继承模式
tags: 继承
categories: JS高级
excerpt: JS中对象的常见继承模式
abbrlink: c75e301c
date: 2020-09-05 18:02:06
---
总共3种。
## 方式1: 原型链继承
 * 子类型的原型为父类型的一个实例对象

```js
//父类型
  function Supper() {
    this.supProp = 'Supper property'
  }
  Supper.prototype.showSupperProp = function () {
    console.log(this.supProp)
  }

  //子类型
  function Sub() {
    this.subProp = 'Sub property'
  }

  // 子类型的原型为父类型的一个实例对象
  Sub.prototype = new Supper()
  // 让子类型的原型的constructor指向子类型
  Sub.prototype.constructor = Sub
  Sub.prototype.showSubProp = function () {
    console.log(this.subProp)
  }
  var sub = new Sub()
  sub.showSupperProp()
  // sub.toString()
  sub.showSubProp()
```
****************
## 方式2: 借用构造函数继承(假的)
  * 在子类型构造函数中通用call()调用父类型构造函数

```js
  function Person(name, age) {
    this.name = name
    this.age = age
  }
  function Student(name, age, price) {
    Person.call(this, name, age)  // 相当于: this.Person(name, age)
    /*this.name = name
    this.age = age*/
    this.price = price
  }
```
******************
## 方式3: 原型链+借用构造函数的组合继承
  * 利用原型链实现对父类型对象的方法继承
  * 利用 call() 借用父类型构建函数初始化相同属性

```js
function Person(name, age) {
  this.name = name
  this.age = age
}
Person.prototype.setName = function (name) {
  this.name = name
}

function Student(name, age, price) {
  Person.call(this, name, age)  // 为了得到属性
  this.price = price
}
Student.prototype = new Person() // 为了能看到父类型的方法
Student.prototype.constructor = Student //修正constructor属性
Student.prototype.setPrice = function (price) {
  this.price = price
}

var s = new Student('Tom', 24, 15000)
s.setName('Bob')
s.setPrice(16000)
```
