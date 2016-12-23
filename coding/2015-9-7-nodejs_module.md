---
layout: post
title: nodejs 模块
tags:
- javascript
---

## module 对象

每个js文件，被node编译过程中，会传入module对象，
(被`(function (exports, require, module, __filename, __dirname) {
    .....
});`包装)当一个文件直接被node运行，require.main
会被设为该module，因此可以通过
`require.main === module`，来判断文件是直接被运行的还是被其他模块require后运行的

## 模块定义方法：

{% highlight js %}
// cicle.js
var PI = Math.PI;
module.exports.area = function (r) {
    return PI * r * r;
};
module.exports.circumference = function (r) {
    return 2 * PI * r;
};
{% endhighlight %}

## 模块使用方法：

{% highlight js %}
var circle = require('./circle.js');
circle.area(4); //16PI
{% endhighlight %}

## module.exports

{% highlight js %}
// cicle.js
var PI = Math.PI;
module.exports.area = function (r) {
    return PI * r * r;
};
module.exports.circumference = function (r) {
    return 2 * PI * r;
};
module.exports = '8';
{% endhighlight %}
此时：
{% highlight js %}
var circle = require('./circle.js');
circle.area(4); // 会出错！！
{% endhighlight %}

**注意**：如果出现 `module.exports = ...` export的其它的东西会被忽略：

node 文档：

If you want the root of your module's export to be a function (such as a constructor) or if you want to export a complete object in one assignment instead of building it one property at a time, assign it to module.exports instead of exports.
## module 中的变量会被包在一个函数中，防止污染全局变量

如果想要操纵module中的变量，可以暴露出操纵函数

## exports 与 module.exports 基本是一样的但不要混着用。。。

## 参考

http://www.hacksparrow.com/node-js-exports-vs-module-exports.html
http://www.infoq.com/cn/articles/nodejs-module-mechanism
http://www.hacksparrow.com/node-js-exports-vs-module-exports.html
