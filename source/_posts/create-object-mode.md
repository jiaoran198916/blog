---
title: 9、对象创建模式
tags: object
categories: JS高级
abbrlink: a879112e
date: 2020-08-29 11:35:11
---
一共5种，除了工厂函数不常用外，其他都很常用。
## 方式一: Object构造函数模式
  * 套路: 先创建空Object对象, 再动态添加属性/方法
  * 适用场景: 起始时不确定对象内部数据
  * 问题: 语句太多

```
var obj = new Object()
obj.name = 'Tom'
obj.setName = function(name){this.name=name}
```
****************
## 方式二: 对象字面量模式
  * 套路: 使用{}创建对象, 同时指定属性/方法
  * 适用场景: 起始时对象内部数据是确定的
  * 问题: 如果创建多个对象, 有重复代码

```
var p = {
  name: 'Tom',
  age: 12,
  setName: function (name) {
    this.name = name
  }
}
```
  ****************
## 方式三: 工厂模式
  * 套路: 通过工厂函数动态创建对象并返回
  * 适用场景: 需要创建多个对象
  * 问题: 对象没有一个具体的类型, 都是Object类型

```
function createPerson(name, age) {
  var obj = {
    name: name,
    age: age,
    setName: function (name) {
      this.name = name
    }
  }
  return obj
}
```
  ****************
## 方式四: 自定义构造函数模式
  * 套路: 自定义构造函数, 通过new创建对象
  * 适用场景: 需要创建多个类型确定的对象
  * 问题: 每个对象都有相同的数据, 浪费内存

```
function Person(name, age) {
  this.name = name;
  this.age = age;
  this.setName = function(name){this.name=name;};
}
new Person('tom', 12);
```
  ****************
## 方式五: 构造函数+原型的组合模式
  * 套路: 自定义构造函数, 属性在函数中初始化, 方法添加到原型上
  * 适用场景: 需要创建多个类型确定的对象

```
function Person(name, age) {
   this.name = name
   this.age = age
}
Person.prototype.setName = function (name) {
   this.name = name
}
new Person('Tom', 23)
```
