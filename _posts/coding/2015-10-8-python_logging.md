---
layout: post
title: python logging 模块用法小记
tags:
- python
---

## 使用logging将log写入文件：

```python
import logging

# logging level: debug < info < warning
logging.basicConfig(filename='example.log', format='%(levelname)s:%(message)s', level=logging.DEBUG)
logging.debug('This message should go to the log file')
logging.info('So should this')
logging.warning('And this, too')
```

- 当basicConfig 中没有指定filename时，直接logging打印到console
- 多个模块中logging basicConfig 写在调用其他函数之前

## 参考
[https://docs.python.org/2/howto/logging.html#logging-basic-tutorial](https://docs.python.org/2/howto/logging.html#logging-basic-tutorial)
