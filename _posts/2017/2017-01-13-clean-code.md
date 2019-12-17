---
layout: post
title: js小结：JavaScript 代码整洁之道（一）
tags: [js]
categories: [it]

---


## 概述

Robert C. Martin 在 [《代码整洁之道》](http://vdisk.weibo.com/s/zrPOK0IqWgbk1){:target="_blank"} 中提到的软件工程原则，同样适用于 JavaScript。这不是一个风格参考。它指导如何用 JavaScript 编写可读、可复用、可重构的软件。

并不是每一个原则都必须严格遵循，甚至很少得到大家的认同。它们仅用于参考，不过要知道这些原则都是《代码整洁之道》的作者们累积多年的集体经验。

我们在软件工程方面的技术发展刚刚超过 50 年，我们仍然在学习很多东西。当软件架构和架构本身一样古老的时候，我们应该遵循更为严格规则。现在，对于你和你的团队编写的 JavaScript 代码，不妨依据这些准则来进行质量评估。

还有一件事：知道这些不会马上让你成为更好的软件开发者，在工作中常年使用这些准则不能让你避免错误。每一段代码都从最初的草图开始到最终成型，就像为湿粘土塑形一样。最后，当我们与同行一起审查的时候，再把不完美的地方消除掉。不要因为初稿需要改善而否定自己，需要要否定的只是那些代码！

---

## 变量

---

#### 使用有准确意义的变量名

不好:

	var yyyymmdstr = moment().format('YYYY/MM/DD');

好:
	
	var yearMonthDay = moment().format('YYYY/MM/DD');

---

#### 在变量的值不会改变时使用 ES6 的常量

在不好的示例中，变量可以被改变。如果你申明一个常量，它会在整个程序中始终保持不变。

不好:
	
	var FIRST_US_PRESIDENT = "George Washington";

好:
	
	const FIRST_US_PRESIDENT = "George Washington";

---

#### 对同一类型的变量使用相同的词汇

不好:
	
	getUserInfo();getClientData();getCustomerRecord();

好:

	getUser();

---

#### 使用可检索的名称

我们阅读的代码永远比写的折。写可读性强、易于检索的的代码非常重要。在程序中使用无明确意义的变量名会难以理解，对读者造成伤害。所以，把名称定义成可检索的。

不好:

	// 见鬼，525600 是个啥？
	for (var i = 0; i < 525600; i++) {
		runCronJob();
	}

好:

	// 用 `var` 申明为大写的全局变量
	var MINUTES_IN_A_YEAR = 525600;for (var i = 0; i < MINUTES_IN_A_YEAR; i++) {
		runCronJob();
	}

---

#### 使用解释性的变量

不好:
	
	const cityStateRegex = /^(.+)[,\\s]+(.+?)\s*(\d{5})?$/;
	saveCityState(cityStateRegex.match(cityStateRegex)[1], cityStateRegex.match(cityStateRegex)[2]);

好:
	
	const cityStateRegex = /^(.+)[,\\s]+(.+?)\s*(\d{5})?$/;
	const match = cityStateRegex.match(cityStateRegex);
	const city = match[1];
	const state = match[2];saveCityState(city, state);

---

#### 避免暗示

显式优于隐式。

不好:
	
	var locations = ['Austin', 'New York', 'San Francisco'];locations.forEach((l) => {
		doStuff();
		doSomeOtherStuff();
		...
		...
		...
		// 等等，`l` 又是什么？
		dispatch(l);
	});

好:

	var locations = ['Austin', 'New York', 'San Francisco'];locations.forEach((location) => {
		doStuff();
		doSomeOtherStuff();
		...
		...
		...
		dispatch(location);
	 });

---

#### 不要添加没必要的上下文

如果你的类名称/对象名称已经说明了它们是什么，不要在(属性)变量名里重复。

不好:

	var Car = {
		carMake: 'Honda',
		carModel: 'Accord',
		carColor: 'Blue'
	};
	function paintCar(car) {
		car.carColor = 'Red';
	}

好:

	var Car = {
		make: 'Honda',
		model: 'Accord',
		color: 'Blue'
	};
	function paintCar(car) {
		car.color = 'Red';
	}

---

#### 短路语法比条件语句更清晰

不好:

	function createMicrobrewery(name) {
		var breweryName;
		if (name) {
			breweryName = name;
		} else {
			breweryName = 'Hipster Brew Co.';
		}
	}

好:

	function createMicrobrewery(name) {
		var breweryName = name || 'Hipster Brew Co.'
	}

---

## 函数

---

#### 函数参数 (理论上少于等于2个)

限制函数参数的数量极为重要，它会让你更容易测试函数。超过3个参数会导致组合膨胀，以致于你必须根据不同的参数对大量不同的情况进行测试。

理想情况下是没有参数。有一个或者两个参数也还好，三个就应该避免了。多于那个数量就应该考虑合并。通常情况下，如果你有多于2个参数，你的函数会尝试做太多事情。如果不是这样，大多数时候可以使用一个高阶对象作为参数使用。

既然 JavaScript 允许我们在运行时随意创建对象，而不需要预先定义样板，那么你在需要很多参数的时候就可以使用一个对象来处理。

不好:

	function createMenu(title, body, buttonText, cancellable) {
		...
	}

好:

	var menuConfig = {
		title: 'Foo',
		body: 'Bar',
		buttonText: 'Baz',
		cancellable: true
	}
	function createMenu(menuConfig) {
		...
	}

---

#### 一个函数只做一件事

目前这是软件工程中最重要的原则。如果函数做了较多的事情，它就难以组合、测试和推测。当你让函数只做一件事情的时候，它们就很容易重构，而且代码读起来也会清晰得多。你只需要遵循本指南的这一条，就能领先于其他很多开发者。

不好:

	function emailClients(clients) {
		clients.forEach(client => {
			let clientRecord = database.lookup(client);
			if (clientRecord.isActive()) {
				email(client);
			}
		});
	}

好:

	function emailClients(clients) {
		clients.forEach(client => {
			emailClientIfNeeded(client);
		});
	}
	function emailClientIfNeeded(client) {
		if (isClientActive(client)) {
			email(client);
		}
	}
	function isClientActive(client) {
		let clientRecord = database.lookup(client);
		return clientRecord.isActive();
	}

---

#### 函数名称要说明它做的事

不好:

	function dateAdd(date, month) {
		// ...
	}
	let date = new Date();
	// 很难从函数名了解到加了什么dateAdd(date, 1);

好:

	function dateAddMonth(date, month) {
		// ...
	}
	let date = new Date();
	dateAddMonth(date, 1);

---

#### 函数应该只抽象一个层次

如果你有多个层次的抽象，那么你的函数通常做了太多事情，此时应该拆分函数使其易于复用和易于测试。

不好:

	function parseBetterJSAlternative(code) {
		let REGEXES = [
			// ...
		];
		let statements = code.split(' ');
		let tokens;
		REGEXES.forEach((REGEX) => {
			statements.forEach((statement) => {
				// ...
			})
		});
		let ast;
		tokens.forEach((token) => {
			// lex...
		});
		ast.forEach((node) => {
			// parse...
		})
	}

好:

	function tokenize(code) {
		let REGEXES = [
			// ...
		];
		let statements = code.split(' ');
		let tokens;
		REGEXES.forEach((REGEX) => {
			statements.forEach((statement) => {
				// ...
			})
		});
		return tokens;
	}
	function lexer(tokens) {
		let ast;
		tokens.forEach((token) => {
			// lex...
		});
		return ast;
	}
	function parseBetterJSAlternative(code) {
		let tokens = tokenize(code);
		let ast = lexer(tokens);
		ast.forEach((node) => {
			// parse...
		})
	}

---

#### 删除重复代码

任何情况下，都不要有重复的代码。没有任何原因，它很可能是阻碍你成为专业开发者的最糟糕的一件事。重复代码意味着你要修改某些逻辑的时候要修改不止一个地方的代码。JavaScript 是弱类型语句，所以它很容易写通用性强的函数。记得利用这一点！

不好:

	function showDeveloperList(developers) {
		developers.forEach(developers => {
			var expectedSalary = developer.calculateExpectedSalary();
			var experience = developer.getExperience();
			var githubLink = developer.getGithubLink();
			var data = {
				expectedSalary: expectedSalary,
				experience: experience,
				githubLink: githubLink
			};
			render(data);
		});
	}
	function showManagerList(managers) {
		managers.forEach(manager => {
			var expectedSalary = manager.calculateExpectedSalary();
			var experience = manager.getExperience();
			var portfolio = manager.getMBAProjects();
			var data = {
				expectedSalary: expectedSalary,
				experience: experience,
				portfolio: portfolio
			};
			render(data);
		});
	}

好:

	function showList(employees) {
		employees.forEach(employee => {
			var expectedSalary = employee.calculateExpectedSalary();
			var experience = employee.getExperience();
			var portfolio;
			if (employee.type === 'manager') {
				portfolio = employee.getMBAProjects();
			} else {
				portfolio = employee.getGithubLink();
			}
			var data = {
				expectedSalary: expectedSalary,
				experience: experience,
				portfolio: portfolio
			};
			render(data);
		});
	}

---

#### 使用默认参数代替短路表达式

不好:

	function writeForumComment(subject, body) {
		subject = subject || 'No Subject';
		body = body || 'No text';
	}

好:

	function writeForumComment(subject = 'No subject', body = 'No text') {
		...
	}

---

#### 用 Object.assign 设置默认对象

不好:

	var menuConfig = {
		title: null,
		body: 'Bar',
		buttonText: null,
		cancellable: true
	}
	function createMenu(config) {
		config.title = config.title || 'Foo'
		config.body = config.body || 'Bar'
		config.buttonText = config.buttonText || 'Baz'
		config.cancellable = config.cancellable === undefined ? config.cancellable : true;
	}
	createMenu(menuConfig);

好:

	var menuConfig = {
		title: 'Order',
		// User did not include 'body' key
		buttonText: 'Send',
		cancellable: true
	}
	function createMenu(config) {
		config = Object.assign({
			title: 'Foo',
			body: 'Bar',
			buttonText: 'Baz',
			cancellable: true
		}, config);
		// 现在 config 等于: {title: "Foo", body: "Bar", buttonText: "Baz", cancellable: true}
		// ...
	}
	createMenu(menuConfig);

---

#### 不要把标记用作函数参数

标记告诉你的用户这个函数做的事情不止一件。但是函数应该只做一件事。如果你的函数中会根据某个布尔参数产生不同的分支，那就拆分这个函数。

不好:

	function createFile(name, temp) {
		if (temp) {
			fs.create('./temp/' + name);
		} else {
			fs.create(name);
		}
	}

好:

	function createTempFile(name) {
		fs.create('./temp/' + name);
	}
	function createFile(name) {
		fs.create(name);
	}

---

#### 避免副作用

如果一个函数不是获取一个输入的值并返回其它值，它就有可能产生副作用。这些副作用可能是写入文件、修改一些全局变量，或者意外地把你所有钱转给一个陌生人。

现在你确实需要在程序中有副作用。像前面提到的那样，你可能需要写入文件。现在你需要做的事情是搞清楚在哪里集中完成这件事情。不要使用几个函数或类来完成写入某个特定文件的工作。采用一个，就一个服务来完成。

关键点是避免觉的陷阱，比如在没有结构的对象间共享状态，使用可以被任意修改的易变的数据类型，没有集中处理发生的副作用等。如果你能做到，你就能比其他大多数程序员更愉快。

不好:

	// 下面的函数使用了全局变量。
	// 如果有另一个函数在使用 name，现在可能会因为 name 变成了数组而不能正常运行。
	var name = 'Ryan McDermott';
	function splitIntoFirstAndLastName() {
		name = name.split(' ');
	}
	splitIntoFirstAndLastName();
	console.log(name); 
	// ['Ryan', 'McDermott'];

好:

	function splitIntoFirstAndLastName(name) {
		return name.split(' ');
	}
	var name = 'Ryan McDermott';
	var newName = splitIntoFirstAndLastName(name);
	console.log(name); 
	// 'Ryan McDermott';console.log(newName); 
	// ['Ryan', 'McDermott'];

---

#### 不要写入全局函数

JavaScript 中全局污染是一件糟糕的事情，因为它可能和另外库发生冲突，然而使用你 API 的用户却不会知道——直到他们在生产中遇到一个异常。来思考一个例子：你想扩展 JavaScript 的原生 Array，使之拥有一个 diff 方法，用来展示两数据之前的区别，这时你会怎么做？你可以给 Array.prototype 添加一个新的函数，但它可能会与其它想做同样事情的库发生冲突。如果那个库实现的 diff 只是比如数组中第一个元素和最后一个元素的异同会发生什么事情呢？这就是为什么最好是使用 ES6 的类语法从全局的 Array 派生一个类来做这件事。

不好:

	Array.prototype.diff = function(comparisonArray) {
		var values = [];
		var hash = {};
		for (var i of comparisonArray) {
			hash[i] = true;
		}
		for (var i of this) {
			if (!hash[i]) {
				values.push(i);
			}
		}
		return values;
	}

好:

	class SuperArray extends Array {
		constructor(...args) {
			super(...args);
		}
		diff(comparisonArray) {
			var values = [];
			var hash = {};
			for (var i of comparisonArray) {
				hash[i] = true;
			}
			for (var i of this) {
				if (!hash[i]) {
					values.push(i);
				}
			}
			return values;
		}
	}

---

#### 喜欢上命令式编程之上的函数式编程

如果 Haskell 是 IPA 那么 JavaScript 就是 O'Douls。就是说，与 Haskell 不同，JavaScript 不是函数式编程语言，不过它仍然有一点函数式的意味。函数式语言更整洁也更容易测试，所以你最好能喜欢上这种编程风格。

不好:

	const programmerOutput = [
	{
		name: 'Uncle Bobby',
		linesOfCode: 500
	}, {
		name: 'Suzie Q',
		linesOfCode: 1500
	}, {
		name: 'Jimmy Gosling',
		linesOfCode: 150
	}, {
		name: 'Gracie Hopper',
		linesOfCode: 1000
	}];
	var totalOutput = 0;
	for (var i = 0; i < programmerOutput.length; i++) {
		totalOutput += programmerOutput[i].linesOfCode;
	}

好:

	const programmerOutput = [
	{
		name: 'Uncle Bobby',
		linesOfCode: 500
	}, {
		name: 'Suzie Q',
		linesOfCode: 1500
	}, {
		name: 'Jimmy Gosling',
		linesOfCode: 150
	}, {
		name: 'Gracie Hopper',
		linesOfCode: 1000
	}];
	var totalOutput = programmerOutput.map((programmer) => programmer.linesOfCode).reduce((acc, linesOfCode) => acc + linesOfCode, 0);

---

#### 封装条件

不好:

	if (fsm.state === 'fetching' && isEmpty(listNode)) {
		/// ...
	}

好:

	function shouldShowSpinner(fsm, listNode) {
		return fsm.state === 'fetching' && isEmpty(listNode);
	}
	if (shouldShowSpinner(fsmInstance, listNodeInstance)) {
		// ...
	}

---

#### 避免否定条件

不好:

	function isDOMNodeNotPresent(node) {
		// ...
	}
	if (!isDOMNodeNotPresent(node)) {
		// ...
	}

好:

	function isDOMNodePresent(node) {
		// ...
	}
	if (isDOMNodePresent(node)) {
		// ...
	}

---

#### 避免条件

这似乎是个不可能完成的任务。大多数人第一次听到这个的时候会说，“没有 if 语句我该怎么办？”回答是在多数情况下都可以使用多态来实现相同的任务。第二个问题通常是，“那太好了，不过我为什么要这么做呢？”答案在于我们之前了解过整洁的概念：一个函数应该只做一件事情。如果你的类和函数有 if 语句，就意味着你的函数做了更多的事。记住，只做一件事。

不好:

	class Airplane {
		//...
		getCruisingAltitude() {
			switch (this.type) {
			case '777':
				return getMaxAltitude() - getPassengerCount();
			case 'Air Force One':
				return getMaxAltitude();
			case 'Cessna':
				return getMaxAltitude() - getFuelExpenditure();
			}
		}
	}

好:

	class Airplane {
		//...
	}
	class Boeing777 extends Airplane {
		//...
		getCruisingAltitude() {
			return getMaxAltitude() - getPassengerCount();
		}
	}
	class AirForceOne extends Airplane {
		//...
		getCruisingAltitude() {
			return getMaxAltitude();
		}
	}
	class Cessna extends Airplane {
		//...
		getCruisingAltitude() {
			return getMaxAltitude() - getFuelExpenditure();
		}
	}

---

#### 避免类型检查(第1部分)

JavaScript 是无类型的，也就是说函数可以获取任意类型的参数。有时候你会觉得这种自由是种折磨，因而会不由自主地在函数中使用类型检查。有很多种方法可以避免类型检查。首先要考虑的就是 API 的一致性。

不好:

	function travelToTexas(vehicle) {
		if (vehicle instanceof Bicycle) {
			vehicle.peddle(this.currentLocation, new Location('texas'));
		} else if (vehicle instanceof Car) {
			vehicle.drive(this.currentLocation, new Location('texas'));
		}
	}

好:

	function travelToTexas(vehicle) {
		vehicle.move(this.currentLocation, new Location('texas'));
	}

---

#### 避免类型检查(第2部分)

如果你在处理基本类型的数据，比如字符串，整数和数组，又不能使用多态，这时你会觉得需要使用类型检查，那么可以考虑 TypeScript。这是普通 JavaScript 的完美替代品，它在标准的 JavaScript 语法之上提供了静态类型。普通 JavaScript 手工检查类型的问题在于这样会写很多废话，而人为的“类型安全”并不能弥补损失的可读性。让你的 JavaScript 保持整洁，写很好的测试，并保持良好的代码审查。否则让 TypeScript (我说过，这是很好的替代品)来做所有事情。

不好:

	function combine(val1, val2) {
		if (typeof val1 == "number" && typeof val2 == "number" ||
		typeof val1 == "string" && typeof val2 == "string") {
			return val1 + val2;
		} else {
			throw new Error('Must be of type String or Number');
		}
	}

好:

	function combine(val1, val2) {
		return val1 + val2;
	}

---

#### 不要过度优化

现在浏览器在运行时悄悄地做了很多优化工作。很多时候你的优化都是在浪费时间。这里有很好的资源 可以看看哪些优化比较缺乏。把它们作为目标，直到他们能固定下来的时候。

不好:

	// 在旧浏览器中，每次循环的成本都比较高，因为每次都会重算 `len`。
	// 现在浏览器中，这已经被优化了。
	for (var i = 0, len = list.length; i < len; i++) {
		// ...
	}

好:

	for (var i = 0; i < list.length; i++) {
		// ...
	}

---

#### 删除不用的代码

不用的代码和重复的代码一样糟糕。在代码库中保留无用的代码是毫无道理的事情。如果某段代码用不到，那就删掉它！如果你以后需要它，仍然可以从代码库的历史版本中找出来。

不好:

	function oldRequestModule(url) {
		// ...
	}
	function newRequestModule(url) {
		// ...
	}
	var req = newRequestModule;
	inventoryTracker('apples', req, 'www.inventory-awesome.io');

好:

	function newRequestModule(url) {
		// ...
	}
	var req = newRequestModule;
	inventoryTracker('apples', req, 'www.inventory-awesome.io');

---

未完～

> PS：这本书在前面跟大家分享过，关注公号，输入关键字：2010107，则可以获取《代码整洁之道》电子版图书的下载地址，进行下载PDF版。


	原文：https://github.com/ryanmcdermott/clean-code-javascript/blob/master/README.md
	译文：http://www.zcfy.cc/article/clean-code-javascript-readme-md-at-master-ryanmcdermott-clean-code-javascript-github-2273.html
	译者：边城

