---
layout: post
title: javascript 函数式编程总结
tags:
- 函数式编程
---

对在[这个网页](http://reactive-extensions.github.io/learnrx/)中学到的总结

# Working with Arrays

## - `forEach(操作)`:

对每个元素做相同的操作，**Traversing**

## - `map(操作)`:

对每个元素做相同地操作，并产出一个新元素(返回一个新的数组)**Projecting**

## - `filter(操作)`:

对每个元素做相同的操作，如果操作return true，在新数组中保留该元素，否则不保留（返回一个新的数组）

> 可以通过组合`map()`,`mergeAll()`,`filter()` 从tree结构(Array的元素是Object，
Object的属性又是Array。。。)中获取任意想要的数据

> `map()`和`mergeAll()`可以组合在一起，成为`flatMap()`;(在传入函数中有`map`时用！
因为`map`套`map`之后数组维度增加了)

## - `reduce(callback(pre, cur), initialValue)`:

initialValue 为可选.
如果给定 initialValue, callback() 第一次执行时 pre 值为 initialValue, cur 为数组第一个元素, 否则 pre 为数组第一个元素, cur 为数组第二个元素
第二次执行 callback() 时, pre 为 callback() 上一次 return 的值, cur 为数组下一个元素.
以此类推, 直到没有下一个元素时, callback() 的 return 值就是 reduce() 的返回值

使用例子:

0. 对数组临近两个元素做操作


1. 数组求和

```javascript
var a = [0, 1, 2, 3, 4].reduce(function(pre, cur, index, array) {
  return pre + cur;
});

// a = 10
```

2. 把Array转换成其他类型：[{id:2, title:'hi'},{id:3, title:'hh'}] ==>{2:'hi', 3:'hh'}:

```javascript
[{id:2, title:'hi'},{id:3, title:'hh'}].reduce(
  function(acc, cur){
    acc[cur.id] = cur.title;
    return acc
  }
,{})
```
## - `zip(left, right, combinerFunction)`: combinerFunction 对 left 数组和 right 数组中元素同时做操作，最终返回一个数组

## - 待续
