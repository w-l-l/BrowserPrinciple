# 浏览器工作原理与实战

[原文链接](https://blog.poetries.top/browser-working-principle/)

## 宏观视角上的浏览器

- [Chrome架构：仅仅打开1个页面，为什么有4个进程](./宏观视角上的浏览器/Chrome架构：仅仅打开1个页面，为什么有4个进程/index.md)
- [TCP协议：如何保证页面文件能被完整送达浏览器](./宏观视角上的浏览器/TCP协议：如何保证页面文件能被完整送达浏览器/index.md)
- [HTTP请求流程：为什么很多站点第二次打开速度会很快](./宏观视角上的浏览器/HTTP请求流程：为什么很多站点第二次打开速度会很快/index.md)
- [导航流程：从输入URL到页面展示这中间发生了什么](./宏观视角上的浏览器/导航流程：从输入URL到页面展示这中间发生了什么/index.md)
- [渲染流程（上）：HTML、CSS和JavaScript是如何变成页面的](./宏观视角上的浏览器/渲染流程（上）：HTML、CSS和JavaScript是如何变成页面的/index.md)
- [渲染流程（下）：HTML、CSS和JavaScript是如何变成页面的](./宏观视角上的浏览器/渲染流程（下）：HTML、CSS和JavaScript是如何变成页面的/index.md)

## 浏览器中的JavaScript执行机制

- [变量提升：JavaScript代码是按顺序执行的吗](./浏览器中的JavaScript执行机制/变量提升：JavaScript代码是按顺序执行的吗/index.md)
- [调用栈：为什么JavaScript代码会出现栈溢出](./浏览器中的JavaScript执行机制/调用栈：为什么JavaScript代码会出现栈溢出/index.md)
- [块级作用域：var缺陷以及为什么要引入let和const](./浏览器中的JavaScript执行机制/块级作用域：var缺陷以及为什么要引入let和const/index.md)
- [作用域链和闭包：代码中出现相同的变量，JavaScript引擎如何选择](./浏览器中的JavaScript执行机制/作用域链和闭包：代码中出现相同的变量，JavaScript引擎如何选择/index.md)
- [this：从JavaScript执行上下文视角讲this](./浏览器中的JavaScript执行机制/this：从JavaScript执行上下文视角讲this/index.md)

## V8工作原理

- [栈空间和堆空间：数据是如何存储的](./V8工作原理/栈空间和堆空间：数据是如何存储的/index.md)
- [垃圾回收：垃圾数据如何自动回收](./V8工作原理/垃圾回收：垃圾数据如何自动回收/index.md)
- [编译器和解析器：V8如何执行一段JavaScript代码的](./V8工作原理/编译器和解析器：V8如何执行一段JavaScript代码的/index.md)

## 浏览器中的页面循环系统

- [消息队列和事件循环：页面是怎么活起来的](./浏览器中的页面循环系统/消息队列和事件循环：页面是怎么活起来的/index.md)
- [Webapi：setTimeout是怎么实现的](./浏览器中的页面循环系统/Webapi：setTimeout是怎么实现的/index.md)
- [Webapi：XMLHttpRequest是怎么实现的](./浏览器中的页面循环系统/Webapi：XMLHttpRequest是怎么实现的/index.md)
- [宏任务和微任务：不是所有的任务都是一个待遇](./浏览器中的页面循环系统/宏任务和微任务：不是所有的任务都是一个待遇/index.md)
- [使用Promise告别回调函数](./浏览器中的页面循环系统/使用Promise告别回调函数/index.md)
- [async-await使用同步方式写异步代码](./浏览器中的页面循环系统/async-await使用同步方式写异步代码/index.md)

## 浏览器中的页面

- [页面性能分析：利用chrome做web性能分析](./浏览器中的页面/页面性能分析：利用chrome做web性能分析/index.md)
- [DOM树：JavaScript是如何影响DOM树构建的](./浏览器中的页面/DOM树：JavaScript是如何影响DOM树构建的/index.md)
- [渲染流水线：CSS如何影响首次加载时的白屏时间](./浏览器中的页面/渲染流水线：CSS如何影响首次加载时的白屏时间/index.md)
- [分层和合成机制：为什么CSS动画比JavaScript高效](./浏览器中的页面/分层和合成机制：为什么CSS动画比JavaScript高效/index.md)
- [页面性能：如何系统优化页面](./浏览器中的页面/页面性能：如何系统优化页面/index.md)
- [虚拟DOM：虚拟DOM和实际DOM有何不同](./浏览器中的页面/虚拟DOM：虚拟DOM和实际DOM有何不同/index.md)
- [PWA：解决了web应用哪些问题](./浏览器中的页面/PWA：解决了web应用哪些问题/index.md)
- [webComponent：像搭积木一样构建web应用](./浏览器中的页面/webComponent：像搭积木一样构建web应用/index.md)

## 浏览器中的网络

- [HTTP1：HTTP性能优化](./浏览器中的网络/HTTP1：HTTP性能优化/index.md)
- [HTTP2：如何提升网络速度](./浏览器中的网络/HTTP2：如何提升网络速度/index.md)
- [HTTP3：甩掉TCP、TCL包袱，构建高效网络](./浏览器中的网络/HTTP3：甩掉TCP、TCL包袱，构建高效网络/index.md)
- [同源策略：为什么XMLHttpRequest不能跨域请求资源](./浏览器中的网络/同源策略：为什么XMLHttpRequest不能跨域请求资源/index.md)
- [跨站脚本攻击XSS：为什么cookie中有httpOnly属性](./浏览器中的网络/跨站脚本攻击XSS：为什么cookie中有httpOnly属性/index.md)
- [CSRF攻击：陌生链接不要随便点](./浏览器中的网络/CSRF攻击：陌生链接不要随便点/index.md)
- [沙盒：页面和系统之间的隔离墙](./浏览器中的网络/沙盒：页面和系统之间的隔离墙/index.md)
- [HTTPS：让数据传输更安全](./浏览器中的网络/HTTPS：让数据传输更安全/index.md)
