---
layout: post
title: 这样赌，一定赢？
tags: 
- mathmatic
---
## 0. 核心科技

室友称自己掌握了赌博的核心科技(虽然目前应用地不是很顺利)。于夜深人静之时传授于我，陈述如下：

**记住！如果你第一次输了，第二次就将赌注加倍；如果第二次又输了，再将赌注加倍；...依次类推，不管赢的概率再小，照这种方式操作，只要你有足够多的钱，总会等到赢的那一次。然后，你就赚到了你想赢得钱！！！**
听起来好有道理！如果你已经忍不住想试一下，你可以去 [网易彩票 - 新快3](http://caipiao.163.com/order/gxkuai3/#from=leftnav) 猜数字。合法赌博！

不过，这种方法是否真的像看上去那么有效？还是先拿 *概率论* 来学以致用一下，毕竟关系到RMB啊。。

## 1. 貌似挺对

假设赌博胜负的概率*真的是*随机的，每一次赢的概率为 $$p$$。我们一共进行n次赌博。那么，
在第一次赢的概率就是： $$p$$；
在第二次赢的概率是： $$(1-p)p$$（条件概率，还记得吧）；
在第三次：$$(1-p)^2p$$；
...
在第n次：$$(1-p)^{n-1} p$$。

下图说明了当$$p=0.4$$时，在第n次获胜的概率：

<center>
	<span>在第n次获胜的概率</span>
	<canvas id="canvas" height="300" width="700"></canvas>
</center>

利用等比数列前n项和公式可得，在前n次赢的概率是：

$$P_n = p + (1-p)p + (1-p)^2 p + \dots + (1-p)^{n-1} p = 1-(1-p)^n $$ 

容易证明：

$$
\lim_{n \to \infty} P_n = 1
$$

也就是说，如果你不差钱，利用刚刚的规则，的确，总有一天会赢的。来看看当 $$p=0.4$$时，在**前**n次获胜的概率：

<center>
	<span>在<b>前</b>n次获胜的概率</span>
	<canvas id="canvas2" height="300" width="700"></canvas>
</center>

然而现实生活总是差钱的，看看这种策略是怎么花钱的应该不是坏事。

## 2. 考虑成本

假设我们的目标收益是 $$1$$ 元，在第n次下注时我们所投入的总资金：

第一次：1元
第二次：2元
第三次：4元
第四次：8元
...
第n次：$$2^{n-1}$$ 元
总投入：$$M = 1 + 2^1 + 2^2 + \dots + 2^{n-1}$$ 元

来看一下 $$M, n$$ 的关系：

<center>
	<span>在<b>前</b>n次的总投入M</span>
	<canvas id="canvas3" height="300" width="700"></canvas>
</center>

在真实生活中，我们可以输掉的钱是有限的（从图中可以看出，如果第35次还没赢，需要投入350亿元，不是马云的儿子，敢玩？）。

由于资金的限制，导致我们无法玩无穷多次，于是，我们就有可能会输了（很遗憾）。可以来计算一下，当我们有一定的预算（$$M$$）时，期望收益($$E$$)是多少。但是要怎么计算期望呢？先来看一个例子：
假设预算是$$3$$元，那么，最多可以赌两次。于是赢的概率是 $$P_{win} = 1 - (1-p)^1$$；期望收益可以用下式表示：

$$
E = p_{win} \times 1 - (1-p_{win}) \times 3
$$

按照这样的方法，我们可以计算出不同预算对应的期望收益。

还是以$$p=0.4$$为例，期望与预算的关系如图所示，为方便起见，这里的预算取为作n次总投资所需要的资金：

<center>
	<span>期望收益与预算的关系</span>
	<canvas id="canvas4" height="300" width="700"></canvas>
	<small>预算</small>
</center>

看到这张图，我好像明白了什么，，你呢 SiPu You？


<script src="http://cdn.bootcss.com/Chart.js/1.0.2/Chart.js"></script>
<script src="http://cdnjs.cloudflare.com/ajax/libs/jquery/2.1.3/jquery.min.js"></script>
<script>
	var p = 0.4; //winning probability
    var n = 35;  //trial #

    var x_axis = []; //x 轴

    var Pn = [];  //在第n次内中奖的概率
    var P = 0; //temp

    var PPn = [];  //前n次内中奖的概率
    var PP = 0;

    var Mn = []; //n次总投资数组
    var M = 0; //temp

    var En = []; //第n次投资的期望收益
    var E = 0; //temp
    for(var i=1; i<=n; i++){
    	x_axis.push("前" + i + "次");

    	P = Math.pow(1-p, i-1) * p;
        Pn.push(P);

        PP = 1 - Math.pow(1-p, i);
        PPn.push(PP);

        M += Math.pow(2, i-1);
        Mn.push(M);

        E = 1 * PP - (1 - PP) * M;
        En.push(E);
    }

	var lineChartData = {
		labels : x_axis,
		datasets : [
			{
				label: "1",
				fillColor : "rgba(151,187,205,0.2)",
				strokeColor : "rgba(151,187,205,1)",
				pointColor : "rgba(151,187,205,1)",
				pointStrokeColor : "#fff",
				pointHighlightFill : "#fff",
				pointHighlightStroke : "rgba(151,187,205,1)",
				data : Pn
			}
		]
	}

	var lineChartData2 = {
		labels : x_axis,
		datasets : [
			{
				label: "2",
				fillColor : "rgba(151,187,205,0.2)",
				strokeColor : "rgba(151,187,205,1)",
				pointColor : "rgba(151,187,205,1)",
				pointStrokeColor : "#fff",
				pointHighlightFill : "#fff",
				pointHighlightStroke : "rgba(151,187,205,1)",
				data : PPn
			}
		]

	}

	var lineChartData3 = {
		labels : x_axis,
		datasets : [
			{
				label: "3",
				fillColor : "rgba(151,187,205,0.2)",
				strokeColor : "rgba(151,187,205,1)",
				pointColor : "rgba(151,187,205,1)",
				pointStrokeColor : "#fff",
				pointHighlightFill : "#fff",
				pointHighlightStroke : "rgba(151,187,205,1)",
				data : Mn
			}
		]

	}

	var lineChartData4 = {
		labels : Mn.map(function(elem){return elem + '元'}),
		datasets : [
			{
				label: "4",
				fillColor : "rgba(151,187,205,0.2)",
				strokeColor : "rgba(151,187,205,1)",
				pointColor : "rgba(151,187,205,1)",
				pointStrokeColor : "#fff",
				pointHighlightFill : "#fff",
				pointHighlightStroke : "rgba(151,187,205,1)",
				data : En
			}
		]

	}

window.onload = function(){
	var ctx = document.getElementById("canvas").getContext("2d");
	window.myLine = new Chart(ctx).Line(lineChartData);

	var ctx2 = document.getElementById("canvas2").getContext("2d");
	window.myLine2 = new Chart(ctx2).Line(lineChartData2);		

	var ctx3 = document.getElementById("canvas3").getContext("2d");
	window.myLine3 = new Chart(ctx3).Line(lineChartData3);	

	var ctx4 = document.getElementById("canvas4").getContext("2d");
	window.myLine4 = new Chart(ctx4).Line(lineChartData4);	

}
</script>

<script type="text/javascript" src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS_HTML"></script>