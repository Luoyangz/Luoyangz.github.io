---
title: mutationObserver与resizeObserver
top: false
cover: false
toc: true
mathjax: true
tags: ['observe']
categories: ['html','js']
date: 2023-8-23 10:15:22
password:
summary:	'监听dom的所有变化'
coverImg:
img:
---
## mutationObserver

<strong>该方法是观察dom的变化，可以监听dom本身的一些变化，包括文本、属性、子节点与所有后代节点的变动，需要注意的是 <font color="red">该方法是异步触发的</font>，观察的dom发生变动后不会立即触发，而是当dom停止变动后才会触发。</strong>

异步的原因是，dom的变化常常都不是单个因素的变化，如果每个变化都触发一次观察器，那么性能消耗会很大，所以mutationObserver是当dom停止变动后才会触发。可以想象往通过遍历往dom中添加成百上千的子节点，这是比较消耗性能的🤣🤣🤣。

### 兼容性

兼容性非常好，可以无压力使用，[点击查看](https://caniuse.com/mutationobserver)

### 新建观察器

```js
	const observer = new MutationObserver(callback)
	const config = {
		childList：true,
		attributes：true,
		characterData：true,
		subtree：true,
	}
	observer.observe(dom, config)	// 开启观察
```
观察器的回调函数callback在每次dom变化完成后触发，而观察期本身observer接受两个参数，第一个是观察的dom，第二个是配置对象，可以观察变动的属性，包括：
- <font color="red">childList</font>：子节点的变动，包括新增节点和删除节点
- <font color="red">attributes</font>：属性的变动
- <font color="red">characterData</font>：节点内容或节点文本的变动
- <font color="red">subtree</font>：所有后代节点的变动
需要观察哪个变动就添加哪个设置为true即可，PS：<font color="#42b983">不能单独观察subtree，必须同时设置childList、attributes、characterData一个或多个为true。</font>

除了这些属性外，也可以配置以下属性：
- <font color="red">attributeOldValue</font>：布尔类型，观察属性的变动，并记录变动前的属性值
- <font color="red">characterDataOldValue</font>：布尔类型，观察文本节点或节点文本的变动时，记录变动前的值
- <font color="red">attributeFilter</font>：数组，观察特定属性，例如["class","id","title"]等

### 停止观察 disconnect()与takeRecords()

```js
	observer.disconnect()	// 停止观察
	observer.takeRecords()	// 停止观察且返回该观察到的所有变动记录
```

## resizeObserver

<strong>该方法是观察dom的所有尺寸变化，包括但不限于宽高，边框之类的尺寸变化，<font color="red">同步触发</font>其实观察元素的尺寸的话，window.resize也是可以的，当窗口变化的时候我们读取我们关注的元素的尺寸，但是实际上是有局限性的，比如说窗口没有变化，但是我们关注的dom尺寸变化他就不一定能观察到，而且这个方法是关注的页面上所有的dom，这个有点儿浪费性能。还有一点就是window.resize是<font color="red">无法被取消</font>的，这这一点需要注意。</strong>

### 兼容性

兼容性非常好，可以放心使用，[点击查看](https://caniuse.com/resizeobserver)

### 新建观察器

```js
	const domRef = document.querySelector('.demo')
	const observer = new ResizeObserver(entries => {
		console.log(entries)
	})
	observer.observe(domRef)	// 开启观察
```
回调函数中包含了观察dom的所有尺寸数据，可根据这些数据完成我们想要的操作

### 停止观察 disconnect()与unobserve()

```js
	const domRef = document.querySelector('.demo')
	const observer = new ResizeObserver(entries => {
		console.log(entries)
	})
	observer.observe(domRef)	// 开启观察
	ResizeObserver.disconnect()	// 取消所有的resizeObserve观察
	ResizeObserver.unobserve(domRef)	// 取消指定的观察器
	domRef.disconnect()	// 这样也可以去掉domRef的观察
```

## 注意事项

<font color="red">当你在用了这两个api之后，如果你销毁当前的组件的时候，一定记着要执行disconnect方法，否则控制台可能会报错。</font>

## 查看实例

[点击查看实例](https://codepen.io/luoyangz/pen/abRxeBQ)
