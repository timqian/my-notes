---
layout: post
title: jSDoc 基本使用方式
tags:
- javascript
---

## Big picture

JSDoc 会从以 `/**` 开头的注释中提取信息, 生产文档。
例：
{%highlight js%}
/** hi there */
{%endhighlight%}

## 常用标签

### `@param`: 方法的参数

用法: @param {类型} 参数名 - 描述
例子
{%highlight js%}
/**
 * @param {string} somebody - Somebody's name
 */
{%endhighlight%}

### `@returns`: 方法的返回值

用法 : @returns {类型} 返回值描述

## @file : 文件描述

## @author：作者

## @constructor: 表明是构造器

## @todo: 描述将要做的事情
