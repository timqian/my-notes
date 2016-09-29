---
layout: post
title: ES6 模块
tags: 
- javascript
---

nodejs 使用Commonjs 语法来编写模块(关键词：`require`, `export`)；而es6拥有了自己的原生语法。不管是函数，对象，还是变量，都可以从模块中export出来

## 一个模块中export多个东西

{% highlight js%}
//globals.js
export var API_ENDPOINT = 'http://api.app.com/'
export var API_VERSION  = 1;

// importing them in app.js. Note that .js can be omitted
import { API_ENDPOINT, API_VERSION } from 'globals';
{% endhighlight %}

## 使用`default`关键词export出整个模块

{% highlight js %}
//person.js
class Person {
    constructor() {
        this.age = 0;
        this.gender = 'Unknown';
    }
}
export default Person;

// import in app.js
import Person from 'person';
{% endhighlight %}