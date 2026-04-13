---
name: "(145条消息) 用Python绑定调用C/C++/Rust库_python调用rust_JarodYv的博客-CSDN博客"
description: "在[《让你的Python程序像C语言一样快》](https://jarod.blog.csdn.net/article/details/128221350)我们学习了如何利用[Python API]("
url: "https://jarod.blog.csdn.net/article/details/128384888"
category: "engineering/python"
content_type: "technical-article"
tags: ["engineering", "python"]
key_claims:
  - "在[《让你的Python程序像C语言一样快》](https://jarod.blog.csdn.net/article/details/128221350)我们学习了如何利用[Python API]("
taste_signals:
reuse_contexts:
  - situation: "讨论 用Python绑定调用C/C++/Rust库"
    how: "引用核心论点和案例"
quality_score:
  depth: 4
  originality: 1
  practicality: 3
  writing: 4
---

## Summary

在[《让你的Python程序像C语言一样快》](https://jarod.blog.csdn.net/article/details/128221350)我们学习了如何利用[Python API](https://docs.python.org/3/c-api/index.html)来用C语言编写Python模块，通过将核心功能或性能敏感运算用C语言实现，Python程序可以运行地像C语言一样快 然而，尽管Cython像Python但并不完全是Python，因此，当你使用Cython时，会有一个轻微的学习曲线。

## Key Insights
- 用Python绑定调用C/C++/Rust库
- Python绑定概述
- ctypes
- Cython
- 总结

## Memorable Quotes
> "ctypes最大的优势是它是标准库的一部分，自Python 2.5开始ctypes随Python一起发行，不需要额外安装。使用时直接`import`进来即可。"
> "当共享库与Python脚本位于同一目录中时，这将起作用，但当您尝试加载来自Python绑定以外的包的库时，请小心。"

## Concrete Examples
- 如果你学习过[《让你的Python程序像C语言一样快》](https://jarod.blog.csdn.net/article/details/128221350)或者你曾经用C语言写过Python模块，那么你应该体会到，Python调用C需要做的主要工作就是**数据的封装和转换**。这是因为Python和C的数据存储方式不同——C语言的数据存储更加紧凑。例如，C语言中的`uint8_t`在内存
- 例如，在Python中，当执行`x = 3`时，会创建一个对象并且由Python的垃圾收集器来管理，对应C语言的代码为：
- ctypes提供多种方法[加载共享库](https://docs.python.org/3.5/library/ctypes.html#loading-shared-libraries)，其中有些是平台特有的。例如，我们可以通过传入所需共享库的完整路径来直接创建一个ctypes.CDLL对象。

## When To Reference
- **讨论 用Python绑定调用C/C++/Rust库** → 引用核心论点和案例
