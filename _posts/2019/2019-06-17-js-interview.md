---
layout: post
title: 45道JS面试题【整理篇】
tags: [js]
categories: [it]

---

###### 0.下面代码输出是什么？
```
// 0 '' null false undefined
console.log(0 == '',0 == null,0 == false,0 == undefined)
console.log('' == null,'' == false,'' == undefined)
console.log(null == false,null == undefined,false == undefined)
console.log(!0,!'',!null,!false,!undefined)
console.log(+0,+'',+null,+false,+undefined)
console.log(-0,-'',-null,-false,-undefined)
console.log(~0,~'',~null,~false,~undefined)
console.log(~~0,~~'',~~null,~~false,~~undefined)
```

###### 1.下面代码输出是什么？
```
function sayHi(){
	console.log(name);
	console.log(age);
	var name = 'me';
	let age = 18;
}
sayHi()
```

###### 2.下面代码输出是什么？
```
let name = 'me';
{
	console.log(name);
	let name = 'code';
}
```

###### 3.下面代码输出是什么？
```
const shape = {
	radius: 10,
	diameter(){
		return this.radius * 2
	},
	perimeter: () => 2 * Math.PI * this.radius
}
console.log(shape.diameter());
console.log(shape.perimeter());
```

###### 4.下面代码输出是什么？
```
console.log(+true);
console.log(!'linda');
```

###### 5.下面代码输出是什么？
```
const bird = {
	size: 'small'
}
const mouse = {
	name: 'Mickey',
	small: true
}
console.log(mouse.bird.size)
console.log(mouse[bird.size])
console.log(mouse[bird['size']])
```

###### 6.下面代码输出是什么？
```
let c = {
	greeting: 'hey',
}
let d;
d = c;
c.greeting = 'hello';
console.log(d.greeting);
```

###### 7.下面代码输出是什么？
```
let a = 3;
let b = new Number(3);
let c = 3;
console.log(a == b);
console.log(a === b);
console.log(b === c);
console.log(a === c);
```

###### 8.下面代码输出是什么？
```
class Chameleon {
	static colorChange(newColor){
		this.newColor = newColor
	}
	constructor({newColor='green'} = {}) {
		this.newColor = newColor
	}
}
const freddie = new Chameleon({newColor:'purple'});
console.log(freddie.colorChange('orange'));
```

###### 9.下面代码输出是什么？
```
// 'use strict'
let greeting;
greetign = {};
console.log(greetign)
```

###### 10.下面代码输出是什么？
```
function bark(){
	console.log('Woof')
}
bark.animal = 'dog'
console.log(bark.animal)
```

###### 11.下面代码输出是什么？
```
function Person(firstName,lastName){
	this.firstName = firstName;
	this.lastName = lastName;
}
const member = new Person('Linda','Harlin');
Person.getFullName = () => this.firstName + this.lastName;
// Person.prototype.getFullName = function(){
// 	return `${this.firstName} ${this.lastName}`
// }
console.log(member.getFullName());
```

###### 12.下面代码输出是什么？
```
function Person(firstName,lastName){
	this.firstName = firstName;
	this.lastName = lastName;
}
const Linda = new Person('Linda','Harlin');
const Sarah = Person('Sarah','Smith');
console.log(Linda)
console.log(Sarah)
```

###### 13.事件传播的三个阶段是什么？
```
// 捕获->目标->冒泡
```

###### 14.所有对象都有原型？
```
// 错误
// 除基础对象外，所有对象都有原型。基础对象的原型是null
```

###### 15.下面代码输出是什么？
```
function sum(a,b){
	return a + b;
}
console.log(sum(1,'2'))
```

###### 16.下面代码输出是什么？
```
let number = 0;
console.log(number++);
console.log(++number);
console.log(number);
```

###### 17.下面代码输出是什么？
```
function getPersonInfo(one,two,three){
	console.log(one)
	console.log(two)
	console.log(three)
}
const person = 'Linda';
const age = 18;
console.log(getPersonInfo`${person} is ${age} year old`)
```

###### 18.下面代码输出是什么？
```
function checkAge(data){
	if(data==={age:18}){
		console.log('A')
	} else if(data=={age:18}){
		console.log('B')
	}else{
		console.log('C')
	}
}
console.log(checkAge({age:18}))
```

###### 19.下面代码输出是什么？
```
function getAge(...args){
	console.log(args)
	console.log(typeof args)
} 
console.log(getAge(21));
```

###### 20.下面代码输出是什么？
```
function getAge(){
	'use strict';
	age = 18;
	console.log(age)
}
console.log(getAge());
```

###### 21.下面代码输出是什么？
```
const sum = eval('10*10+5')
console.log(sum)
```

###### 22.cool_secret可以访问多长时间？
```
sessionStorage.setItem('cool_secret',123);
// 用户关闭选项卡时清除
```

###### 23.下面代码输出是什么？
```
var num = 8;
var num = 10;
console.log(num);
```

###### 24.下面代码输出是什么？
```
const obj = {1:'a',2:'b',3:'c'};
const set = new Set([1,2,3,4,5]);
console.log(obj.hasOwnProperty('1'));
console.log(obj.hasOwnProperty(1));
console.log(set.has('1'));
console.log(set.has(1));
```

###### 25.下面代码输出是什么？
```
const obj = {a:'one',b:'two',a:'three'};
console.log(obj)
// 如果对象有两个具有相同名称的键，则将替换前面的键。它仍将处于第一个位置，但具有最后指定的值
```

###### 26.JavaScript全局执行上下文为你创建了两个东西...
```
// 全局对象和this关键字
```

###### 27.下面代码输出是什么？
```
for (let i = 0; i < 5; i++) {
	if(i===3) continue;
	console.log(i)
}
// 如果某个条件返回 true ，则 continue 语句跳过迭代
```

###### 28.下面代码输出是什么？
```
String.prototype.giveLindaPizza = () => {
	return 'ddd'
}
const name = 'Linda';
console.log(name.giveLindaPizza())
```

###### 29.下面代码输出是什么？
```
const a = {};
const b = {key:'b'};
const c = {key:'c'};
a[b] = 123;
a[c] = 456;
console.log(a[b]);
// a["[object Object]"] = 123
// a["[object Object]"] = 456
```

###### 30.下面代码输出是什么？
```
const foo = () => console.log('1')
const bar = () => setTimeout(() => console.log('2'))
const baz = () => console.log('3')
console.log(foo())
console.log(bar())
console.log(baz())
```

###### 31.单击按钮时 event.target 是什么？
```
<div onclick="console.log('1')">
	<div onclick="console.log('2')">
		<button onclick="console.log('3')">
			Click!
		</button>
	</div>
</div>
// button
```

###### 32.单击下面 html 片段打印的内容是什么？
```
<div onclick="console.log('div')">
	<p onclick="console.log('p')">
		Click here!
</div>
// p div
```

###### 33.下面代码输出是什么？
```
const person = {name:'Linda'};
function sayHi(age){
	console.log(`${this.name} id ${age}`)
}
console.log(sayHi.call(person,18));
console.log(sayHi.bind(person,18));
```

###### 34.下面代码输出是什么？
```
function sayHi() {
	return (() => 0)();
}
// console.log(sayHi());
console.log(typeof sayHi());
```

###### 35.以上哪些是假值？
```
0;
new Number(0);
('');
(' ');
new Boolean(false);
undefined;
// JavaScript 中只有6个假值：
undefined null NaN 0 '' false
```

###### 36.下面代码输出是什么？
```
console.log(typeof typeof 1);
```

###### 37.下面代码输出是什么？
```
const numbers = [1,2,3];
numbers[10] = 11;
console.log(numbers)
```

###### 38.下面代码输出是什么？
```
(() => {
	let x,y;
	try{
		throw new Error();
	}catch(x){
		(x=1),(y=2);
		console.log(x);
	}
	console.log(x);
	console.log(y);
})()
```

###### 39.JavaScript 中的所有内容都是...
```
// 原始和对象
// JavaScript 只有原始类型和对象
// 原始类型是 
Boolean null undefined BigInt Number String Symbol
```

###### 40.下面代码输出是什么？
```
[[0,1],[2,3]].reduce(
	(acc,cur) => {
		return acc.concat(cur);
	},
	[1,2]
)
```

###### 41.下面代码输出是什么？
```
console.log(!!null);
console.log(!!'');
console.log(!!1);
```

###### 42.下面方法返回值是什么？
```
setInterval(() => console.log('Hi'),1000);
// 一个唯一的id 可使用 claerInterval(id) 清除定时器
```

###### 43.下面代码输出是什么？
```
console.log([...'Linda']);
```

###### 44.TypeError、ReferenceError、SyntaxError的区别
```
// ReferenceError是跟作用域判别失败有关 
// TypeError是作用域判别成功后对结果非法操作或者不合理

// TypeError 对一个变量的值做不合理的操作,如对非函数的变量进行函数调用 
// 或者引用null或undefined类型的值得属性
let a = {};
console.log(a.list.name); //这种情况也比较常出现
```






