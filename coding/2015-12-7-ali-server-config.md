---
layout: post
title: 阿里云服务器(centos)配置纪录
tags:
- linux
---

1. 创建用户：`useradd timqian`
2. 设置密码：`passwd timqian`
2. 将用户加入 sudo配置文件 ([参考](http://jingyan.baidu.com/article/2a1383284bb3e8074a134f2d.html))?
3. 加入 root 组：`usermod -G root timqian`?
3. 把笔记本的public key `scp` 到服务器，使得笔记本可以免密码登录，([参考博客](http://chenlb.iteye.com/blog/211809))
3. 安装node 和 npm: 运行 `curl -sL https://rpm.nodesource.com/setup_5.x | bash -` 之后它会告诉你怎么做. ([官方参考](https://github.com/nodesource/distributions))
4. 安装 `mongodb 3.2`([官方参考](https://docs.mongodb.org/master/tutorial/install-mongodb-on-red-hat/))

    1. 设置yum 源：/etc/yum.repos.d/mongodb-org-3.2.repo
    2. 安装：`sudo yum install -y mongodb-org`
    3. 遇到[这个问题](http://stackoverflow.com/questions/27375137/failed-global-initialization-badvalue-invalid-or-no-user-locale-set-please-ens),最后在 用户家目录的 `.bash_profile` 中添加了这样一行`export LC_ALL=C`  ?
