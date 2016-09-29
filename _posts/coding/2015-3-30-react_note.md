---
layout: post
title: React 笔记
tags: 
- javascript
---



## React

前端做两件事：资料呈现，交互作用

## component（组件）

Html 是基于components(image 标签， video标签)
复合式组件（form标签里面有其他组件）
自己想定义component怎么办？ Web Component（google polymer, mozilla x-tag）
问题：不兼容
解决：React component

## React component

    var hello = React.DOM.div(null, 'hello');
    
等价于：

    // JSX
    var hello = <div> hello</div>;

自己建component

    var Hello = React.createClass(    //描述component
        render: function(){
            return(
                <div className='hello'>
                    <span> Hello</span>
                </div>
            );
        }
    ); 


使用(令浏览器载入)：

    React.render(<Hello/>, document.body);

特点：

1. 是宣告性的：先宣告，再render
2. 可配置的（configurable）
3. 可交互的（在宣告components时可以添加onClick 事件的监听函数）
4. 安全的:
5. 可组合的（宣告components时可以应用其他的component）

## React帮助开发者做两件事：

render，interactive

### Reactive Rendering

* React 根据初始数据数据 render 整个component
* 数据更新时：通知React重新render整个component
* 不需要额外的资源绑定

### Virtual DOM Tree

浏览器中：js 快，DOM tree慢(ECMAScript承认两类对象，本地对象和宿主对象("Native Object"&"Host Object")。其中Native Objects的子类中有一类：内置对象("Built-in Object", ECMA 262 3rd Ed Section 4.3)。Native objects属于语言本身。Host objects是由环境提供，例如document对象，DOM节点之类的。
Native objects是松散的，而且动态的包含命名属性的（可能部分的实现中built-in object子类并非动态的，但这无关紧要）。)

用js打造virtual DOM tree
更新速度可达60fps

## React 的基本分层架构（它们是完全分开的）

* Data Input Interface
* Components Composition
* Rendering

## 使用分离的jsx

`sudo npm install -g react-tools`

`jsx --watch src/ build/` 自动将jsx格式的js转化为纯js并放倒build目录下

index.html 中把js地址指向`build/..`

## 在本地使用reacter-router

装browserify：`npm install -g browserify`

bundle 到一起：`browserify component.jsx.js > bundle.js`





