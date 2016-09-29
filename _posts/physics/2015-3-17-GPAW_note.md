---
layout: post
title: GPAW note
tags: 
- quantum mechanics
---

* GPAW is a open sourse DFT software, written with python and c++. I hope I can firstly learn it well, and then do some meaningfull calculation with it. Finally, I hope I can contribute sth to this project. This article is a note for [this vedio](https://www.youtube.com/watch?v=4hgWXbyjpS4)


## GPAW 支持的不同基底

* Real-space grids
* Localized basis set
* Plane waves

### Real-space grids

* 波函数，电子密度等表示在grids 上
* 只有一个参数：grid 间距 h
* 计算精度可以通过减小h提高
* 导数利用finite differences 近似


### Localized basis set

* LCAO 提供完备的基底
* 。。

### Plane wave basis

* 周期性的函数可以用该基底展开


## Boundary conditions 可以是：

* Zero Boundary condition (有限系统)
* Periodic ..（块材）
* mixed
    * 在某一个维度上周期性（原子线）
    * 在两个维度上周期性（表面）


## GPAW features

* 探究基态性质
    * 总能，力，磁矩
    * 结构优化
    * electronic structure analysis
    * ...
* 浩如烟海的 XC-potentials(借助libxc)
    * LDAs, GGAs, meta-GGas, hybrids, DFT+U, vdW, RPA

## Time-Dependent DFT

* 实时演化
    * 吸收光谱
    * Non-linear emission
    * Ehrenfest dynamics
* 线性响应
    * Casida equation(finite systes)
    * Dyson equation(extended systems)
    * ...

参考：jcp 128(2008); prb 83,245122(2011)


## Many-body perturbation theory

* GW-approximation
    * 准粒子能谱
* Bethe-Salpeter equation

应用： PRB 86,045208(2012)

## Other features
* Transport(非线性格林函数)
* XAS 能谱
* 。。。


## 使用特性（Usage features）

* 简单而灵活的 Python 脚本接口（借助ASE）
* 模块化的设计使扩展新features 变得容易
* 高效的Parallelization（平行计算）

## GPAW xing'n

总的来说，与VASP不想上下

## Some history

* 曾用名： GridPAW(2004)


















