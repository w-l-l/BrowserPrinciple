# this：从JavaScript执行上下文视角讲this

在上篇文章中，我们讲了词法作用域、作用域链以及闭包，并在最后思考题留了下面这样一段代码：

```js
var bar = {
  myName: 'time.geekbang.com',
  printName: function() {
    console.log(myName)
  }
}
function foo() {
  let myName = '极客时间'
  return bar.printName
}
let myName = '极客邦'
let _printName = foo()
_printName()
bar.printName()
```

相信你已经知道了，在 printName 函数里面使用的变量 myName 是属于全局作用域下面的，所以最终打印出来的值都是“极客邦”。这是因为 JavaScript 语言的作用域链是由词法作用域决定的，而词法作用域是由代码结构来确定的。

不过按照常理来说，调用 bar.printName 方法时，该方法内部的变量 myName 应该使用 bar 对象中的，因为它们是一个整体，大多数面向对象语言都是这样设计的，比如我用 C++ 改写了上面那段代码，如下所示：

```c++
#include <iostream>
using namespace std;
class Bar{
  public:
  char* myName;
  Bar() {
    myName = 'time.geekbang.com';
  }
  void printName() {
    cout<< myName <<endl;
  }  
} bar;
 
char* myName = '极客邦';
int main() {
	bar.printName();
	return 0;
}
```

在这段 C++ 代码中，我同样调用了 bar 对象中的 printName 方法，最后打印出来的值就是 bar 对象内部变量 myName 值——"time.geekbang.com"，而并不是最外面定义变量 myName 的值——"极客邦"，所以在对象内部的方法中使用对象内部的属性是一个非常普遍的需求。但是 JavaScript 的作用域机制并不支持这一点，基于这个需求，JavaScript 又搞出另外一套 this 机制。

所以，在 JavaScript 中可以使用 this 实现在 printName 函数中访问到 bar 对象的 myName 属性了。具体该怎么操作呢？你可以调整 printName 的代码，如下所示：

```js
printName: function() {
  console.log(this.myName)
}
```

接下来咱们就展开来介绍 this，不过在讲解之前，希望你能区分清楚作用域链和 this 是两套不同的系统，它们之间基本没太多联系。在前期明确这点，可以避免你在学习 this 的过程中，和作用域产生一些不必要的关联。

## JavaScript中的this是什么

关于 this，我们还得先从执行上下文说起。在前面几篇文章中，我们提到执行上下文中包含了变量环境、词法环境、外部环境，但其实还有一个 this 没有提及，具体你可以参考下图：

![执行上下文环境](./img/execute-context-environment.png)

从图中可以看出，this 是和执行上下文绑定的，也就是说每个执行上下文中都有一个 this。前面《08 | 调用栈：为什么JavaScript代码会出现栈溢出？》中我们提到过，执行上下文主要分为三种——全局执行上下文、函数执行上下文和 eval 执行上下文，所以对应的 this 也只有这三种——全局执行上下文中的 this、函数中的 this 和 eval 中的 this。

那么接下来我们就重点讲解下全局执行上下文中的 this 和函数执行上下文中的 this。

## 全局执行上下文中的this

首先我们来看看全局执行上下文中的 this 是什么。

你可以在控制台中输入 console.log(this) 来打印出来全局执行上下文中的 this，最终输出的是 window 对象。所以你可以得出这样一个结论：在全局执行上下文中的 this 是指向 window 对象的。这也是 this 和作用域链的唯一交点，作用域链的最低端包含了 window 对象，全局执行上下文中的 this 也是指向 window 对象。
