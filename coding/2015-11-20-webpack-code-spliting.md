---
layout: post
title: react 项目代码拆分
tags:
- javascript
---

在使用 react 和 react-router 开发应用时， 当应用变大， 将 bundle.js 根据不同的 route 打包的需求出现了(code split)。
查了下， webpack 可以帮你做这件事。

## 参考：

官方文档和例子：
[文档](https://webpack.github.io/docs/code-splitting.html)
[例子](https://github.com/webpack/webpack/tree/master/examples/code-splitting)

与react-router组合的例子：
[https://github.com/rackt/react-router/blob/master/examples/auth-with-shared-root/config/routes.js](https://github.com/rackt/react-router/blob/master/examples/auth-with-shared-root/config/routes.js)

## 总结：

// TODO
