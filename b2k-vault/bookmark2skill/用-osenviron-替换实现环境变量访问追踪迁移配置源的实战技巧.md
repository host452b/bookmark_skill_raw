---
url: "https://noamlerner.com/posts/python_environment_hook/"
original_title: "Adding hooks when accessing environment variables in Python"
date_processed: 2026-04-14T01:00:00Z
tags: ["python", "import-hook", "environment-variables", "migration", "observability"]
---

# 用 os.environ 替换实现环境变量访问追踪——迁移配置源的实战技巧

> **原文链接:** https://noamlerner.com/posts/python_environment_hook/

## 摘要

作者在将 Python 服务从环境变量配置迁移到 JSON 文件时，发现代码中散落着大量直接访问 os.environ 的调用点。通过重写 os.environ 为自定义的 EnvAccessLoggingDict，在运行时自动记录哪些环境变量被访问、从哪里访问，从而找到所有需要迁移的代码位置。这是一种优雅的'观察而非搜索'策略。

## 逻辑推导链
- 服务配置从环境变量迁移到 JSON 文件
- 直接删环境变量 → 服务崩溃（散落的 os.environ 调用太多）
- grep 搜索不可靠（跨多目录，间接访问）
- 解法：重写 os.environ 为 logging proxy → 运行时自动发现所有访问点
- 观察比搜索更可靠

## 叙事手法
- 从失败的迁移尝试切入，逐步引出 hook 方案——问题驱动叙事

## 具体案例与数据
- EnvAccessLoggingDict 继承 os._Environ，重写 __getitem__ 记录访问日志
- 在 sitecustomize.py 中替换 os.environ = EnvAccessLoggingDict(os.environ)

## 反对声音与局限性
- 只适用于运行时能触达的代码路径，静态分析可能覆盖更全

## 容易忽略的细节
- 使用了 os._Environ 这个内部类
- sitecustomize.py 是 Python 启动时自动执行的钩子
