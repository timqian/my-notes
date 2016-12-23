---
layout: post
title: javascript tips
tags:
- javascript
---

## Array对象的`map()`函数与`forEach()`的区别：

    * `forEach`方法对所有元素依次执行一个函数，改变数组
    * `map`方法对所有元素依次调用一个函数，根据函数结果返回一个新数组,不改变数组

例子：

foreach：

{% highlight js%}
[1, 2, 3].forEach(function(elem, index, arr){
    console.log("array[" + index + "] = " + elem);
});
// array[0] = 1
// array[1] = 2
// array[2] = 3
{% endhighlight %}

接受3个参数：当前元素、当前元素的位置（从0开始）、整个数组。
map：

{% highlight js%}
var a = [1, 2, 3].map(function(elem, index, arr){
    return elem * elem;
});
// a = [1, 4, 9]
{% endhighlight %}

## function 对象的 apply 函数：`fun.prototype.apply(thisArg, [argsArray])`

1. 为`fun`提供 `thisArg` 作为 `fun` 中的 `this`;
2. [argsArray] 作为参数提供给 `fun`

> 与`fun.prototype.call(thisArg, arg1, arg2, ...)`的区别在于它接受的参数不是 array like 
