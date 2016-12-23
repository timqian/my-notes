---
layout: post
title: 笔记： webpack 基本用法
tags: 
- javascript
---

http://webpack.github.io/docs/tutorials/getting-started/

### install

	npm install webpack -g

### 从 entry.js 开始 boundle 成 bundle.js

	webpack ./entry.js bundle.js

### load css file 

条件：

1. Create a empty node_modules folder. 
2. Run npm install css-loader style-loader inside the floder.
3. 

	require("!style!css!./style.css"); //in entry.js

或者 better：

	require("./style.css"); //in entry.js
	webpack ./entry.js bundle.js --module-bind 'css=style!css'  //in commend line

### * 在 config file 中配置

	module.exports = {
	    entry: "./entry.js",
	    output: {
	        path: __dirname,
	        filename: "bundle.js"
	    },
	    module: {
	        loaders: [
	            { test: /\.css$/, loader: "style!css" }
	        ]
	    }
	};


	webpack  //命令

### * 方便查看变更：watch mode 以及 dev－server mode

	webpack --progress --colors --watch
	webpack-dev-server --progress --colors //(需要npm install webpack-dev-server -g)

dev-server 地址： http://localhost:8080/webpack-dev-server/bundle

### 完整代码：

https://github.com/timqian/learning_webpack