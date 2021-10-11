# async await使用同步方式写异步代码

在上篇文章中，我们介绍了怎么使用 Promise 来实现回调操作，使用 Promise 能很好地解决回调地狱的问题，但是这种方式充满了 Promise 的 then() 方法，如果处理流程比较复杂的话，那么整段代码将充斥着 then，语义化不明显，代码不能很好地表示执行流程。

比如下面这样一个实际的使用场景：我先请求极客邦的内容，等返回信息之后，我再请求极客邦的另外一个资源。下面代码展示的是使用 fetch 来实现这样的需求，fetch 被定义在 window 对象中，可以用它来发起远程资源的请求，该方法返回的是一个 Promise 对象，这和我们上篇文章中讲的 XFetch 很像，只不过 fetch 是浏览器原生支持的，并没有利用 XMLHttpRequest 来封装。

```js
fetch('https://www.geekbang.org')
.then((response) => {
  console.log(response)
  return fetch('https://www.geekbang.org/test')
}).then((response) => {
  console.log(response)
}).catch((error) => {
  console.log(error)
})
```

从这段 Promise 代码可以看出来，使用 promise.then 也是相当复杂的，虽然整个请求流程已经线性化了，但是代码里面包含了大量的 then 函数，使得代码依然不是太容易阅读。基于这个原因，ES7 引入了 async / await，这是 JavaScript 异步编程的一个重大改进，提供了在不阻塞主线程的情况下使用同步代码实现异步访问资源的能力，并且使得代码逻辑更加清晰。你可以参考下面这段代码：

```js
async function foo() {
  try {
    let response1 = await fetch('https://www.geekbang.org')
    console.log('response1')
    console.log(response1)
    let response2 = await fetch('https://www.geekbang.org/test')
    console.log('response2')
    console.log(response2)
  } catch(err) {
    console.error(err)
  }
}
foo()
```

通过上面代码，你会发现整个异步处理的逻辑都是使用同步代码的方式来实现的，而且还支持 try catch 来捕获异常，这就是完全在写同步代码，所以非常符合人的线性思维的。但是很多人都习惯了异步回调的编程思维，对于这种采用同步代码实现异步逻辑的方式，还需要一个转换的过程，因为这中间隐藏了一些容易让人迷惑的细节。

那么本篇文章我们继续深入，看看 JavaScript 引擎是如何实现 async / await 的。如果上来直接介绍 async / await 的使用方式的话，那么你可能会有点懵，所以我们就从其最底层的技术点一步步往上讲解，从而带你彻底弄清楚 async 和 await 到底是怎么工作的。

本文我们首先介绍生成器（Generator）是如何工作的，接着讲解 Generator 的底层实现机制——协程（Coroutine）；又因为 async / await 使用了 Generator 和 Promise 两种技术，所以紧接着我们就通过 Generator 和 Promise 来分析 async / await 到底是如何以同步的方式来编写异步代码的。
