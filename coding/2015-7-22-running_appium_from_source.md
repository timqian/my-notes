---
layout: post
title: 从源码运行Appium
tags: 
- javascript
---

## 为了读懂 Appium 的源代码，我想，可能首先需要构建一下这个项目

装在tim目录下


## 步骤

[github上这篇md文件里](https://github.com/appium/appium/blob/master/docs/en/contributing-to-appium/appium-from-source.md)已经给出了步骤，我在这里记录一下它没写具体的

- 安装需要的部件
{%highlight bash%}
npm install -g mocha
npm install -g grunt-cli
{%endhighlight%}

- clone 这个项目

- `npm install` 一下

- 安装所需的软件(ant, maven;所谓安装，其实解压就可以了)并加到 `PATH`中，在`.profile`文件里加了这么几行：
{%highlight bash%}
export PATH=$PATH:/Users/junhuachen/Library/apache-maven-3.3.3/bin # maven
export PATH=$PATH:/Users/junhuachen/Library/apache-ant-1.9.6/bin # ant
export PATH=$PATH:/Users/junhuachen/Library/Android/sdk/platform-tools # android adb
export PATH=$PATH:/Users/junhuachen/Library/Android/sdk/tools # android tools
export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_45.jdk/Contents/Home # java
export ANDROID_HOME=/Users/junhuachen/Library/Android/sdk # android sdk
{%endhighlight%}
    
- 看依赖是否都装了：`node bin/appium-doctor.js --dev`

- install and build: `./reset.sh --dev`

## 遇到的问题

- `npm install` 时命令行像是一些gcc错误，不知道有没有影响
- 最后一步时，selendroid 装不上，不影响其他driver的使用，nexus5虚拟机可以使用

## 不明白的事情

- 从源码运行与`npm install` 区别在哪里
- 


