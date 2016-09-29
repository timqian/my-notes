---
layout: post
title: Stanford machine learning 笔记1
tags: 
- machine learning
---

* Introduction



## Superviced learning (监督学习)

'right answer' is given. 给出一些已知的输入（features）和输出，由此建立模型，预测未知输入的输出。

两种类型问题：
1. Regression problem(连续性问题，可能结果比较多)
2. Classification problem 


## Unsupervised Learning

从数据中发现规则。如：聚类（Google news）,组织计算机，social network analysis, 

例子：两个话筒区分说话人

    [W,s,v] = svd((repmat(sum(x.*x,1),size(x,1),1).*x)*x');
    
## 另：

* matlab/octave 帮助： `help` followed by a function name displays documentation for a built-in function，比如： `help plot`
* Machine learning 用途：手写识别，大数据分析（medical records， web click data），机器视觉，自然语言处理autonomous helicopter
    
