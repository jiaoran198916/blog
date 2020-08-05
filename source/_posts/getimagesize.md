---
title: getimagesize()获取图片尺寸等信息
tags: getimagesize
categories: PHP
abbrlink: 7495c85b
date: 2020-08-05 11:25:16
---
## 定义
getimagesize - 获取图片尺寸
## 语法
```php
getimagesize ( string $filename [, array &$imageinfo ] ) : array
```
返回一个 **关联** 数组，包含指定图片的相关信息。    
$filename 可以是本地也可以是远程图片。  
$imageinfo 用于获取更多扩展信息，只支持 JFIF 文件。
## 返回值
返回数组中最多可以包含7个元素，分别如下:

索引 `0`，`1`分别是宽度和高度；  
索引 `2`是图片的类型，是格式如 IMAGETYPE_XXX 的预定义常量之一，如IMAGETYPE_GIF, IMAGETYPE_JPEG, IMAGETYPE_PNG, IMAGETYPE_BMP；  
索引 `3` 是宽高的拼接好的字符串，如height="yyy" width="xxx"，方便直接用在img标签里；   
`mime` 是对应的MIME 类型，可用于http头信息，如 `header("Content-type: {$size['mime']}");`;

`channels` will be 3 for RGB pictures and 4 for CMYK pictures.  
`bits` is the number of bits for each color.
*************
## 示例
```php
$image = 'https://avatars2.githubusercontent.com/u/646129?s=52&v=4';
$data = getimagesize($image, $info);
print_r($data);
print_r($info);
```
输出
```php
Array
(
    [0] => 52
    [1] => 52
    [2] => 2
    [3] => width="52" height="52"
    [bits] => 8
    [channels] => 3
    [mime] => image/jpeg
)
Array
(
    [APP0] => JFIF``
)
```
## 总结
一般常用于获取图片宽高，其他信息基本用不到。  
名称是image size，但不知道返回的是图片的实际大小还是图片的尺寸，而且既然已经返回这么多信息了，为啥不返回图片的字节大小呢，虽然可以通过其他方式获取，但如果能一步到位岂不更省事。
