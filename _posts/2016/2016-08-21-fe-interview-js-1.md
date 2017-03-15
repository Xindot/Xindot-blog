---
layout: post
title: 前端面试之js篇（一）
tags: [js]
---

#### Q1：JavaScript包含哪些数据类型，请分别写出3种以上类型的判断函数如：isString()？
	
	//js有6种数据类型（5种基本数据类型、1种复杂数据类型）
		1.String字符串; 2.Number数字; 3.Boolean布尔; 4.Null空对象指针; 5.Undefined没有定义
		6.Object对象; 
		7.Function函数; 8.Array数组;
	//isString(str)
		① typeof 'str' === "string"
		② Object.prototype.toString.call('str') === "[object String]"
		③ String('str') === 'str'
	//isNumber(num)
		方法一：!isNaN(parseFloat(1)) && isFinite(1)
		方法二：typeof 1 === "number" && !isNaN(1)
		方法三：typeof 1 === "number" && isFinite(1)
		方法四：Object.prototype.toString.call(1) === "[object Number]"
		方法五：1 === +1
	//isBoolean(b)
		① Object.prototype.toString.call(true) === "[object Boolean]"
		② typeof false === "boolean"
	//isNull(null)
		① Object.prototype.toString.call(null) === "[object Null]"
		② typeof null === "object"
	//isUndefined()
		① Object.prototype.toString.call() === "[object Undefined]"
		② typeof a === "undefiend"
	//isObject(obj)
		① Object.prototype.toString.call({}) === "[object Object]"
		② typeof {} === "object"
	//isFunction(func)
	 	① Object.prototype.toString.call(function(){}) === "[object Function]"
	 	② typeof funciton(){} === "function"
	 	//js固有函数
	 	③ Object.prototype.toString.call(clear) === "[object Function]"
	 	③ typeof clear === ”function“
	//isArray(arr)
		① Object.prototype.toString.call([]) === "[object Array]"
		② typeof [] === "object"

#### Q2：编写一个JavaScript函数，实时显示当前时间，格式"年-月-日 时-分-秒"？
	
	setInterval(function(){
		var time = new Date(),
			yyyy = time.getFullYear(),
			M = time.getMonth()+1,
			d = time.getDate(),
			h = time.getHours(),
			m = time.getMinutes(),
			s = time.getSeconds(),
			MM = M<10?('0'+M):M,
			dd = d<10?('0'+d):d,
			hh = h<10?('0'+h):h,
			mm = m<10?('0'+m):m,
			ss = s<10?('0'+s):s;
		var now = yyyy+'-'+MM+'-'+dd+' '+hh+':'+mm+':'+ss;
		console.log(now);
	},1000)
	//ES6

#### Q3：如何显示/隐藏一个DOM元素？
	
	//js
	//jQuery
	$('.a').toggle()


