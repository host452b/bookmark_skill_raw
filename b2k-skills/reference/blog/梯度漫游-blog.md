---
name: "梯度漫游 | blog"
description: "在面向对象语言中，以类为中心的设计，一个类对应该矩阵中的一行。扩展类（增加新的行）很容易，但是扩展方法（增加新的列）很难，可以表示为："
url: "https://strint.github.io/221113-visitor_pattern.html"
category: "reference/blog"
content_type: "opinion-essay"
tags: ["reference", "blog"]
key_claims:
  - "在面向对象语言中，以类为中心的设计，一个类对应该矩阵中的一行。扩展类（增加新的行）很容易，但是扩展方法（增加新的列）很难，可以表示为："
  - "在以函数为中心的设计中，一个处理操作对应该矩阵中的一列。扩展方法(增加新的列)很容易，但是扩展类（增加新的行）很难，可以表示为："
taste_signals:
reuse_contexts:
  - situation: "讨论 访问者模式和应用于表达式求解的实现"
    how: "引用核心论点和案例"
quality_score:
  depth: 4
  originality: 3
  practicality: 3
  writing: 4
---

## Summary

在面向对象编程中，我们定义对类和处理对类的函数。一般情况下，要么类比较稳定，这样可以比较独立的扩展函数；要么函数比较稳定，可以通过类继承扩展类。但是一种麻烦的情况是，类和处理类的函数都要扩展。

## Key Insights
- 访问者模式和应用于表达式求解的实现
- 代码的扩展问题
- 以类为中心的扩展问题
- 以函数为中心的扩展问题
- 扩展问题总结
- 如何让扩展类和扩展方法都变得容易

## Memorable Quotes
> "在面向对象编程中，我们定义对类和处理对类的函数。一般情况下，要么类比较稳定，这样可以比较独立的扩展函数；要么函数比较稳定，可以通过类继承扩展类。但是一种麻烦的情况是，类和处理类的函数都要扩展。"
> "但是如果我们想新增一个基类方法，如生成表达式的汇编代码 ToAssembly，我们需要修改原来每个子类，给其增加 ToAssembly 方法。"

## Concrete Examples
- 可以看到，当前的 Evaluator 中，已经没有和 Constant 或者 BinaryPlus 这些具体 Expr 相关的耦合了。而 Evaluator 和具体 Expr 的耦合已经被拆分出来，比如 Evaluator 和 Constant 的组合，已经被拆分成了 EvalConstant。
- ExprProcesser 之前扩展方法就比较方便，现在可以让扩展 Expr 也变得方便，比如现在扩展一个 FunctionCall Expr 类型：
- 但是 BinaryPlus 和 FunctionCall 都比较特别，他们会嵌套 Expr。比如我们定义一个 FunctionCall Expression：

## When To Reference
- **讨论 访问者模式和应用于表达式求解的实现** → 引用核心论点和案例
