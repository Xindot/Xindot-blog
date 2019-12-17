---
layout: post
title: 前端面试之js篇（一）
tags: [js]
categories: [it]

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
	document.getElementById("text").style.display="none"
	//jQuery
	$('.a').hide(1000); $('.a').show(5000); $('.a').toggle(1000)
	$('.a').addClass('hide'); $('.a').removeClass('hide'); $('.a').toggleClass('hide')
	//vue
	<div v-if="a">demo1</div>
	<div v-if="{hide:a}">demo2</div>
	data层改变a的布尔值

#### Q4：如何添加html元素的事件处理，有几种方法？
	...

#### Q5：如何控制alert中的换行？
	...

#### Q6：判断一个字符串中出现次数最多的字符，统计这个次数？
	...

#### Q7：判断字符串是否是这样组成的：第一个必须是字母，后面可以是字母、数字、下划线、总长度为5-30？
	...

#### Q8：请编写一个JavaScript函数parseQueryString，它的用途是把URL参数解析为一个对象，如：var url = "http://xxx.com/index.html?key0=0&key1=1&key2=2"？
	...

#### Q9：在页面中有如下html，要求用闭包方式写一个js从文本框中取出值并在标签span中显示出来？
	<div id="field">
		<input type="text" value="user name">			
	</div>
	<span class="red"></span>
							

#### Q10：在IE6.0下面是不支持position:fixed的，请写一个js使用<div id="box"></div>固定在页面的右下角？
	...

#### Q11：请实现鼠标到页面中的任意标签，显示出这个标签的基本矩阵轮廓？
	...

#### Q12：js的基本对象有哪些，window和documnet的常用方法和属性列出来？
	...

#### Q13：JavaScript中如何对一个对象进行深度clone？
	...

#### Q14：js中如何定义class，如何扩展prototype？
	...

#### Q15：ajax是什么？ajax的交互模型？同步和异步的区别？如何解决跨域问题？
	...

#### Q16：请给出异步加载js方案，不少于两种？
	...

#### Q17：多浏览器检测通过什么？
	...

#### Q18：讲述一个你所了解的前端开发的优化方式？
	...







