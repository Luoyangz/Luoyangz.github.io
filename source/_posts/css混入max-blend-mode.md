---
title: css混入之max-blend-mode
top: false
cover: false
toc: true
mathjax: true
tags: ['max-blend-mode']
categories: ['css']
date: 2022-08-26 20:40:52
password:
summary:	'max-blend-mode'
coverImg:
img:
---

## max-blend-mode

max-blend-mode意为混入，是css的一个属性，他描述了元素的内容应该与元素的直系父元素的内容和元素的背景如何混合。<u><font color="#42b983">简单来讲就是说两个或者多个dom在重叠之处的显示效果。</font> </u>

> max-blend-mode的兼容性

![max-blend-mode兼容性](https://cdn.jsdelivr.net/gh/ZhjDestiny/other/2022826-1.png)

> max-blend-mode的属性介绍

|  属性名  | 描述  |
|  ----  | ----  |
| normal  | 正常模式 |
| multiply  | 正片叠底 |
| screen  | 滤色 |
| overlay  | 叠加 |
| darken  | 变暗 |
| lighten  | 变亮 |
| color-dodge  | 颜色减淡 |
| color-burn  | 颜色加深 |
| hard-light  | 强光 |
| soft-light  | 柔光 |
| difference  | 差值 |
| exclusion  | 排除 |
| hue  | 色相 |
| saturation  | 饱和度 |
| color  | 颜色 |
| luminosity  | 亮度 |

> 使用
> 1.可以用于文字的一些特殊效果，比如在一个动态文字在不同的背景色调下显示不同的颜色，可以使用css直接实现
> 2.也可用于图片的混合，或者背景的混合（背景混合属性：background-blend-mode，参数类似于混合），有点儿像css滤镜-filter的效果，不过filter是针对于一个dom整体的更改，而混合是针对于两个dom在重叠的地方显示的方式


### 在线预览

在线预览效果地址：<u>[点击预览](https://codepen.io/luoyangz/pen/MWVdxwe)</u>