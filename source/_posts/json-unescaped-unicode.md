---
title: JSON_UNESCAPED_UNICODE的作用与理解
tags:
  - Json
categories:
  - PHP
abbrlink: 8157d8ea
date: 2020-08-03 10:11:21
---
## 背景
在使用json_encode转换的时候，默认情况下中文会转换成 `\u***` 的格式, 不仅不可读，还会在一定程度上增加传输的数据量.
```
<?php
echo json_encode("中文");
//"\u4e2d\u6587"
```
在PHP5.4, 这个问题得以解决, Json新增了一个选项: JSON_UNESCAPED_UNICODE,加上之后就可以正确输出中文。
详见鸟哥的文章，[让Json更懂中文](https://www.laruence.com/2011/10/10/2239.html)
## 总结
对这个选项的作用和用法都没有歧义，有点不同的是对这个组合词 JSON_UNESCAPED_UNICODE 的理解，鸟哥文章中说是"顾名思义，不要编码Unicode"，实际上并这里的意思并不明显，escape是避开，避免的意思，前面加上 un 表示否定，是不要避开不要避免，应该是说把Unicode当成本身处理，不要避开Unicode这种字符或格式，即承认它，再结合官网对这个选项的解释，(逐个字符的编码多字节Unicode字符)
`Encode multibyte Unicode characters literally (default is to escape as \uXXXX).`
，虽然最后结果是一样的，但从字义上其实很难一下子看出来。
