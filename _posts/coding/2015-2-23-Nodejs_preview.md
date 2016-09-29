---
layout: post
title: Nodejs入门
tags: 
- javascript
---

*nodejs 是运行在服务端的javascript代码。具有异步风格，充分利用了js事件驱动的特性。。。其实我还不太懂，这里记录下基本的使用方法及一些注意事项*

	
### 同步与异步

- 同步代码（阻塞）（传统服务器）：同步的代码意味着在前一次操作完成之前，代码的执行会被阻塞
- 异步代码（非阻塞）（node方式）：脚本无需等待某个操作完成就能继续前进，操作结果会在事件发生时由回调来处理（内部并行执行仍任务）。


### 回调：将一个函数作为参数传递给另一个函数，且常在另一个函数完成后被调用

例子：

{% highlight js %}
//函数f作为参数传递给test()
function test(c,f){
	console.log('Content is' + c);
	f();
}

test('test',function(){
	console.log('a test');
});

//运行后在console中输出：
Content is test
a test
{% endhighlight %}	

其中`f()` 是作为参数传递给`test()`。

### 在node中如何使用回调：

**例1**：读取文件，完成后执行回调函数：

{% highlight js %}
//请求filesystem模块(详见http模块说明)
var fs = require('fs');
//传递3个参数给readFile()函数，最后一个参数是回调函数
fs.readFile('file.txt', 'utf8', function (err, data) {
    if (err) { throw err; }
    console.log(data);
});
{% endhighlight %}

其中：
- 当`fs.readFile()`函数运行时，将会以utf8格式读取*file.txt*文件，当读取完成，调用回调函数，并将`err, data`两个参数传递过去。
- err 为'true'说明读取文件发生错误；data代表读取到的数据。

**例2**：使用http模块，对特定网站做get请求(HTTP客户端)

{% highlight js %}
//请求http模块（详见http模块说明）
var http = require('http');
//传递两个参数给http.get()函数，后一个是回调函数
http.get({ host: 'shapeshed.com' }, function(res) {
    console.log("Got a response from shapeshed.com");
}).on('error', function(e) {
    console.log("There was an error from shapeshed.com");
});

http.get({ host: 'www.bbc.co.uk' }, function(res) {
    console.log("Got a response from bbc.co.uk");
}).on('error', function(e) {
    console.log("There was an error from bbc.co.uk");
});
{% endhighlight %}

其中：	
	两个http.get()操作执行回调函数的时间顺序不确定！若要操作顺序执行，可用回调方式。

