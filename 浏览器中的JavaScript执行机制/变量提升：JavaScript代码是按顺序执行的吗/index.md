# 变量提升：JavaScript代码是按顺序执行的吗

讲解完宏观视角下的浏览器后，从这篇文章开始，我们就进入下一个新的模块了，这里我会对 JavaScript 执行原理做深入介绍。

今天在该模块的第一篇，我们主要讲解执行上下文相关的内容。那为什么先讲执行上下文呢？它这么重要吗？可以这么说，只有理解了 JavaScript 的执行上下文，你才能更好地理解 JavaScript 语言本身，比如变量提升、作用域和闭包等。不仅如此，理解执行上下文和调用栈的概念还能助你成为一名更合格的前端开发者。

不过由于我们专栏不是专门讲 JavaScript 语言的，所以我并不会对 JavaScript 语法本身做过多介绍。本文主要是从 JavaScript 的顺序执行讲起，然后一步步带你了解 JavaScript 是怎么运行的。

接下来咱们先看段代码，你觉得下面这段代码输出的结果是什么？

```js
showName()
console.log(myname)
var myname = '极客时间'
function showName() {
  console.log('函数showName被执行')
}
```

使用过 JavaScript 开发的程序员应该都知道，JavaScript 是按顺序执行的。若按照这个逻辑来理解的话，那么：

- 当执行到第1行的时候，由于函数 showName 还没有定义，所以执行应该会报错。

- 同样执行第2行的时候，由于变量 myname 也未定义，所以同样也会报错。

然而实际执行结果却并非如此，如下图：

![代码打印结果](./img/console-result.png)

第1行输出“函数showName被执行”，第2行输出“undefined”，这和前面想象中的顺序执行有点不一样啊！

通过上面的执行结果，你应该已经知道了函数或者变量可以在定义之前使用，那如果使用没有定义的变量或者函数，JavaScript 代码还能继续执行吗？为了验证这点，我们可以删除第3行 myname 的定义，如下所示：

```js
showName()
console.log(myname)
function showName() {
  console.log('函数showName被执行')
}
```

然后再次执行这段代码时，JavaScript 引擎就会报错，结果如下：

![代码报错](./img/console-reference-error.png)

从上面两段代码的执行结果来看，我们可以得出如下三个结论。

- 执行过程中，若使用了未声明的变量，那么 JavaScript 执行会报错。

- 在一个变量定义之前使用它，不会出错，但是该变量的值会为 undefined，而不是定义时的值。

- 在一个函数定义之前使用它，不会出错，且函数能正确执行。

第一个结论很好理解，因为变量没有定义，这样在执行 JavaScript 代码时，就找不到该变量，所以 JavaScript 会抛出错误。

但是对于第二个和第三个结论，就挺让人费解的：

- 变量和函数为什么能在其定义之前使用？这似乎表明 JavaScript 代码并不是一行一行执行的。

- 同样的方式，变量和函数的处理结果为什么不一样？比如上面的执行结果，提前使用的 showName 函数能打印出来完整结果，但是提前使用的 myname 变量值却是 undefined，而不是定义时使用的“极客时间”这个值。

## 变量提升（hoisting）

要解释这两个问题，你就需要先了解下什么是变量提升。

不过在介绍变量提升之前，我们先通过下面这段代码，来看看什么是 JavaScript 中的声明和赋值。

```js
var myname = '极客时间'
```

这段代码你可以把它看成是两行代码组成的：

```js
var myname  // 声明部分
myname = '极客时间' // 赋值部分
```

![声明和赋值](./img/statement-and-assignment.png)

上面是变量的声明和赋值，那接下来我们再来看看函数的声明和赋值，结合下面这段代码：

```js
function foo() {
  console.log('foo')
}

var bar = function() {
  console.log('bar')
}
```

第一个函数 foo 是一个完整的函数声明，也就是说没有涉及到赋值操作；第二个函数是先声明变量 bar，再把 `function() {console.log('bar')}` 赋值给 bar。为了直观理解，你可以参考下图：

![函数声明](./img/function-statement.png)

好了，理解了声明和赋值操作，那接下来我们就可以聊聊什么是变量提升了。

**所谓的变量提升，是指在 JavaScript 代码执行过程中，JavaScript 引擎把变量的声明部分和函数的声明部分提升到代码开头的“行为”。变量被提升后，会给变量设置默认值，这个默认值就是我们熟悉的 undefined。**

下面我们来模拟下实现：

```js
/* 变量提升部分 */
// 把变量 myname 提升到开头
// 同时给 myname 赋值为 undefined
var myname = undefined
// 把函数 showName 提升到开头
function showName() {
  console.log('showName被调用')
}

/* 可执行代码部分 */
showName()
console.log(myname)
// 去掉var声明部分，保留赋值语句
myname = '极客时间'
```

为了模拟变量提升的效果，我们对代码做了以下调整，如下图：

![模拟变量提升](./img/simulation-variable-promote.png)

从图中可以看出，对原来的代码主要做了两处调整：

- 第一处是把声明的部分都提升到了代码开头，如变量 `myname` 和函数 `showName`，并给变量设置默认值 `undefined`。

- 第二处是移除原本声明的变量和函数，如 `var myname = '极客时间'` 的语句，移除了 `var` 声明，整个移除 `showName` 的函数声明。

- 通过这两步，就可以实现变量提升的效果。你也可以执行这段模拟变量提升的代码，其输出结果和第一段代码应该是完全一样的。

通过这段模拟的变量提升代码，相信你已经明白了可以在定义之前使用变量或者函数的原因——函数和变量在执行之前都提升到了代码开头。
