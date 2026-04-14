---
url: "https://apple1417.dev/posts/2024-06-08-python-import-hook-aliasing"
original_title: "Python Import Hooks and Module Aliasing"
date_processed: 2026-04-14T01:00:00Z
tags: ["python", "import-hook", "meta-path", "module-aliasing", "deep-dive"]
---

# Python Import Hooks 深度实战：用 meta_path hook 实现模块别名重定向

> **原文链接:** https://apple1417.dev/posts/2024-06-08-python-import-hook-aliasing

## 摘要

以 Borderlands 2 mod SDK 升级为背景，详解如何用 Python import hooks（sys.meta_path + Finder/Loader）实现模块别名。旧 SDK 的 mod 通过 Mods.ModMenu 导入，新 SDK 改为顶层 ModMenu，需要兼容层自动重定向。文章从 sys.modules 简单方案讲到完整的 MetaPathFinder+Loader 实现，是 Python import 机制最深入的实战教程之一。

## 逻辑推导链
- Borderlands mod SDK 升级：Mods.ModMenu → ModMenu（路径变化）
- 需要兼容层让旧 mod 的 import 自动重定向
- 方案 1: sys.modules 直接赋值（简单但有缺陷——子模块不工作）
- 方案 2: MetaPathFinder + Loader（完整但复杂）
- Finder 拦截 import 请求 → Loader 加载真实模块 → 注册别名到 sys.modules
- 结论：import hooks 强大但文档稀缺，需要读 CPython 源码理解

## 精彩表达
> "It turns out, most of the Python import system is written in Python itself, and is quite customizable."
> — *指出 Python import 系统的可定制性——大多数人不知道这一点*

## 叙事手法
- 从真实的游戏 mod 兼容性问题切入，把抽象的 import 机制具象化

## 具体案例与数据
- sys.modules['Mods.ModMenu'] = sys.modules['ModMenu'] — 最简单的别名方案
- MetaPathFinder.find_module() 拦截以 'Mods.' 开头的导入请求
- Loader.create_module() + exec_module() 完整实现模块加载

## 反对声音与局限性
- sys.modules 方案在子模块和 reload 场景下会失败

## 容易忽略的细节
- targeting Python 3.12.3
- 作者后来写了更好的入门版本（2025-12-14 更新）
- importlib.abc.MetaPathFinder 和 importlib.abc.Loader 是关键基类
