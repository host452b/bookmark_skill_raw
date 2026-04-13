---
url: "https://www.dreamsongs.com/RiseOfWorseIsBetter.html"
original_title: "The Rise of Worse is Better"
author: ["Richard P. Gabriel"]
date_processed: 2026-04-13T15:00:00Z
tags: ["software-design", "philosophy", "worse-is-better", "unix", "simplicity", "classic"]
---

# Worse is Better: 实现简单性胜过接口完美性的生存优势

> **原文链接:** https://www.dreamsongs.com/RiseOfWorseIsBetter.html

## 摘要

Richard Gabriel 提出软件设计的两种哲学：MIT 派追求接口完美（the right thing），New Jersey 派追求实现简单（worse is better）。通过 Unix/C vs Lisp/ITS 的对比，论证 worse-is-better 虽然看起来'更差'，但因为实现简单→易于移植→快速扩散→社区改进，反而有更强的生存和进化优势。这是软件工程史上最有影响力的设计哲学论述之一。

## 逻辑推导链
- MIT 派优先级：接口简单 > 实现简单。New Jersey 派优先级：实现简单 > 接口简单
- 实现简单 → 更容易移植到新平台
- 更容易移植 → 更快扩散（Unix 跑在所有机器上）
- 更快扩散 → 更大的用户基数 → 更大的改进压力
- 虽然初始版本'更差'，但在进化中胜出（survival characteristics）
- 因此：worse is better 不是妥协，是更优的生存策略

## 精彩表达
> "It is slightly better to be simple than correct."
> — *一句话概括了 worse-is-better 的核心取舍——直接挑战了'正确性不可妥协'的信条*
> "The MIT guy then muttered that sometimes it takes a tough man to make a tender chicken, but the New Jersey guy didn't understand (I'm not sure I do either)."
> — *用幽默结束了一场严肃的哲学辩论，承认这个问题没有干净的答案*
> "Completeness must be sacrificed whenever implementation simplicity is jeopardized."
> — *把 worse-is-better 的取舍推到极端——完整性是第一个被牺牲的*
> "It is important to remember that the initial virus has to be basically good. If so, the viral spread is assured as long as it is portable."
> — *将软件比作病毒——必须'基本够用'才能扩散，完美反而阻碍传播*

## 叙事手法
- 用'MIT 派 vs New Jersey 派'的对立结构组织全文，制造张力
- PC loser-ing 故事是经典的'两个人争论'叙事模板——把抽象的设计哲学具象化为一次对话
- 作者故意先把 worse-is-better 描述为'显然是坏哲学'，然后翻转——修辞手法上是先抑后扬
- 用 virus 比喻软件传播，把生物学概念引入技术讨论，降低理解门槛

## 具体案例与数据
- PC loser-ing 问题：MIT 方案是系统回退并恢复用户程序 PC（正确但复杂），Unix 方案是返回错误码让用户程序重试（简单但把复杂度推给用户）
- Unix/C 是 worse-is-better 的典型：实现简单→移植到所有平台→成为事实标准
- Common Lisp/CLOS 和 Scheme 是 MIT 派的典型：接口优雅但实现复杂→难以移植→市场份额萎缩
- 50% 的正确功能 + 病毒式传播 → 最终进化到 90%，而 the-right-thing 的 90% 正确功能可能永远无法发布

## 反对声音与局限性
- 作者自己承认他'故意漫画化了 worse-is-better 哲学'
- the-right-thing 在某些领域（安全关键系统、数学证明）可能确实更优
- worse-is-better 的成功可能是特定历史条件（硬件碎片化时代）的产物，不一定普适

## 容易忽略的细节
- 文章是 'Lisp: Good News, Bad News, How to Win Big' 的节选
- 作者 Richard Gabriel 来自 Lucid, Inc.（Lisp 公司），立场本应偏向 MIT 派，但他反过来论证了对手的优势
- loser 是 MIT AI Lab 对 user 的昵称
- ITS 是 MIT AI Lab 的操作系统名称
- 文章写于约 1991 年，但至今仍被广泛引用
