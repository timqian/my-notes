---
layout: post
title: Gitpage小贴士
tags: 
- 杂七杂八
---

* 在使用Github page 时遇到的一些问题及解决

### 代码高亮和公式输入的矛盾  

似乎只有kramdown(markdown process) 支持latex公式识别(用“$$”包围latex公式，行内和行间公式用空行区分)。
但是gitpage不支持kramdown自带(?)的用于代码高亮的coderay（见[这里](https://github.com/jekyll/jekyll/issues/2709)）。
因此我现在输入公式使用的方式是利用liquid自带的方式：{% raw %} {% highlight %}{% endraw %} 。

### 代码加行数：

linenos 

### 使用{% raw %} {% raw %} {% endraw %} 来停用liquid
 