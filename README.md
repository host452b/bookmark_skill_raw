# bookmark_skill_raw

[bookmark2skill](https://github.com/host452b/bookmark2skill) 蒸馏产出——从 Chrome 收藏夹蒸馏为结构化知识。

## 统计

| 指标 | 数量 |
|---|---|
| Skills 总数 | 140 |
| Vault 笔记 | 29 |
| 分类 | 22 |
| 来源 | Chrome 全 Profile 收藏夹 |

## 分类分布

| 分类 | 数量 | 说明 |
|---|---|---|
| `design/game` | 47 | 游戏开发素材、独立游戏案例、Godot 引擎、地图生成器、BGM 资源 |
| `engineering/ai` | 39 | LLM agent、Claude Code skills、AI 编程、prompt 工程、语音合成 |
| `design/visual` | 10 | UI 设计灵感、封面图生成、图标集、配色方案、排版参考 |
| `thinking/insights` | 7 | 职业成长、学习方法论、YC 创业经验、被低估的技术技能 |
| `engineering/gpu` | 5 | CUDA 编程、eBPF GPU 监控、NCCL 通信 |
| `product/indie` | 4 | 独立开发者博客、阅读工具、个人项目经验 |
| `engineering/python` | 3 | Python hook 机制、环境变量拦截、工作流简化 |
| `reference/blog` | 3 | 技术博客索引 |
| `uncategorized` | 3 | 待分类 |
| `thinking/mental-models` | 2 | 模仿理论、居家办公经验 |
| `product/strategy` | 2 | 注意力争夺战、产品策略 |
| `engineering/docs` | 2 | Diataxis 文档方法论、Docling 文档处理 |
| `engineering/devops` | 2 | 免费域名、YAML 简历生成 |
| `engineering/apple` | 2 | Core ML、Swift Transformers |
| `culture/art` | 2 | 明朝艺术史、源氏香数学 |
| `engineering/systems` | 1 | C++ 实践 |
| `engineering/search` | 1 | Qdrant 向量搜索 |
| `engineering/frontend` | 1 | CSS 技巧 |
| `engineering/deep-learning` | 1 | 模型量化 |
| `design/ui-ux` | 1 | Iconify 图标集 |
| `culture/research` | 1 | MISRA-C 研究 |
| `learning/platform` | 1 | Chrome Experiments |

## Skill 文件格式

每个 `.md` 文件包含 YAML frontmatter + Markdown body：

```yaml
---
name: "蒸馏后的标题（核心主张）"
description: "一句话描述"
url: "原始 URL"
category: "area/sub"
tags: ["tag1", "tag2"]
key_claims:
  - "可以被同意或反对的核心论断"
taste_signals:
  aesthetic: ["审美偏好"]
  intellectual: ["思维模式"]
  values: ["价值取向"]
reuse_contexts:
  - situation: "什么场景下引用"
    how: "具体怎么用"
quality_score:
  depth: 1-5
  originality: 1-5
  practicality: 1-5
  writing: 1-5
---

## Summary
2-4 句摘要

## Key Insights / Memorable Quotes / Concrete Examples / When To Reference
（按内容类型选择性呈现）
```

## 目录结构

```
b2k-skills/                  ← AI agent 可检索的 skill 文件
├── culture/art/             ← 艺术与文化
├── design/game/             ← 游戏开发（最大分类）
├── design/visual/           ← 视觉设计
├── design/ui-ux/            ← UI/UX
├── engineering/ai/          ← AI/LLM（第二大分类）
├── engineering/apple/       ← Apple 平台
├── engineering/deep-learning/
├── engineering/devops/
├── engineering/docs/        ← 技术文档方法论
├── engineering/frontend/
├── engineering/gpu/         ← GPU/CUDA
├── engineering/python/
├── engineering/search/      ← 向量搜索
├── engineering/systems/     ← 系统编程
├── learning/platform/
├── product/indie/           ← 独立开发
├── product/strategy/
├── reference/blog/
├── thinking/insights/       ← 深度思考
├── thinking/mental-models/
└── uncategorized/

b2k-vault/                   ← Obsidian 人类阅读笔记
└── bookmark2skill/
    └── *.md
```

## 工具

使用 [bookmark2skill (b2k)](https://github.com/host452b/bookmark2skill) CLI 生成：

```bash
pip install bookmark2skill
b2k list --source chrome              # 解析收藏夹
b2k fetch <url>                       # 抓取页面
b2k write-skill --data distilled.json # 生成 skill
b2k search "关键词"                    # 搜索 skill
```

## License

MIT
