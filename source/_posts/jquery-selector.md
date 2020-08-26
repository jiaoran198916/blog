---
title: jQuery选择器
tags:
  - selector
  - attribute
categories: jQuery
excerpt: jQuery常用选择器
abbrlink: ca11ba0c
date: 2020-08-26 11:12:54
---
## 基础选择器（Basic）
* $("\*") 所有标签
* $(".className")
* $("#id")
* $("标签名")
* $("selector1, selector2, selectorN")

## 根据标签层级关系（Hierarchy）
* Child Selector: 匹配 parent 的直接 child
  `jQuery( "parent > child" )`
* Descendant Selector: 匹配ancestor下面的所有 descendant
  `jQuery( "ancestor descendant" )`
* Next Adjacent Selector: 捕获的是 prev 后最近的兄弟 next ，并且必须是直接的兄弟标签
  `jQuery( "prev + next" )`
* Next Siblings Selector: 匹配 prev 后的所有兄弟 siblings 同级关系
  `jQuery( "prev ~ siblings" )`

## 根据属性（Attribute）
写法有如下四种，具体哪一种根据个人习惯。
- double quotes inside single quotes: $('a[rel="nofollow self"]')
- single quotes inside double quotes: $("a[rel='nofollow self']")
- escaped single quotes inside single quotes: $('a[rel=\'nofollow self\']')
- escaped double quotes inside double quotes: $("a[rel=\"nofollow self\"]")

* Has Attribute Selector: 是否包含某属性
  `jQuery( "[attribute]" )`
* Attribute Equals Selector: 属性是某一具体值
  `jQuery( "[attribute='value']" )`
* Attribute Starts With Selector: 属性以某值开头
  `jQuery( "[attribute^='value']" )`
* Attribute Ends With Selector: 属性以某值结尾
  `jQuery( "[attribute$='value']" )`
* Attribute Contains Selector: 属性包含某值
  `jQuery( "[attribute*='value']" )`

## 基础过滤器（Basic Filter）
根据函数捕获对象，就是选择器选择到对象后进行二次筛选。
* :eq() Selector: 下标等于某个值
  `jQuery( ":eq(index)" )`
* :even Selector: 偶数
  `jQuery( ":even" )`
* :odd Selector: 奇数
  `jQuery( ":odd" )`
* :gt() Selector: 大于某个值
  `jQuery( ":gt(index)" )`
* :lt() Selector: 小于某个值
  `jQuery( ":lt(index)" )`
* :first Selector: 第一个元素
  `jQuery( ":first" )`
* :last Selector: 最后一个元素
  `jQuery( ":last" )`
* :not() Selector: 排除，非
  `jQuery( ":not(selector)" )`

## 根据子节点过滤（Child Filter）
根据函数捕获对象，就是选择器选择到对象后进行二次筛选。
* :first-child Selector: 第一个子节点
  `jQuery( ":first-child" )`
* :last-child Selector: 最后一个子节点
  `jQuery( ":last-child" )`
* :nth-child() Selector: 子节点索引，从1开始
  `jQuery( ":nth-child(index/even/odd/equation)" )`

## 根据表单控件（Form）
根据表单元素的类型等获取对象。
* :checkbox Selector: 所有的复选框
  `jQuery( ":checkbox" )`
* :checked Selector: checked or selected
  `jQuery( ":checked" )`

## 根据可见性（Visibility Filter）
根据元素是否可见，共有两个。
* :hidden Selector: 隐藏
  `jQuery( ":hidden" )`
* :visible Selector: 可见
  `jQuery( ":visible" )`
