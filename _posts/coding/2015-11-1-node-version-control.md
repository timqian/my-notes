---
layout: post
title:  node npm 版本控制
tags:
- javascript
---

## node:

使用 Tj 写的 [n](https://github.com/tj/n);

1. 安装 n: `npm install -g n`

2. 使用 n 安装不同版本的 node:

    - 最新版 stable node: `n stable`

    - 最新版 node: `n latest`

    - 指定 node 版本: `n 0.8.20`

3. 切换 node 版本: `n`

4. 删除等其他功能: 见[项目 git 地址](https://github.com/tj/n)

## 升级 npm 版本:

> sudo npm install -g npm

## 升级 npm 包

升级 global package:
> npm install -g [<pkg>...]

升级当前目录下 package:
> npm update [<pkg> ...]

## 参考:

[http://stackoverflow.com/questions/6237295/how-can-i-update-node-js-and-npm-to-the-next-versions](http://stackoverflow.com/questions/6237295/how-can-i-update-node-js-and-npm-to-the-next-versions)
