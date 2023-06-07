---
title: js数组遍历方法
top: false
cover: false
toc: true
mathjax: true
tags: ['Array']
categories: ['js']
date: 2022-08-25 21:48:27
password:
summary: 'js数组遍历方法'
coverImg:
img:
---

# 数组遍历方法
<font color="#42b983">数组方法有很多种，本篇文章只谈论数组的遍历</font>
```javascript
	let arr1 = [1,2,3,4,5]
```
## some
> some表示某一个，遍历找到数组中的某一个满足条件的值，返回值boolean类型。（找到元素停止）
```javascript
	let someb = arr1.some(item=>{
		return item > 1
	})
```
## every
> true
```javascript
	let everyb = arr1.every(item=>{
		return item > 1
	})
```
## find
> find遍历数组，根据条件判断，返回满足条件的元素本身。（找到元素停止）
```javascript
	let findObj = arr1.find(item=>{
		return item > 1
	})
	console.log('find值',findObj)
```
## filter
> filter遍历数组，根据条件判断，找到满足条件的每一个值，返回一个新的数组。（遍历每一个元素）
```javascript
	let filterArr = arr1.filter(item=>{
		return item > 1
	})
	console.log(filterArr)
```
## forEach与for
> forEach方法 该方法不能使用return跳出循环，break会报错，当用for循环的时候如果只是一个循环用return会报错，只能用berak跳出循环，如果想用return就要把他包括在一个方法里面，当然如果想用条件判断中途结束的话最好使用while或do while
```javascript
	arr1.forEach((item,index)=>{
		console.log(index)
		if(item > 2) return
	})
	!function(){
		for (var i = 0; i < arr1.length; i++) {
			console.log(i)
			return
		}
	}()
```
## map
> map方法遍历数组每一个元素，根据需要返回一个新的数组
```javascript
		let mapArr = arr1.map((item,index)=>{
		let obj = {}
		obj.value = item
		obj.index = index
		return obj
	})
	console.log('mapArr',mapArr)
```
## reduce
> reduce遍历，一般用于数组对象去重，求和或者多维数组转为一维数组，有四个参数，第一个是最终要返回的集合，第二个当前元素，第三个当前索引，第四个当前遍历的数组，方法最后的值是最终要返回的值的默认值

1. 数组求和
```javascript
	let numArr = [1,2,3,4,5,6,7,8,9]
	let num = numArr.reduce((aim,item,indx)=>{
		item > 5 ? aim += item : aim
		return aim
	},0)
	console.log(num)
```
2. 数组对象去重
```javascript
	let arrObj = [
		{
			name: '王哥',
			age: '11',
		},{
			name: '张哥',
			age: '12'
		},{
			name: '李哥',
			age: '12'
		},{
			name: '张哥',
			age: '13'
		}
	]
	let obj = {}
	let riddingArr = arrObj.reduce((arr,item,index,arrObj)=>{
		obj[item.age] ? false : obj[item.age] = true && arr.push(item)
		return arr
	},[])
	console.log(riddingArr)
```
3.	多维数组转为一维数组
```javascript
	let moreArr = [1,2,[3,4],[5,[6,[7,8],9],10],11]
	const oneMore = function(arr){
		return arr.reduce((pre,item)=>pre.concat(Array.isArray(item) ? oneMore(item) : item),[])
	}
	console.log(oneMore(moreArr))
```
## 在线预览

在线预览效果地址：<u>[点击预览](https://codepen.io/luoyangz/pen/BarXBRJ)</u>
