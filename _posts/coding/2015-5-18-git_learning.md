---
layout: post
title: Git 学习
tags: git
---


##git for windows

下载与简介：[https://msysgit.github.io/](https://msysgit.github.io/)

## 本地项目初始化远程项目

    mkdir toggle_view_bee
    cd toggle_view_bee
    git init
    echo "# toggle_view_bee" >> README.md
    git add README.md
    git commit -m "first commit"
    git remote add origin https://git.coding.net/timqian/toggle_view_bee.git
    git push -u origin master

## 从github获取项目，更改，最后提交的最简过程

- git clone [https]：用github提供的https克隆项目代码到本地，之后就可以在本地更改了
- git add --all：将当前更改或者新增的文件加入到Git的索引中
- git commit：提交当前工作空间的修改内容
- git push：将本地commit的代码更新到远程版本库中

## 常用命令

- git pull：远程代码与本地不同时，更新本地代码
- git config user.name timqian --global: 配置git用户名（.email配置邮箱）

## 分支

- git branch [branch name]: 创建分支
- git checkout [branch name]: 转到某个分支
- git checkout -b [branch name]: 创建并转到该分支
- git merge [branch name]: 在master分支下运行该命令，将某个branch与master merge
- git status [file name]: 解决merge过程中的冲突