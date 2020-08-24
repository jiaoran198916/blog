---
title: awk命令详解
tags:
  - awk
categories: Linux
abbrlink: cf83d80f
date: 2020-08-24 15:01:16
---
awk是一个强大的文本分析工具，是把文件逐行的读入，以空格为默认分隔符将每行切片，切开的部分再进行各种分析处理。
<!--more -->
awk其名称得自于它的创始人 `Alfred Aho` 、`Peter Weinberger` 和 `Brian Kernighan` 姓氏的首字母。实际上 AWK 的确拥有自己的语言： AWK程序设计语言，三位创建者已将它正式定义为“样式扫描和处理语言”。它允许您创建简短的程序，这些程序读取输入文件、为数据排序、处理数据、对输入执行计算以及生成报表，还有无数其他的功能。
*******
## 命令行
```
awk [-F  field-separator]  'commands'  input-file(s)
```
其中，commands 是真正awk命令，[-F域分隔符]是可选的。 input-file(s) 是待处理的文件。
在awk中，文件的每一行中，由域分隔符分开的每一项称为一个域。默认的域分隔符是空格。
***********
## 示例1
获取当前目录下所有文件大小
```
ls -l |awk '{print $5}'
```
读入有"\n"换行符分割的一条记录，然后将记录按指定的域分隔符划分域，填充域，$0则表示所有域,$1表示第一个域,$n表示第n个域。所以$5表示文件大小以此类推。
********
## 示例2
显示 /etc/passwd 的账户和账户对应的shell，而账户与shell之间以tab键分割，并且在所有行前添加列名name,shell,在最后一行添加"blue,/bin/nosh"
```
cat /etc/passwd |awk  -F ':'  'BEGIN {print "name,shell"}  {print $1","$7} END {print "blue,/bin/nosh"}'
```
********
## 示例3
搜索/etc/passwd有root关键字的所有行
```
awk -F: '/^root/' /etc/passwd
```
pattern的使用示例，匹配了pattern(这里是以root开头)的行才会执行action(没有指定action，默认输出每行的内容)。
********
## 示例4
统计/etc/passwd:文件名，每行的行号，每行的列数，对应的完整行内容
```
awk  -F ':'  '{print "filename:" FILENAME ",linenumber:" NR ",columns:" NF ",linecontent:"$0}' /etc/passwd
```
FILENAME，NR，NF是内置变量，常用变量如下
- ARGC               命令行参数个数
- ARGV               命令行参数排列
- ENVIRON            支持队列中系统环境变量的使用
- FILENAME           awk浏览的文件名
- FNR                浏览文件的记录数
- FS                 设置输入域分隔符，等价于命令行 -F选项
- NF                 浏览记录的域的个数
- NR                 已读的记录数
- OFS                输出域分隔符
- ORS                输出记录分隔符
- RS                 控制记录分隔符

结果：
```
filename:/etc/passwd,linenumber:1,columns:7,linecontent:root:x:0:0:root:/root:/bin/bash
```
使用printf替代print，可以让代码更加简洁，易读
```
awk  -F ':'  '{printf("filename:%10s,linenumber:%s,columns:%s,linecontent:%s\n",FILENAME,NR,NF,$0)}' /etc/passwd
```
##  awk编程
略，留给运维同学去研究。
*******
awk编程的内容超级多，更多请参考 [The GNU Awk User’s Guide](http://www.gnu.org/software/gawk/manual/gawk.html)
