---
layout: post
title: js实现金额‘千位分隔符’的思路及代码（+优化版）
tags: [js]
---

>
找了一些js实现千位分隔符的代码，发现有些有漏洞，一个是不能处理带有小数点的数，一个是不能处理大数，综合两个代码，整理了一下，大概思路：
	
	数先转为字符串并判断数是否有小数，如有，连小数点拿掉并暂存，
	再除以3得余数，再根据‘余数’和‘3’将字符串拆分push到数组，
	最后转字符串再加上之前暂存的小数

代码如下：

	// 千位分隔符(js 实现)
	function thousandBitSeparator(str){ 
		str = String(str);
		if (str.indexOf('.')>=0) {
			var postfix = str.substring(str.indexOf('.'));
			str = str.substring(0,str.indexOf('.'));
		}else{
			var postfix = '';
		};
		// console.log(postfix);
		// .99
		// console.log(str);
		// 9999999999999
		var iNum = str.length % 3; 
		var prev = ''; 
		var iNow = 0; 
		var temp = ''; 
		var arr = []; 
		if (iNum != 0){ 
			prev = str.substring(0, iNum); 
			arr.push(prev); 
		} 
		str = str.substring(iNum); 
		for (var i = 0; i < str.length; i++){ 
			iNow++; 
			temp += str[i]; 
			if (iNow == 3 && temp){ 
			  arr.push(temp); 
			  temp = ''; 
			  iNow = 0; 
			} 
		} 
		// console.log(arr);
		// ["9", "999", "999", "999", "999"]
		return arr.join(',') + postfix; 
	}
	 
	// console.log(thousandBitSeparator('9999999999999.99'));
	// 9,999,999,999,999.99

>
测试有效


### 后来看到同事发布的优化方案，不拿锅里来觉得对不起他

	function splitK(num) {
	  var decimal = String(num).split('.')[1] || '';//小数部分
	  var tempArr = [];
	  var revNumArr = String(num).split('.')[0].split("").reverse();//倒序
	  for (i in revNumArr){
	    tempArr.push(revNumArr[i]);
	    if((i+1)%3 === 0 && i != revNumArr.length-1){
	      tempArr.push(',');
	    }
	  }
	  var zs = tempArr.reverse().join('');//整数部分
	  return decimal?zs+'.'+decimal:zs;
	}
	var num = '123456789.123';
	console.log(splitK(num));
	//输出：123,456,789.123

>
思路更简单：
先分离出小数部分；
对整数部分逆序为数组；
每三个数字插入一个逗号，如果是3的倍数位则最后一个不插入；
再逆序回来，拼接小数部分（如果有的话）。
[查看原文https://segmentfault.com/a/1190000005906366](https://segmentfault.com/a/1190000005906366){:target="_blank"}

>
点赞

>
测试如果是数字类型可能提示undefined,对num加个String()即可

