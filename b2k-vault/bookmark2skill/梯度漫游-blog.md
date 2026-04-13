---
url: "https://strint.github.io/221113-visitor_pattern.html"
original_title: "梯度漫游 | blog"
date_processed: 2026-04-14T00:00:00Z
tags: ["reference", "blog"]
---

# 梯度漫游 | blog

> **原文链接:** https://strint.github.io/221113-visitor_pattern.html

## 摘要

在面向对象编程中，我们定义对类和处理对类的函数。一般情况下，要么类比较稳定，这样可以比较独立的扩展函数；要么函数比较稳定，可以通过类继承扩展类。但是一种麻烦的情况是，类和处理类的函数都要扩展。

## 逻辑推导链
- 访问者模式和应用于表达式求解的实现
- 代码的扩展问题
- 以类为中心的扩展问题
- 以函数为中心的扩展问题
- 扩展问题总结
- 如何让扩展类和扩展方法都变得容易

## 精彩表达
> "在面向对象编程中，我们定义对类和处理对类的函数。一般情况下，要么类比较稳定，这样可以比较独立的扩展函数；要么函数比较稳定，可以通过类继承扩展类。但是一种麻烦的情况是，类和处理类的函数都要扩展。"
> — *简洁有力*
> "但是如果我们想新增一个基类方法，如生成表达式的汇编代码 ToAssembly，我们需要修改原来每个子类，给其增加 ToAssembly 方法。"
> — *简洁有力*

## 具体案例与数据
- 可以看到，当前的 Evaluator 中，已经没有和 Constant 或者 BinaryPlus 这些具体 Expr 相关的耦合了。而 Evaluator 和具体 Expr 的耦合已经被拆分出来，比如 Evaluator 和 Constant 的组合，已经被拆分成了 EvalConstant。
- ExprProcesser 之前扩展方法就比较方便，现在可以让扩展 Expr 也变得方便，比如现在扩展一个 FunctionCall Expr 类型：
- 但是 BinaryPlus 和 FunctionCall 都比较特别，他们会嵌套 Expr。比如我们定义一个 FunctionCall Expression：
