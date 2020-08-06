---
title: 打水印命令convert详解
tags: 水印
categories: PHP
abbrlink: 6ab45c92
date: 2020-08-03 11:44:18
excerpt: 使用PHP扩展ImageMagick给图片打水印，convert...
---
打水印时主要用的是PHP扩展ImageMagick，该扩展专门用于处理图片，功能丰富，使用灵活，详细介绍可参看[官方文档](https://www.imagemagick.org/script/command-line-processing.php).

基本操作有打水印、裁剪、划线、画矩形、格式转换等。其中打水印命令最为复杂，下面对其中的参数和选项做个梳理。
```sh
convert +profile '*' source -quality 80 -resize '800x600'
water.png -gravity southeast -geometry +0+0 -composite
-fill rgba\(255,255,255,0.35\) -font fzltchjt.TTF
-pointsize 20 -stroke rgba\(0,0,0,0.22\) -strokewidth 1
-gravity SouthEast -draw "text 28,15 '贴图ID:188916'" dest
```
- +profile  
  Use `+profile profile_name` to remove the indicated profile.  
  `*`代表去除所有。但没弄懂profile是啥。
- source 原图片
- quality 质量，品质
- resize 重新设置大小，以上两项均针对原图片source
- water.png 水印图片
- southeast 和 geometry 指定图片叠加位置，遵循地理位置，上北下南左西右东，southeast就是右下角，geometry指定相对原点的偏移值，有很多写法，默认是 +0+0，可省略
- composite 代表用多个图片合并起来，这里应该是将两个图片（source和water.png）叠加起来
- (下面一些是对添加水印字体的设置)
- fill 字体颜色
- font 指定字体
- pointsize 字体大小，像素为单位
- stroke 描边颜色
- strokewidth 描边宽度
- -gravity SouthEast 第二个指定水印字体相对位置，此处如同上面相同可省略
- draw 绘制字体 text 28,15 代表相对水平和垂直位置，后面是具体值
- dest 目标输出图片

关于路径写法，绝对路径和相对路径都支持，但输出图片时不允许新建目录。

测试过部分参数，不知道理解的对不对，原参数实在太多了 -_-||
