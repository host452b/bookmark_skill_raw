---
name: "一些关于 Cursor 的使用技巧 - 资源荟萃 - LINUX DO"
description: "The commit message should be structured as follows: <type>: <description>"
url: "https://linux.do/t/topic/172395"
category: "engineering/ai"
content_type: "technical-article"
tags: ["engineering", "ai"]
key_claims:
  - "The commit message should be structured as follows: <type>: <description>"
taste_signals:
reuse_contexts:
  - situation: "讨论 post by Theigrams on Aug 7, 2024"
    how: "引用核心论点和案例"
quality_score:
  depth: 4
  originality: 2
  practicality: 3
  writing: 4
---

## Summary

Title: 一些关于 Cursor 的使用技巧 - 资源荟萃 - LINUX DO

## Key Insights
- post by Theigrams on Aug 7, 2024
- [](https://linux.do/t/topic/172395#p-1362236-h-1)引言
- [](https://linux.do/t/topic/172395#p-1362236-h-2)上手
- [](https://linux.do/t/topic/172395#p-1362236-cursor-3)Cursor 为什么是神
- [](https://linux.do/t/topic/172395#p-1362236-cursor-4)Cursor 的一些隐藏技巧
- [](https://linux.do/t/topic/172395#p-1362236-h-1-5)1. 附加文档

## Memorable Quotes
> "最近论坛和 Twitter 上多了很多关于 Cursor 的讨论，其实我在 Cursor 刚出时就已经测试过，但当时的 Cursor 跟 Copilot 比并没有什么太大区别，所以很快就不再关注。"
> "最近一次 Cursor 重新出现在我的视线中，是在 AI Engineer World’s Fair 2024，OpenAI的工程师在展示时暴露了他的常用工具："

## Concrete Examples
- 在让 LLM 写代码时，一个常见的问题就是，LLM 给出的代码有时会是过时的写法，一个是因为老代码在训练数据中的占比更大，另一个是大模型的知识库有截止日期，例如GPT-4o的知识库截止日期是2023年10月，如果一个库在2024年出现了 API 上的变动，那它是不可能知道的。
- 例如在下面的例子中，我们@Pytoch，那么它就精准地将 nn.RNN 的文档页面添加到了检索文件中，回答的效果也非常好，有效避免了幻觉。

## When To Reference
- **讨论 post by Theigrams on Aug 7, 2024** → 引用核心论点和案例
