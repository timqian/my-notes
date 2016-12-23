---
layout: post
title: linux tips
tags:
- linux
---

## `~/.profile`, `~/.bashrc`, `~/.bash_profile` 文件 ([ref1](http://linux.chinaunix.net/doc/system/2005-02-03/1084.shtml); [ref2](http://stackoverflow.com/questions/415403/whats-the-difference-between-bashrc-bash-profile-and-environment))

- `/bin/bash`: The bash executable
- `/etc/profile`: The systemwide initialization file, executed for login shells
- `~/.bash_profile`: The personal initialization file, executed for login shells (是交互式、login 方式进入 bash 运行的)
- `~/.bashrc`: The individual per-interactive-shell startup file (交互式 non-login 方式进入 bash 运行的)
- `~/.bash_logout`: The individual login shell cleanup file, executed when a login shell exits
- `~/.inputrc`: Individual readline initialization file

## linux 进程管理 command &、fg、bg、jobs、&、ctrl + z

- `command &`: 命令在后台执行
- `ctrl + z`: 将一个正在前台执行的命令放到后台，并且暂停
- `jobs`: 查看当前有多少在后台运行的命令
- `fg`: 将后台中的命令调至前台继续运行 `fg %jobnumber`
- `bg`: 将一个在后台暂停的命令，变成继续执行 `bg %jobnumber`

## Run mpi programs： `mpirun -np 40 gpaw-python`

## 关闭 ssh 连接程序继续运行的方法: `nohup 命令 &`
