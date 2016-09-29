---
layout: post
title: 从哈密顿量出发，理解多电子原子的“轨道模型”和它的磁矩
tags: 
- quantum mechanics
---

* （字太多！讲要点就好了！逻辑关系）由原子的哈密顿量出发，经过近似和微扰，得到“原子轨道模型”

若仅考虑库伦相互作用，拥有N个电子的原子的哈密顿量可以这样表示：

$$
H = \sum_{i=1}^N \left[ -\frac{1}{2} \nabla_i^2 - \frac{Z}{r_i} \right] + \sum_{i>j} \frac{1}{ r_{ij} }
$$

然而遗憾的是这个哈密顿量很难解（why?），前人最有经验的问题是单粒子问题，于是，最暴力的近似方式是直接忽略电子与电子之间的相互作用。这样的近似下，可以通过分离变量法将多粒子问题转化为单粒子问题。但是，电子与电子之间的相互作用与电子与核的相互作用应该在一个档次（都是库伦相互作用，电荷量又差不多）。可想而知，这样做误差会很大。于是有人想到一种既可以分离变量，误差又没那么大的方法：中心力场近似。

## Central field approximation(中心力场近似)

用一个中心对称的势能函数来近似其余电子对某个电子的作用。而且，每个电子体验到的势能函数都一样。由于原子核对电子的作用也是中心对称的，我们可以把二者合写为：$$U(r)$$，于是哈密顿量可以表示为：

$$
H =  \sum_{i=1}^N \left[ -\frac{1}{2} \nabla_i^2 + U(r_i) \right] + H_{res}
$$

其中$$H_{res}$$ 代表residual hamiltonian，是电子相互作用非中心对称部分，把它看做小量。如果先忽略$$H_{res}$$，那么对于的schrodinger方程就可以分离变量，转化为单粒子问题。只不过这里的$$U(r)$$ 与电子波函数有关，也就是说，我们要知道了电子的状态，才能得到 $$U$$。这种问题常用[自洽场方法](http://zh.wikipedia.org/wiki/%E8%87%AA%E6%B4%BD%E5%9C%BA%E6%96%B9%E6%B3%95)处理(Self-Consistant Field method)。
我们可以用单粒子波函数构造体系的波函数：

\begin{equation}
| \Psi \rangle = |\psi_a(r_1,\chi_1)\rangle |\psi_b(r_2,\chi_2)\rangle |\psi_c(r_3,\chi_3)\rangle ... 
= \frac{1}{\sqrt{N!}} 
\left[             %左括号
  \begin{array}{ccc}   %该矩阵一共3列，每一列都居中放置
    |\psi_a(r_1,\chi_1)\rangle  & |\psi_b(r_1,\chi_1)\rangle  & ...\\ 
    |\psi_a(r_2,\chi_2)\rangle  & |\psi_b(r_2,\chi_2)\rangle  & ...\\ 
    ...                         & ...                         & ... \\
  \end{array}
\right]
\end{equation}

\begin{equation}
\left[             %左括号
  \begin{array}{ccc}   %该矩阵一共3列，每一列都居中放置
    |\psi_a(r_1,\chi_1)\rangle  & |\psi_b(r_1,\chi_1)\rangle  & ...\\ 
    |\psi_a(r_2,\chi_2)\rangle  & |\psi_b(r_2,\chi_2)\rangle  & ...\\ 
    ...                         & ...                         & ... \\
  \end{array}
\right]
\end{equation}

其中的单粒子态是分离变量之后的的schrodidnger方程的解：

$$
\left[ -\frac{1}{2} \nabla^2 + U(r) \right] |\psi_i(r,\chi)\rangle = E_i |\psi_i(r,\chi)\rangle
$$

需要记住的是：所有电子都是一样的，所谓电子占据轨道只是一种形象化的说法。其本质是电子系统波函数需要满足反对称关系。
另外，由于$$U(r)$$ 是中心对称的，因此单粒子哈密顿量与角动量算对易，电子角动量守恒。因此电子的状态还是可以用 $$n, l, m_l$$来表示，与氢原子不同之处在于，能量不再只与 n 有关，还和l有关了。具体计算过程可以在[这里找到]()。
计算结果可以用以下这个图片来表示：
<center><img src = '/public/blogfigure/2014-4-1.png'></img></center>
在中心力场近似下，可以得到原子能级的分布图(Aufbau Principle)：
<center><img src = '/public/blogfigure/2014-4-1-energy.png'></img></center>
从这幅图中我们可以看出，由于电子之间的相互作用，









$$
H =  -\frac{1}{2} \nabla^2 - \frac{1}{r}
$$








$$
H = \sum_{i=1}^N \left{ -0.5 \nabla_i^2 - \frac{Z}{r_i} \right. + \sum_{i>j} \frac{1}{ r_{ij} } + H_{s-o}
$$

其中，$$H_{s-0}$$ 代表自旋轨道耦合作用。首先我们忽略自旋轨道耦合项（后面用微绕论加进来）。那么哈密顿量就变成：























* 磁铁为什么有磁性？当然是因为构成磁铁的原子有磁性咯。那么原子的磁性又是怎么来的呢？学过原子物理的你可能已经知道，原子的基态磁矩可以根据 Hund 规则得到。本文的目的有二：一是从原子的Hamiltonian出发，告诉你 Hund 定则是怎么来的；二是告诉你如何利用 Hund 定则计算原子的磁矩。


## Hund 规则及其限制

Hund 总结了光谱数据得到了如

## 从 Hund 规则计算原子磁矩

## Hund 规则是怎么来的

我们从原子的哈密顿量出发：

$$

$$

第一步近似：得到与氢原子类似的能级结构，形象地理解为电子占据能级，但其实所有电子完全一样。一个态最多有一个电子占据的原因是体系波函数的反对称要求决定。

第二步近似：剩下的静电势能。导致了








* 我希望从哈密顿量出发，理解物质磁性的量子力学起源。麦克斯韦告诉我们，物质的磁性来自于磁矩，而磁矩来自于带电物体运动圆周运动（如果不是圆周运动会如何？）。物质由原子组成，原子由电子和原子核组成。在我们的故事中，做圆周运动的带电物体指的是电子。电子的轨道和自旋角动量，就是物质磁性的主要来源。要理解物质磁性的起源，我想，首先自然需要理解组成物质的原子的磁性咯。原子中的那么多电子，是如何在量子力学的指导下，为我们显现出这奇妙的磁性的呢？-----写得太糟糕，需要修改！



<script type="text/javascript" src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS_HTML"></script>