---
layout: post
title: ES6 `=>` 函数
tags: 
- javascript
---


## 用 `=>` 定义函数（Arrow Function）

有两个好处：

### 1.  less ceremony when defining an anonymous function

例子：
{% highlight js%}
var x = [0,1,2];
x.map(function (x) { //anonymous function
  console.log(x * x);
});
{% endhighlight %}
等价于

{% highlight js%}
let x = [0,1,2];
x.map(x => console.log(x * x)); //arrow function
{% endhighlight %}
    
### 2. lexical scoping of the this keyword

{% highlight js%}
function Car() { //Note, we could use the new Class feature in ES6 instead
  this.speed = 0;

  setInterval(() => {
    this.speed += 5; //this is from Car arrow function 没有自己的this！
    console.log
    console.log('now going: ' + this.speed);
  }, 1000);
}
{% endhighlight %}

用es5写需要这样，因为每个函数定义时，this都会指向调用它的object
{% highlight js%}
function Car() {
  var self = this; //locally assign this that can be closed over
  self.speed = 0;

  setInterval(function goFaster() {
    //this has a different scope, but we can use the self variable to reference the parent "this"
    self.speed += 5;
      console.log('now going: ' + self.speed);
  }, 1000);
}

var car = new Car();
{% endhighlight %}

