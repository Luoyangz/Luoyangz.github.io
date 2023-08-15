---
title: 浅谈css滤镜-filter
top: false
cover: false
toc: true
mathjax: true
tags: ['css-filter']
categories: ['html','css']
date: 2022-08-25 21:38:27
password:
summary:	'浅谈css滤镜-filter'
coverImg:
img:
---

## css-filter
PS：filter有js的数组的filter方法，也有css的filter属性，我这里只谈论css的属性，查看数组filter，请点击<a href="/2022/08/25/js数组遍历方法/#toc-heading-4"><font color="red">这里</font></a>跳转

filter是css的滤镜属性，一般用于图片的处理（如亮度、模糊度、饱和度等），也可以用于基本的dom处理

> filter的兼容性

![filter兼容性](https://cdn.jsdelivr.net/gh/ZhjDestiny/other/20220825-1.png)

> filter的属性介绍

|  属性名   | 描述  |
|  ----  | ----  |
| none  | 默认值，无效果 |
| blur  | 设置一个dom的高斯模糊程度，格式：filter:blur({a}px)，默认值为0，其中a为正数，可以为小数，数值越大越模糊 |
| brightness  | 设置一个dom的亮度，格式：filter:brightness({a})，默认值为1，其中a为正数，可以为小数，小数越小表示越暗，0为黑色，1是正常亮度，可以比大于1，越大越亮 |
| contrast  | 设置一个dom的对比度，格式：filter:contrast({a})，参数同brightness一样 |
| drop-shadow  | 设置一个dom的阴影，格式：filter:drop-shadow({a})，参数同box-shadow一样，跟boxShadow对比可看出，本属性可对于非规则的元素每一个点都添加阴影 |
| grayscale  | 设置一个dom的灰度，格式：filter:grayscale({a})，默认值0，范围在0-1之间，0表示无变化，1表示完全为灰色 |
| hue-rotate  | 设置一个dom的色相值旋转，格式：filter:hue-rotate({a}deg)，默认值0，无最大最小值，可以理解为一个圈，超过360deg相当于重新开始，简单理解为从0到180即是从黑到白，然后180到360是从白到黑 |
| invert  | 设置一个dom的反转输入，格式：filter:invert({a})，默认值0，范围在0-1之间，0表示无变化，1表示完全反转 |
| opacity  | 设置一个dom的透明度，格式：filter:opacity({a})，默认值1，范围在0-1之间，0表示完全透明 |
| saturate  | 设置一个dom的饱和度，格式：filter:saturate({a})，默认值1，参数同对比度contrast |
| sepia  | 设置一个dom的深褐色，格式：filter:sepia({a})，默认值0，参数同灰色grayscale |

> filter属性例子对比

![filter例子对比](https://cdn.jsdelivr.net/gh/ZhjDestiny/other/20220825-2.jpg)

### 在线预览

在线预览效果地址：<u>[点击预览](https://codepen.io/luoyangz/pen/QWmRPEM)</u>（注：本文所用图片外链皆是cdn.jsdelivr.net，有时候可能会打不开，有梯子的挂个梯子就好，没有就😂😂😂）

### <p style="color:red;">注意</p>
<p style="color:#42b983">filter有个很有意思的属性，就是drop-shadow。从上方效果对比图可看出，drop-show可以对非规则的图片添加描边的阴影，而box-shadow只能对容器本身添加阴影，这是个很有意思的点。😄😄😄<p>