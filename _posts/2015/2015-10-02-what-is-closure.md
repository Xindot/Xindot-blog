---
layout: post
title: js小结：什么是闭包？
tags: [js]
---

在我面试时问出的一系列问题里，闭包通常是我问的第一个或最后一个问题。坦白地说，如果你连闭包也弄不明白，你是不会在 JavaScript 的道路上走多远的。

你别东张西望，说的就是你。你真的理解如何构建一个严谨的 JavaScript 应用？你真的理解代码背后发生的事情或者说一个应用程序是如何工作的？我表示怀疑。如果连个闭包问题都搞不清的话，真是有点够呛。

你不仅仅应该了解闭包的机制，更应该了解闭包为什么很重要，以及能够很容易地回答出闭包的几种可能的应用场景。

闭包在 JavaScript 中常用来实现对象数据的私有，在事件处理和回调函数中也常常会用到它，此外还有**偏函数应用（partial applications）**和**柯里化（currying）**，以及其他函数式编程模式。

我不在乎面试者是否知道“closure”这个单词或者它的专业定义。我只想弄清他们是否理解基本原理。如果他们没有，那么通常意味着这些面试者在构建实际 JavaScript 应用方面并没有很多经验。

> 如果你不能回答这个问题，你只是个初级开发者。不管你实际上已经干这个多久了。

为了快速理解下面的内容：你想一下能否举出两个闭包的通用场景？

### 什么是闭包？

简言之，闭包是由函数引用其周边状态（词法环境）绑在一起形成的（封装）组合结构。在 JavaScript 中，闭包在每个函数被创建时形成。

这是基本原理，但为什么我们关心这些？实际上，由于闭包与它的词法环境绑在一起，因此**闭包让我们能够从一个函数内部访问其外部函数的作用域。**

要使用闭包，只需要简单地将一个函数定义在另一个函数内部，并将它暴露出来。要暴露一个函数，可以将它返回或者传给其他函数。

**内部函数将能够访问到外部函数作用域中的变量**，即使外部函数已经执行完毕。

闭包使用的例子

闭包的用途之一是实现对象的私有数据。数据私有是让我们能够面向接口编程而不是面向实现编程的基础。而面向接口编程是一个重要的概念，有助于我们创建更加健壮的软件，因为实现细节比接口约定相对来说更加容易被改变。

> “面向接口编程，别面向实现编程。” 设计模式：可复用面向对象软件的要素

在 JavaScript 中，闭包是用来实现数据私有的原生机制。当你使用闭包来实现数据私有时，被封装的变量只能在闭包容器函数作用域中使用。你无法绕过对象被授权的方法在外部访问这些数据。在 JavaScript 中，任何定义在闭包作用域下的公开方法才可以访问这些数据。例如：

	const getSecret = (secret) => {
	  return {
	    get: () => secret
	  };
	};
	test('Closure for object privacy.', assert => {
	  const msg = '.get() should have access to the closure.';
	  const expected = 1;
	  const obj = getSecret(1);
	  const actual = obj.get();
	  try {
	    assert.ok(secret, 'This throws an error.');
	  } catch (e) {
	    assert.ok(true, `The secret var is only available
	      to privileged methods.`);
	  }
	  assert.equal(actual, expected, msg);
	  assert.end();
	});

在上面的例子里，get() 方法定义在 getSecret() 作用域下，这让它可以访问任何 getSecret()中的变量，于是它就是一个被授权的方法。在这个例子里，它可以访问参数 secret。

对象不是唯一的产生私有数据的方式。闭包还可以被用来创建有状态的函数，这些函数的执行过程可能由它们自身的内部状态所决定。例如：

	const secret = (msg) => () => msg;
	// Secret - creates closures with secret messages.
	// https://gist.github.com/ericelliott/f6a87bc41de31562d0f9
	// https://jsbin.com/hitusu/edit?html,js,output

	// secret(msg: String) => getSecret() => msg: String
	const secret = (msg) => () => msg;

	test('secret', assert => {
	  const msg = 'secret() should return a function that returns the passed secret.';

	  const theSecret = 'Closures are easy.';
	  const mySecret = secret(theSecret);

	  const actual = mySecret();
	  const expected = theSecret;

	  assert.equal(actual, expected, msg);
	  assert.end();
	});

在函数式编程中，闭包经常用于偏函数应用和柯里化。为了说明这个，我们先定义一些概念：

**函数应用：**一个过程，指将参数传给一个函数，并获得它的返回值。

**偏函数应用：**一个过程，它传给某个函数其中一部分参数，然后返回一个新的函数，该函数等待接受后续参数。换句话说，偏函数应用是一个函数，它接受另一个函数为参数，这个作为参数的函数本身接受多个参数，它返回一个函数，这个函数与它的参数函数相比，接受更少的参数。偏函数应用提前赋予一部分参数，而返回的函数则等待调用时传入剩余的参数。

偏函数应用通过闭包作用域来提前赋予参数。你可以实现一个通用的函数来赋予指定的函数部分参数，它看起来如下：

	partialApply(targetFunction: Function, ...fixedArgs: Any[]) => functionWithFewerParams(...remainingArgs: Any[])

如果你要更进一步理解上面的形式，你可以看这里。

partialApply 接受一个多参数的函数，以及一串我们想要提前赋给这个函数的参数，它返回一个新的函数，这个函数将接受剩余的参数。

下面给一个例子来说明，假设你有一个函数，求两个数的和：

	const add = (a, b) => a + b;

现在你想要得到一个函数，它能够对任何传给它的参数都加 10，我们可以将它命名为 add10()。add10(5) 的结果应该是 15。我们的 partialApply() 函数可以做到这个：

	const add10 = partialApply(add, 10);
	add10(5);

在这个例子里，参数 10 通过闭包作用域被提前赋予 add()，从而让我们获得 add10()。

现在让我们看一下如何实现 partialApply()：

	// Generic Partial Application Function
	// https://jsbin.com/biyupu/edit?html,js,output
	// https://gist.github.com/ericelliott/f0a8fd662111ea2f569e

	// partialApply(targetFunction: Function, ...fixedArgs: Any[]) =>
	//   functionWithFewerParams(...remainingArgs: Any[])
	const partialApply = (fn, ...fixedArgs) => {
	  return function (...remainingArgs) {
	    return fn.apply(this, fixedArgs.concat(remainingArgs));
	  };
	};
	test('add10', assert => {
	  const msg = 'partialApply() should partially apply functions'

	  const add = (a, b) => a + b;

	  const add10 = partialApply(add, 10);


	  const actual = add10(5);
	  const expected = 15;

	  assert.equal(actual, expected, msg);
	});

如你所见，它只是简单地返回一个函数，这个函数通过闭包访问了传给 partialApply() 函数的 fixedArgs 参数。

轮到你来试试了
你用闭包来做什么？如果你有最喜欢的应用场景，举一些例子，在评论中告诉我。

