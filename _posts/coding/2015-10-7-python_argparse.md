---
layout: post
title: python argparse 模块用法小记
tags:
- python
---

argparse 模块用来从命令行读取文件后面带的参数

## positional arguments: 按位置读取参数 (必须输入)

```python
import argparse

# Create a parser¶
parser = argparse.ArgumentParser()

# Add arguments
parser.add_argument("x", type=int, help="the base")
parser.add_argument("y", type=int, help="the exponent")

# Parse arguments
args = parser.parse_args()
print args.x ** args.y
```

## optional arguments: 可选的参数

```python
import argparse
parser = argparse.ArgumentParser()

# Create optional args
parser.add_argument("-v", "--value", help="input value")
parser.add_argument("-f", "--flag", help="used as a flag", action='store_true')
args = parser.parse_args()
if args.flag:
    print "flag turned on"
if args.value:
    print "input value is: " + args.value
```

## 二者组合使用时，optional arguments 不影响positional arguments 的读取位置

```python
# test.py
import argparse
parser = argparse.ArgumentParser()
parser.add_argument("x", type=int, help="the base")
parser.add_argument("y", type=int, help="the exponent")
parser.add_argument("-d", "--doIt", help="used as a flag", action='store_true')
args = parser.parse_args()
if args.doIt:
    print "flag on"
    print args.x ** args.y
else:
    print "please turn on the flag"


# 执行
python test.py 2 -d 2

# output
4
```

## 参考
[https://docs.python.org/2.7/howto/argparse.html](https://docs.python.org/2.7/howto/argparse.html)
