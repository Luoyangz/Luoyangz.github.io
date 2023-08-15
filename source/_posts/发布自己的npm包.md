---
title: 发布自己的npm包
top: false
cover: false
toc: true
mathjax: true
tags: ['npm']
categories: ['js']
date: 2023-8-14 17:37:53
password:
summary: 如何发布自己的npm包
coverImg:
img:
---


# 发布属于自己的npm包

## 1. 创建npm账号
想要发布npm包，首先肯定要有自己的npm账号，[npm官网]( https://www.npmjs.com/)，注册过程不多赘述，自己去注册即可

## 2. 创建项目
 新建一个项目（默认了你已经安装的node），名字自己可以随便定义，我这里以`my-npm-package`为例，进入项目开始操作
> npm init

提示输入npm包的名字，以及描述，作者等信息，按照提示输入，，最后输入y即可，也可以一直回车空着先初始化完成之后在填写，我这里建议一直回车后面在修改更改直观到此初始化完成，然后看文件夹中生成了一个package.json文件，这个里面保存了包的各种配置信息。

> 看一下package.json文件
```json
	{
		"name": "zhj.js",	// 包的名字
		"version": "1.0.1",	// 包的版本号
		"description": "zhj的个人公用js",	// 包的描述
		"main": "index.js",	//主入口文件，默认值是模块根目录下面的 index.js
		"repository": {	// 存储仓库类型
			"type": "git",
			"url": "git+https://github.com/Chulushan/zhj.js"
		},
		"keywords": [	// 在npm社区的搜索关键字
			"zhj"
		],
		"author": "zhj",	// 作者
		"license": "ISC",	//使用ISC作为许可证
		"bugs": {
			"url": "https://github.com/Chulushan/zhj.js/issues"	// 提issues地址
		},
		"homepage": "https://github.com/Chulushan/zhj.js"	// 包主页
	}
```

> 新建入口文件index.js以及readme.md文件

这里根据自己的需要编写自己的包内容，以及md说明，这里我稍微展示一下自己的包内容，我的包导出了各种我自己常用的方法
```javascript
	/**
	* 数组或数组对象去重
	* @param {array} val1 需要去重的数组
	* @param {string} val2 唯一标识字段
	* @returns {array} 返回去重之后的数组
	*/
	export function distinctArr(val1, val2) {...}
```
<font color="#42b983">PS：这里方法最好使用这种写法，这样在引入的时候，用户将鼠标放到方法名上，可以很方便的知道这个方法是做什么用的，以及参数是什么，返回值是什么。😎😎😎</font>

> 最终我的包目录结构是这样的（一个文件夹里面三个文件）

+ my-npm-package
	- index.js （入口文件）
	- readme.md （说明文件）
	- package.json （包配置文件）

> 上传到git
	
包发布之前需要将内容上传到git仓库，就是需要确保git上面有你配置文件里的仓库地址

> 注意事项

* <font color="red">包的命名规则</font>
	* 包名长度不能超过 214 个字符（命名空间也算在里面）
	* 包名必须是小写字母，不能包含空格，不能以.或-开头（中间可以有）
	* 包名不能使用node的保留关键字，如http等
	* 包名不能以node的模块名开头，比如fs、path
	* 包名不能包含node_modules
	* 包名如果以@开头，默认会识别为私有包，需要收费（一般格式为@name/baoming），也可在发布的时候特别注明是公有包，或者在配置文件中添加配置，[详情点击这里查看](#rule)
* 包的入口文件
	* 包的入口文件默认为根目录下的index.js，也可自定义

## 3. 发布

发布之前需要登录自己的npm账号

> npm login

根据提示自己填写，账号密码邮箱啥的，有时候可能需要填写验证码，去自己绑定的邮箱查看，登录成功会提示：`Logged in as yourName on https://registry.npmjs.org/`，此时就登录成功了，这个时候我们就可以发布了。

> npm version 1.0.1

发布的版本号，第一次发布不需要这个，默认是1.0.0版本，之后每次更新根据下面的规则，先确定版本在发布就行
* <font color="red">包的版本号规则</font>
	* 版本号格式：主版本号.次版本号.修订号（如：1.2.3这种），<font color="red">版本号只能递增</font>
	* 版本号递增规则：
		* 主版本号：当你做了不兼容的 API 修改，一般都是大的版本迭代比如vue2至vue3这种
		* 次版本号：当你做了向下兼容的功能性新增，新增了一些功能之类的
		* 修订号：当你做了向下兼容的问题修正，未新增只是改了这种

> npm publish

发布成功会提示：<u><font color="#42b983">+ my-npm-package@1.0.1</font> </u>，此时就发布成功了，去npm官网查看，发现已经发布了。

> <a id="rule">发布注意事项</a> 
* 发布之前要确保配置文件中的git仓库是存在的，否则会报错
* 要确保源地址为官方地址`http://registry.npmjs.org`或`https://registry.npmjs.com`， 可以通过 npm config get registry 命令查看当前 registry 源，如果不是可通过以下四种方式修改
	* 1、在全局配置 .npmrc ，可通过命令 `npm config set registry=http://registry.npmjs.org/ `
	* 2、在当前项目中添加配置文件.npmrc，里面内容为
		```
			registry = http://registry.npmjs.org/
		```
	* 3、发布包时指定 --registry 选项，`npm publish —registry=http://registry.npmjs.org/`
	* 4、在当前项目的 package.json 中通过 publishConfig 字段指定
		```
			"publishConfig": {
				"registry": "http://registry.npmjs.org/"
			}
		```
* 如果想要发布带有命名空间的包，有两种方法
	* 1、发布命令npm publish --access public，指出这是个公有包
	* 2、package的pbulishConfig字段中添加access字段
		```
			"publishConfig": {
				"access": "public"
			}
		```

## 4. 我的包地址

我自己的包：<u>[点击查看](https://www.npmjs.com/package/zhj.js?activeTab=readme)</u>

