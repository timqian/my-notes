---
layout: post
title: Use es6 today 笔记
tags:
- javascript
---

## 历史

- TC39(Ecma Technical Committee 39): the committee evolving js
- Goals for es6: better ..
    - for complex app
    - for libraries
    - as a target of code generators

## How to upgrade a web language

挑战：
- new versions = forced upgrades
- 现有代码必须能跑

How ES features are designed:
- design by "champions" (一到两个专家，而不是committee)
- TC39 和committee 反馈
- TC39 最终决定何时/是否发布

## Variables and scope

### let: Block-scoped variables(more local)

```javascript
function order(x, y) {
  if (x>y) {
    var tmp = x;
    x = y;
    y = tmp;
  }
  console.log(tmp === x); //true
  return [x, y];
}
```

```javascript
function order(x, y) {
  if (x>y) {
    let tmp = x;
    x = y;
    y = tmp;
  }
  console.log(tmp === x); //tmp is not defined
}
```
### Symbols: new kind of primitive value - unique IDs(much like a string) - joining strings, numbers, booleans, null and undefined.

for extensibility

常作为key of 一个function

```javascript
let specialMethod = Symbol();
obj[specialMethod] = function (arg) {
  ...
};
obj[specialMethod](123);
}
```
