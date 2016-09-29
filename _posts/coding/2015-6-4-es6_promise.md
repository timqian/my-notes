---
layout: post
title: ES6 promise
tags: 
- javascript
---

Good resourse：[mozila doc](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)，[Promise 迷你书](http://liubin.github.io/promises-book/)

### 基本使用方法：

1. **建一个Promise对象 `var test = new Promise(function(resolve, reject) { ... });`**

    其中传入的两个参数为 Promise对象的两个函数(`Promise.resolve(value)`,`Promise.reject(reason)`)。在匿名函数中执行`resolve(value)`时，Promise的state变为 *fulfilled*； 执行 `Promise.reject(reason)` 时，state变为 *rejected*；
    
2. **注册`then()` 和 `catch()` （then的特例）方法，等待传入这两个方法中的函数被调用。**

    `then()`,`catch()`是 `Promise.prototype`的两个方法(`Promise.prototype.then(onFulfilled,onRejected)`，`Promise.prototype.catch(onRejected)`)；传入其中的参数是**函数类型的**，当Promise对象中的函数执行`resolve()` 或者`reject()`后，Promise的state被改变，根据state的不同，`onFulfilled()`,`onRejected()`会被执行

3. **`then()` return 的是一个 Promise 对象，于是这个过程可以就重复下去了。**

### Promise chain

* 每次调用then都会返回一个新创建的promise对象

理解下这两句话(来自：[mozila doc](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise))：
`Promise.prototype.catch(onRejected)`
Appends a rejection handler callback to the promise, and returns a new promise resolving to the return value of the callback if it is called, or to its original fulfillment value if the promise is instead fulfilled.
`Promise.prototype.then(onFulfilled, onRejected)`
Appends fulfillment and rejection handlers to the promise, and returns a new promise resolving to the return value of the called handler.

### 例子：见：[mozila doc](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)，[Promise 迷你书](http://liubin.github.io/promises-book/)