---
layout: post
title: Pseudospin in Graphene
tags: 
- quantum mechanics
---


# 1. Starting point (Datta 2006)

## 1.1 紧束缚近似下，晶体中电子满足的方程：

$$
[h(\vec{k})] \{\phi_0\} = E \{\phi_0\}                                                    \tag{1}
$$

with

$$
[h(\vec{k})] = \sum_m [H_{nm}] e^{i \vec{k} \cdot (\vec{d_m} - \vec{d_n})}                 \tag{2}
$$

## 1.2 应用到 Graphene

<center><img src = '/public/blogfigure/2015-5-7-graphene.jpg'></img></center>

$$
H_{nn} = 
  \begin{matrix}
         & |nA> & |nB> \\
    |nA> &  0   & -t   \\
    |nB> & -t   & 0
  \end{matrix}                                                         
$$

and

$$
H_{n1} = 
  \begin{matrix}
         & |1A> & |1B> \\
    |nA> &  0   & 0    \\
    |nB> & -t   & 0
  \end{matrix} 
$$

$$
H_{n3} = 
  \begin{matrix}
         & |2A> & |2B> \\
    |nA> &  0   & -t    \\
    |nB> &  0   & 0
  \end{matrix}                                                                           \tag{3}
$$

同理， $$H_{n2} $$, $$ H_{n4}$$ 也可以写出来。将它们代入 $$(2)$$ 式就可以得到 $$[h(\vec{k})]$$ 的形式为：

$$
[h(\vec{k})] =
 \left[
 \begin{matrix}
   0      &  h_0\\
   h_0^*  &  0 
  \end{matrix}
  \right] 
$$

where

$$
h_0 =  -t(1 + e^{ i \vec{k} \cdot \vec{a1} } + e^{i \vec{k} \cdot \vec{a2}}) = -t( 1 + 2 e^{i k_x a_0} \cos(k_y b_0))     \tag{4}
$$

可以根据 $$(1)$$ 式得到电子的能量本征值：

$$
E(\vec k)=\pm t\sqrt{1 + 4 \cos k_y b_0 \cos k_x a_0 + 4 \cos^2 k_y b_0}
$$

【能带图片】

# 2. Graphene 中，电子在费米面附近的性质----Pseudospin

## 电子性质：

* 在费米面附近，电子的Hamiltonian：

$$
H = \pm \hbar v_F \vec{\sigma} \cdot \vec{k}
$$

由于此时电子的Hamiltonian形式与Dirac-Weyl equation 一样，所以叫 Pseudospin。
Dirac-Weyl equation: （本来是用来描述0质量，自旋1/2的费米子的）

$$
H = \pm \hbar c \vec{\sigma} \cdot \vec{k}
$$



## 证明

### 方法一：对哈密顿量（$$h(\vec k)$$）在狄拉克点( $$K$$, $$K'$$ )附近作泰勒展开

$$
[h(\vec k_1)] = \frac{3ta}{2}

 \left[
 \begin{matrix}
   0            &  k_x - i k_y   \\
   k_x + i k_y  &  0 
  \end{matrix}
  \right] 
  
= \hbar v_F \vec{\sigma} \cdot \vec{k_1}
$$

where

$$
v_F = \frac{3ta}{2 \hbar}
$$

其中，$$\vec k_1$$, 为k空间中相对$$K$$点的坐标；a 为碳原子之间的距离。

### 方法二：对$$E(\vec k)$$ 在狄拉克点附近作泰勒展开，再由能谱去构造哈密顿量


# 附录： Starting point 是怎么来的

[Quantum Transport by Datta P110](http://www.researchgate.net/publictopics.PublicPostFileLoader.html?id=549285f1d3df3e197b8b46b2&key=b52d5541-e5e4-4fbc-a189-54576a1f2daa)

<script type="text/javascript" src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS_HTML"></script>