---
title: package.json的思考
top: false
cover: false
toc: true
mathjax: true
tags: ['配置项']
categories: ['vue','react']
date: 2023-6-5 16:08:44
password:
summary:	由element版本更新产生的bug引起针对于package.json的思考
coverImg:
img:
---

# 由element版本更新产生的bug引起针对于package.json的思考

## 问题的产生
* 在项目开发过程中，某次提交代码后jenkins发布后element-plus的le-tabs组件出现了样式错误，排查后发现是.el-tabs__item这个类由以前的inline-block变成了flex布局，后来排查了下版本发现我本地的版本是2.2.12，然后打包出来是最新的2.3.5版本

## -S/--save/-d/-D/--save-dev的区别
<font color="red">以下所有的命令都省略了依赖的名称</font>

> npm install 或 npm install -S 或npm install  --save（yarn add 一般没有-s、-d）
* 其实这些命令都是一个意思（npm在5之后默认支持了--save），都是将装入package.json的dependencies下（这个是项目运行所需要的库，可以理解为生产依赖）

> npm install -d 或 npm install -D 或npm install  --save--dev
* 这些会将依赖装入package.json的devDependencies下（这是开发环境下的依赖库，一般都是些vite、node、babel、ts、less这些东西我们在开发的时候所用到的，毕竟打包之后包是不需要这些东西的）

> npm install -g
* 全局安装的我们一般在装vue或者react这种脚手架的会全局安装，安装项目内的依赖库一般不这样子使用

## package-lock.json与yarn.lock
1. 前者是npm install产生的依赖缓存文件，而后者是yarn install产生的依赖缓存文件
2. 如果我们没有改动package.json的依赖文件，那么我们install的话就是只读取lock文件的版本来安装依赖，如果有改动的话，他将会绕过lock，依据package.json的依赖版本文件配置来安装依赖。

##	package.json的改动
* 如果我们改动了某些依赖项的版本后者更新规则，如果存在node_modules的话，将会只更新我们改动的依赖，否则将会全部重新更新
```javascript
	"dependencies": {
		"axios": "^0.27.2",
		"echarts": "^5.4.0",
		"element-plus": "~2.2.12",
	},	
	// 举个例子：版本号一般都是1.1.2这中情况，第一个1表示主版本，第二个1表示次版本，第三个2表示修订版本
	//          ^这个图标表示该依赖每次install主版本不能变，次版本与修订版本向上兼容，表示可以是1.1.n，或者1.2.n，1.3.n
	//		   	  ~这个图标表示该依赖每次install主次版本不能变，只能变修订版本，表示可以是1.1.3，1.1.4，1.1.n...
	//		     不加图标只有版本号表示每次install固定死这个版本
```
## 看我们最初的问题
> &emsp;&emsp;为什么我们本地是package.json的版本是2.2.12，但是jenkins打包之后是2.3.5，原因就在于我这里jenkins的打包配置每次都会重新去install一下，而我们的element-plus版本设置了^，导致更新会向上更新获取最新的版本，然后我版本更新设置了~，也就是只更新修订版本，不更新次版本，然后只更新到了2.2.36，就没有了那个问题。

## 总结
 &emsp;&emsp; 项目开发过程中总会遇见各种各样自奇怪的问题，怎么找到问题产生的原因，以及问题解决的思路这个是最重要的！！！


