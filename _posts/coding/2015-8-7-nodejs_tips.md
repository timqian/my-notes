---
layout: post
title: Nodejs小贴士
tags: javascript
---

* 记录Node.js使用过程中的一些小细节

- 尽量使用**package.json**文件来管理模块
    - `npm init` 初始化package.json
    - `npm install --save express@4.10.2` 可以将安装的模块显示在package.json 中。
    - `npm install --save-dev express` 安装在devDependencis 中
- node 不适合：处理大量数据或长时间运行计算
- node 旨在：在网络中推送数据并瞬间完成
- `app.set('port', process.env.PORT || 3000);` means: whatever is in the environment variable PORT, or 3000 if there's nothing there.
    - What is environment variable: Environment variables are a set of dynamic named values that can affect the way running processes will behave on a computer[(wikipedia)](https://en.wikipedia.org/wiki/Environment_variable).
