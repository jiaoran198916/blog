---
title: wc命令详解
tags:
  - wc
  - count
categories: Linux
excerpt: 统计给定文件的字符数、行数、字节数
abbrlink: 682def49
date: 2020-08-24 14:45:29
---
## NAME
wc -- word, line, character, and byte count  
计算给定文件的字符数、行数、字节数等
************
## SYNOPSIS
```
wc [-clmw] [file ...]
```
如果没有指定文件，则使用默认输入，如ls。
************
## DESCRIPTION

- -c  
  输入文件的字节数，byte，characters；
- -l  
    输入文件的行数, line;
- -m  
    输入文件的字符数, multi-byte characters;
- -w  
    输入文件的words数;
默认选项是 -c, -l and -w
************
## EXAMPLES
```
wc -mlw report1 report2
```
