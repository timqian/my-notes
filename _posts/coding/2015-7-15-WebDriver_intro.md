---
layout: post
title: Selenium WebDriver 原理和使用
tags: 自动化测试
---

## 用途

1. 模拟用户使用浏览器（该功能不是这个项目组的工作，而是利用了各大浏览器厂商自己生产的测试工具）
2. 同一份脚本，可以测试多种浏览器（这是卖点）

## 用到的模块

1. [ChromeDriver](https://sites.google.com/a/chromium.org/chromedriver/)，FirefoxDriver，IEDriver 等Driver：它们由各大浏览器厂商生产，用来接受http请求，然后根据请求来操作浏览器。可以看做是server，但是接受http请求的规矩不一样
2. Selenium-server([node 版本](https://www.npmjs.com/package/selenium-standalone))：接受client的http请求，根据client想要操作的浏览器以及操作细节，发送http请求给相应的webdriver，让webdriver来打开浏览器并操作
3. client：根据用户写的测试脚本，转化为http请求发送给Selenium-server

其中http请求使用JSONWireProtocal

## 使用方法（以javascript为例）

- 装client：[wd](https://github.com/admc/wd)
- 装Selenium-server：[selenium-standalone](https://www.npmjs.com/package/selenium-standalone) （各浏览器的driver已经包括在其中）
- 写测试脚本：[wd 提供的一些 exapmle](https://github.com/admc/wd/tree/master/examples)
- 启动selenium-server后，运行脚本，就可以控制浏览器了！！！