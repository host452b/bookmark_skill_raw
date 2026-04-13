---
name: "cursor 的Index 步骤 Codebase Indexing | Cursor Docs"
description: "Title: Semantic & Agentic Search | Cursor Docs 这有助于上下文管理。在许多文件中搜索会生成大量上下文。子代理通过总结结果，而不是直接倾倒原始文件内容，来让"
url: "https://cursor.com/cn/docs/context/codebase-indexing"
category: "engineering/ai"
content_type: "technical-article"
tags: ["engineering", "ai"]
key_claims:
  - "Title: Semantic & Agentic Search | Cursor Docs 这有助于上下文管理。在许多文件中搜索会生成大量上下文。子代理通过总结结果，而不是直接倾倒原始文件内容，来让"
taste_signals:
reuse_contexts:
  - situation: "讨论 语义与 Agent 搜索"
    how: "引用核心论点和案例"
quality_score:
  depth: 3
  originality: 1
  practicality: 3
  writing: 4
---

## Summary

Title: Semantic & Agentic Search | Cursor Docs 这有助于上下文管理。在许多文件中搜索会生成大量上下文。子代理通过总结结果，而不是直接倾倒原始文件内容，来让主对话保持聚焦。

## Key Insights
- 语义与 Agent 搜索
- [Instant Grep](https://cursor.com/cn/docs/context/codebase-indexing#instant-grep)
- [语义搜索](https://cursor.com/cn/docs/context/codebase-indexing#)
- [索引的工作原理](https://cursor.com/cn/docs/context/codebase-indexing#-1)
- [配置](https://cursor.com/cn/docs/context/codebase-indexing#-2)
- [隐私和安全](https://cursor.com/cn/docs/context/codebase-indexing#-3)

## Memorable Quotes
> "查找代码最快的方法是精确匹配：函数名、变量名、错误字符串或正则表达式模式。当你引用特定符号时，Agent 会自动使用 grep。"
> "当你打开一个工作区时，会自动开始建立索引。索引完成 80% 后即可使用语义搜索。索引通过每 5 分钟自动同步一次保持最新状态，并且只处理已更改的文件。"

## Concrete Examples
- 当你不知道确切名称时，语义搜索会按含义查找代码。比如问 “where do we handle authentication?”，Agent 仍然可以定位到 `middleware/session.ts`，即使文件里从未出现过单词 “authentication”。

## When To Reference
- **讨论 语义与 Agent 搜索** → 引用核心论点和案例
