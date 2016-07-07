---
layout: post
title: js实现金额‘千位分隔符’的思路及代码
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

