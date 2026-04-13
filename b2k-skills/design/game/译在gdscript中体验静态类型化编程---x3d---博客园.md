---
name: "[译]在GDScript中体验静态类型化编程 - x3d - 博客园"
description: "这项新特性的使用场景和使用方式，完全根据你自己的习惯和需要来决定：比如只在一些“敏感的”GDScript脚本中使用、或者全部使用、或者不用！ 静态类型化的写法多多一点代码，但是如上所述能因此受益。这里"
url: "https://www.cnblogs.com/x3d/p/godot-gdscript-static-typing.html"
category: "design/game"
content_type: "technical-article"
tags: ["design", "game"]
key_claims:
  - "这项新特性的使用场景和使用方式，完全根据你自己的习惯和需要来决定：比如只在一些“敏感的”GDScript脚本中使用、或者全部使用、或者不用！ 静态类型化的写法多多一点代码，但是如上所述能因此受益。这里"
taste_signals:
reuse_contexts:
  - situation: "游戏开发需要灵感或素材参考"
    how: "参考 [译]在GDScript中体验静态类型化编程 - x3d - 的风格和机制"
quality_score:
  depth: 4
  originality: 1
  practicality: 3
  writing: 4
---

## Summary

这项新特性的使用场景和使用方式，完全根据你自己的习惯和需要来决定：比如只在一些“敏感的”GDScript脚本中使用、或者全部使用、或者不用！ 静态类型化的写法多多一点代码，但是如上所述能因此受益。这里给出两种空骨架代码。

## Key Insights
- 在GDScript中体验静态类型化编程
- 简介
- 用法
- 自定义变量类型
- 变量类型转换
- 安全行

## Memorable Quotes
> "这项新特性的使用场景和使用方式，完全根据你自己的习惯和需要来决定：比如只在一些“敏感的”GDScript脚本中使用、或者全部使用、或者不用！"
> "这种因为是动态类型的代码写法，Godot无法得知传给该函数的节点或值的类型。如果代码显式指定类型，你就会得到编辑器对该节点全部公共方法与属性的提示："

## Concrete Examples
- 这项新特性的使用场景和使用方式，完全根据你自己的习惯和需要来决定：比如只在一些“敏感的”GDScript脚本中使用、或者全部使用、或者不用！
- 另一种是在创建自定义类文件时，通过`class_name`关键字进行声明。 比如上面的例子，那个 Rifle.gd 文件里的写法像这样：
- 可以看到，针对引擎的这些虚拟方法，也可以使用类型声明。同样，节点的信号回调函数，跟所有方法一样，也能使用类型声明。比如一个`body_entered`信号的动态类型写法：

## When To Reference
- **游戏开发需要灵感或素材参考** → 参考 [译]在GDScript中体验静态类型化编程 - x3d - 的风格和机制
