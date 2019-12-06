---
layout: post
title: vue orderBy按数值大小排序
tags: [vue]
---


> 需求：Vue 在列表渲染的时候，能排序显示么。 比如按价格从大到小排序 <br/>
*原文：[https://segmentfault.com/q/1010000004988322/a-1020000004988411](https://segmentfault.com/q/1010000004988322/a-1020000004988411){:target="_blank"}*

#### 如果按照用下面的写法,结果是按string类型进行排序的，会出现1、11、2、3、4这样的如果，显然后面加个-1，则排序为4、3、2、11、1

```
// 定义vue范围及监听的变量
var demo = new Vue({
	el: '#demo',
	data: {
		aaa: [
			{name: "山鹰登山社1",count: "1"},
			{name: "山鹰登山社11",count: "11"},
			{name: "山鹰登山社2",count: "2"},
			{name: "山鹰登山社3",count: "3"}
		]
	}
})
// html
<section id="demo">
	<ul>            
		<li v-for="item in aaa | orderBy 'count' -1">
			...
		</li>
	</ul>
</section>
```

#### 所以建议用orderBy function

```
// 定义vue范围及监听的变量
var demo = new Vue({
	el: '#demo',
	data: {
		aaa: [
			{name: "山鹰登山社1",count: "1"},
			{name: "山鹰登山社11",count: "11"},
			{name: "山鹰登山社2",count: "2"},
			{name: "山鹰登山社3",count: "3"}
		]
	},
	methods: {
		numSort: function (a,b) {
			return a.count-b.count;
		}
	}
})
// html
<section id="demo">
	<ul>            
		<li v-for="item in aaa | orderBy numSort">
			...
		</li>
	</ul>
</section>
```
