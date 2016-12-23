---
layout: post
title: 用 Mocha 做单元测试
tags: 自动化测试
---

### 最简单的使用方式：（测试Array对象的indexOf()函数）：

{%highlight js%}
var assert = require("assert");
describe('测试indexOf方法', function(){
    it('should return -1 when the value is not present', function(){
        assert.equal(1, [1,2,3].indexOf(5), '这是错误信息');
    })
});
{%endhighlight%}

### 用到的函数：

`describe (moduleName, testDetails)`：描述本次测试，其中`testDetail`是测试主体

`it (info, function)`：具体测试语句放在it回调函数中；`info`字符串常用以说明期望的正确输出

`assert.equal (exp1, exp2, msg)`：判断两个表达式是否相同，不同就输出`msg`

### hooks: 测试之前，之后的动作：

{%highlight js%}
describe('hooks', function() {

  before(function() {
    // runs before all tests in this block
  });

  after(function() {
    // runs after all tests in this block
  });

  beforeEach(function() {
    // runs before each test in this block
  });

  afterEach(function() {
    // runs after each test in this block
  });

  // test cases
});
{%endhighlight%}