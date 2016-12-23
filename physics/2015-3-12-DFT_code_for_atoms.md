---
layout: post
title: 基于密度泛函理论(DFT)，使用matlab求解原子状态
tags: 
- quantum mechanics
---

* 使用自洽场方法求解 Kohn-Sham 方程

## 一. DFT简述（使用Atomic units）

密度泛函理论主要由 Kohn 和沈吕九在半个世纪之前创造。用于求解多电子体系基态性质，其主要思想是这样的：

**首先**：假设一组波函数 $$\{\psi_i(\vec x)\}$$ 描述了电子们的状态

**然后**：由 $$\{\psi_i(\vec x)\}$$ 导出体系能量的表达式(包含电子动能，库伦能等)：
1. 电子动能：$$ T_{el} = -\frac{1}{2} \sum_{i=1}^{n}  \int \psi_i^*(\vec x) \nabla^2 \psi_i(\vec x) d^3x $$
2. 电子与原子之间相互作用能： $$ V_{ext} = \int n(\vec x) V_{nuc}(\vec x) d^3x $$
3. 电子受其他电子的库伦能：$$V_H = \frac{1}{2} \int \phi(\vec x) n(\vec x) d^3x $$，其中$$\phi(\vec x)$$ 为电子电荷密度形成的库伦式，可以通过求解 Poisson 方程（$$ \nabla^2 \phi = - 4 \pi n$$）得到 
4. 对库伦能的修正（交换能）：$$E_{x} = \int f_x(n(\vec x)) dV  $$

*注*：
其中：$$n(\vec x) = \sum_i  \psi_i^* \psi_i  $$ 为电子密度；
对于交换能$$E_{x} $$，有各种近似方法，这里使用最简单的局域密度近似。具体介绍可以在[这里找到](http://en.wikipedia.org/wiki/Local-density_approximation)。

> 寻找更好的交换能函数，是凝聚态中一个十分重要的研究课题。

综上，可以得到总能量表达式为：

$$E[\{ \psi_i(x)\}] = T_{el} + V_{ext} + V_H + E_{x}$$

**最后**：利用变分法，求解使体系能量最小时波函数需要满足的条件，就可以得到著名的Kohn-Sham 方程：

$$
    \left[ -\frac{\hbar^2}{2m} \nabla^2 + V_{ext}(\vec x) + \phi(\vec x) + V_{x}(\vec x) \right] \psi_i(\vec x) = \epsilon_i \psi(\vec x)
$$

其中$$V_{x}$$ 为交换势, 具体表达式见[这里（局域密度近似）](http://en.wikipedia.org/wiki/Local-density_approximation)

令人吃惊的是，它与单电子 Schrodinger 方程是如此的相似。不同之处只是在于，由于电子之间相互作用，Hamiltonian 中的势能项包含了电子密度。这使得K-S方程成为一个非线性方程（哈密顿量与波函数有关），与我们熟知的本征值问题不太一样。接下来，介绍如何编程解这个方程。


## 二. 求解 Kohn-Sham 方程的自洽场(self-consistent field method SCF)算法

**Initialization**: 
1. 确定电子个数（N）
2. 用外势能近似总势能，即 $$V_{tot} = V_{ext}$$，得到近似Hamiltonian；
**Iteration**：
1. 求Hamiltonian最小的 N/2 个本征值，及对应的本征函数 $$\psi_i(\vec x)$$（每个态上占据两个电子）
2. 由得到的本征函数集 $$\{\psi_i(\vec x)\}$$ 求交换势（$$\phi(\vec x)$$）和库伦势（$$V_{x}(\vec x)$$）
3. 更新Hamiltonian: $$H = -\frac{\hbar^2}{2m} \nabla^2 + V_{ext}(\vec x) + \phi(\vec x) + V_{x}(\vec x)$$
4. 判断当前结果是否满足要求，如果满足，就跳出循环


## 三. 算法的 Matlab 实现

使用条件及近似方式：

> 只考虑电子成对占据某一能态的原子；
使用[LDA近似](http://en.wikipedia.org/wiki/Local-density_approximation)；
使用空间离散化的方法求解Hamiltonian的本征值；
使用[Dirichlet边界条件](http://en.wikipedia.org/wiki/Dirichlet_boundary_condition)（边界处概率密度为0）；
以4个电子为例。

主程序：

{% highlight matlab %}
%For double occupation
N = 4;  % num of enectrons
g = 50  % num of lattices
g3 = g^3;
p = linspace(-5, 5, g);         % one dimensiton space lattice
[X, Y, Z] = meshgrid(p, p, p);  % three dimension space lattice
h = p(2) - p(1);                % latice spacing
X = X(:); Y = Y(:); Z = Z(:);   % all elements of arraty as a single column
R = sqrt(X.^2 + Y.^2 + Z.^2);   % distance from the center
Vext = -N ./ R;                 % potential energy(2 protons)
e = ones(g,1);               
L = spdiags([e -2*e e], -1:1, g, g) / h^2; % 1D finite difference Laplacian (with 0 boundary condition)
I = speye(g);
L3 = kron(kron(L,I), I) + kron(kron(I, L), I) + kron(kron(I, I), L);  % extend Laplacian to 3 D
Vtot = Vext;  %initial guess
ncomp = exp(-R.^2/2);  %compensation charge(for poisson equation)
ncomp = -N * ncomp / sum(ncomp) / h^3;
ncomppot = -N./R.*erf(R/sqrt(2));   %solution of poisson eq. of compensation charge
%%%%%%%%initial guess for N = 4%%%%%%%%%%%%%%%%%%

E = [ -4 -1 ];
PSI = [ exp(-3.7*R) exp(-0.17*R) ];
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
for iter = 1:5 %Do the main loop not for ever
  H = -0.5 * L3 + spdiags(Vtot, 0, g3, g3);  % Hamiltonian of Helium
  [PSI, E] = lowestNEigen(H, PSI, E, N, 5);
  
  for i = 1:(N/2)
    PSI(:,i) = PSI(:,i) / norm(PSI(:,i));
  end
  PSI = PSI / h^(3/2);   %normalize PSI

  n = 0;
  for i = 1:(N/2) %calculate density of electron
    n = n + 2*PSI(:,i).^2;  
  end
  
  Vx = -(3/pi)^(1/3)*n.^(1/3);  %exchange potantial (LDA)
  Vh = cgs(L3, -4*pi*(n + ncomp), 1e-7, 400) - ncomppot; %Hartree potantial(solution of poisson eq.: L3 Vh = -4*pi*n)
  Vtot = Vx + Vh + Vext;  %total potantial
  
  T = 0;
  for i = 1:(N/2)  %calculate Kinetic energy
    T = T + 2*PSI(:,i)'*(-0.5*L3)*PSI(:,i) * h^3;  %Kinetic enerty(expactation value of Kinetic energy oprator)
  end
  Eext = sum(n.*Vext) * h^3;  %external energy
  Eh = 0.5 * sum(n.*Vh) * h^3;  %hartree energy
  Ex = sum(n.*Vx * (3/4)) * h^3;   %How come the 3/4????????????????
  Etot = T + Eext + Eh + Ex;
  more off;   %see the disp  in the loop, but why?
  E
%  disp(['Kinetic energy ' num2str(T,5) ]);
%  disp(['Exchange energy ' num2str(Ex,5) ]);
%  disp(['External energy ' num2str(Eext,5) ]);
%  disp(['Potential energy ' num2str(Eh,5) ]);
 disp(['Total energy' num2str(Etot,5) ]);
end
%scatter3(X(1:10:g3),Y(1:10:g3),Z(1:10:g3),n(1:10:g3)*1000);
scatter3(X,Y,Z,n*4);  //show electron density
{% endhighlight %}

用Davidson method 求解本征值和本征向量：

{% highlight matlab %}
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%
%  Usage: Get lowest eigenvalue and cooresponding Evetor by Davidson's method
%  H: discrete Hamiltonian
%  PSI, E： initial guess of eigenvectors and eigenvalue
%  N: number of eigen pair needed
%  iter: iteration number
%
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
function [PSI, E] = lowestNEigen(H, PSI, E, N, iter)
for i=1:iter  %"for loop": for faster convergent
  RR = H*PSI - PSI*diag(E);  %All the Residual vectors at once
  PSIe = [ PSI RR ];  %Subsbace
  HH = PSIe' * H * PSIe;  %For transform subspace to a space inwhich H is diagnolized
  SS = PSIe' * PSIe;  %For transform subspace to a space inwhich H is diagnolized
  HH = HH + HH';
  SS = SS + SS';  %Ensure they are Hermition matrix, so that the eigen value will return in order      
  [U, E] = eig(HH,SS);%For transform subspace to a space inwhich H is diagnolized
  E = diag(E);  %Diagnal Matix to vector
  PSIe = PSIe * U;
  %%SIe' * H * PSIe
  PSI = PSI(:,1:(N/2));
  E = E(1:(N/2)); %Pick lowest N/2 eigen vectors and values
end
  
{% endhighlight %}

## 结果 

Total energy: -10.793

电子密度分布图：![电子密度](\public\blogfigure\4electron.png)


## 接下来

误差较大，如何升级？

如何在 DFT 中考虑空间角动量，自旋角动量，由此研究其磁性？


## 参考资料：

[1h DFT code in matlab](https://www.youtube.com/watch?v=bW44gCulrvI)

[Laplace 算子的离散化方法及离散空间中的分离变量法](http://en.wikipedia.org/wiki/Kronecker_sum_of_discrete_Laplacians)

[快速求解矩阵最小（或最大）本征值本征向量的Davidson method](http://web.mit.edu/bolin/www/Project-Report-18.335J.pdf)

[Gaussian compensation charge](http://en.wikipedia.org/wiki/Poisson's_equation#Potential_of_a_Gaussian_charge_density)


<script type="text/javascript"
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>