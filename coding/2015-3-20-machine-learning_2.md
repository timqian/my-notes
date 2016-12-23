---
layout: post
title: Stanford machine learning 笔记2
tags: 
- machine learning
---

* 监督学习之----线性回归(regression)问题的数学表述和Gradient descent算法

## 问题描述

给定一组数据 (x, y)，寻找与其最为接近的函数（hypothesis）：$$ h_{\theta}(x) = \theta_0 + \theta_1 x$$

### 符号说明

* m = 训练数量
* x's = input variable/features
* y's = output
* (x, y) = 一组训练数据
* $$(x_i, y_i) = i_{th}$$ 训练数据

### 监督学习过程：
<center><img src = '/public/blogfigure/supervised_learning.png'></img> </center>


## 如何寻找最好的参数（$$\theta_0, \theta_1$$）：Minimize **Cost function**

思路: 选择$$\theta_0, \theta_1$$ 使得对于我们的training examples $$(x,y)$$, $$h_{\theta}(x) $$与 $$y$$ 最接近。

数学表述：

$$
J(\theta_0, \theta_1) = \frac{1}{2m} \sum^m_{i=1} \left( h_{\theta}(x_i) - y_i \right)^2  \\
Mimimize_{\theta_0, \theta_1} \quad J(\theta_0, \theta_1)
$$

$$J$$ 就是 Cost function（square error cost function）。在这里， cost function 是一个二元函数：
<center><img src = '/public/blogfigure/contour_for_j.png'></img> </center>

怎样才能快速得找到使得cost function 最小的参数呢？可以用梯度下降算法

## 梯度下降算法(Gradient descent algorithm)

**Outline**: 1. 初始化 2. update参数直到最小
**算法：**

$$
repeat until convergence: \\
    \theta_j := \theta_j - \alpha \frac{\partial}{\partial \theta_j} J(\theta_0, \theta_1) \quad (for \; j = 0 \, and \, j = 1) 
$$


注：

* "$$:=$$" means Assigenment
* $$\alpha$$： learning rate
* 越接近local minimum，step 会变小，因为导数变小

## 在本问题中使用梯度下降算法
 
关键：$$\frac{\partial}{\partial \theta_j} J(\theta_0, \theta_1) $$ 是多少

对 $$J(\theta_0, theta_1)$$ 求导可得：

$$
\frac{\partial J(\theta_0, \theta_1)}{\partial \theta_0} = \frac{1}{m} \sum_{i=1}^m \left( h_{\theta}(x_i) - y_i \right) \\

\frac{\partial J(\theta_0, \theta_1)}{\partial \theta_1} = \frac{1}{m} \sum_{i=1}^m \left( h_{\theta}(x_i) - y_i \right) x_i
$$

有了这两个结果，就可以带入上面的算法求h了！

**注：**

* 这是一种 "Batch" Gradient Descent。因为每一步都用到了所有的training examples



<script type="text/javascript"
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>



