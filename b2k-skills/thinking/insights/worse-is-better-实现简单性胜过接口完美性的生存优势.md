---
name: "Worse is Better: 实现简单性胜过接口完美性的生存优势"
description: "实现简单性比接口完美性更重要——因为它决定了软件的可移植性和扩散速度"
url: "https://www.dreamsongs.com/RiseOfWorseIsBetter.html"
category: "thinking/mental-models"
content_type: "technical-essay"
tags: ["software-design", "philosophy", "worse-is-better", "unix", "simplicity", "classic"]
key_claims:
  - "实现简单性比接口完美性更重要——因为它决定了软件的可移植性和扩散速度"
  - "Worse-is-better 有更强的生存特征：先传播再改进，胜过先完美再发布"
  - "50% 的正确功能加上病毒式传播，最终会进化出比 the-right-thing 更好的结果"
  - "把复杂度推给用户（而非藏在实现里）是一种有效的设计策略"
taste_signals:
  aesthetic: ["对立结构", "先抑后扬", "具象化抽象概念"]
  intellectual: ["进化论思维", "反直觉论证", "实用主义"]
  values: ["实现简单优先", "传播优先于完美", "实用主义胜过理想主义"]
reuse_contexts:
  - situation: "讨论是否应该在发布前追求完美还是先发布 MVP"
    how: "引用 worse-is-better 的核心论证——50% 正确 + 病毒式传播胜过 90% 正确 + 无法发布"
  - situation: "技术选型中面临'优雅但复杂'vs'粗糙但简单'的选择"
    how: "引用 PC loser-ing 故事：Unix 选择实现简单，把复杂度推给用户，最终赢了"
  - situation: "解释为什么'更差'的技术反而赢得市场"
    how: "用 Unix/C vs Lisp 的历史案例，论证生存优势来自可移植性和社区而非技术优越性"
quality_score:
  depth: 5
  originality: 5
  practicality: 5
  writing: 5
---

## Summary

Richard Gabriel 提出软件设计的两种哲学：MIT 派追求接口完美（the right thing），New Jersey 派追求实现简单（worse is better）。通过 Unix/C vs Lisp/ITS 的对比，论证 worse-is-better 虽然看起来'更差'，但因为实现简单→易于移植→快速扩散→社区改进，反而有更强的生存和进化优势。这是软件工程史上最有影响力的设计哲学论述之一。

## Key Insights
- MIT 派优先级：接口简单 > 实现简单。New Jersey 派优先级：实现简单 > 接口简单
- 实现简单 → 更容易移植到新平台
- 更容易移植 → 更快扩散（Unix 跑在所有机器上）
- 更快扩散 → 更大的用户基数 → 更大的改进压力
- 虽然初始版本'更差'，但在进化中胜出（survival characteristics）
- 因此：worse is better 不是妥协，是更优的生存策略

## Memorable Quotes
> "It is slightly better to be simple than correct."
> "The MIT guy then muttered that sometimes it takes a tough man to make a tender chicken, but the New Jersey guy didn't understand (I'm not sure I do either)."
> "Completeness must be sacrificed whenever implementation simplicity is jeopardized."
> "It is important to remember that the initial virus has to be basically good. If so, the viral spread is assured as long as it is portable."

## Concrete Examples
- PC loser-ing 问题：MIT 方案是系统回退并恢复用户程序 PC（正确但复杂），Unix 方案是返回错误码让用户程序重试（简单但把复杂度推给用户）
- Unix/C 是 worse-is-better 的典型：实现简单→移植到所有平台→成为事实标准
- Common Lisp/CLOS 和 Scheme 是 MIT 派的典型：接口优雅但实现复杂→难以移植→市场份额萎缩
- 50% 的正确功能 + 病毒式传播 → 最终进化到 90%，而 the-right-thing 的 90% 正确功能可能永远无法发布

## When To Reference
- **讨论是否应该在发布前追求完美还是先发布 MVP** → 引用 worse-is-better 的核心论证——50% 正确 + 病毒式传播胜过 90% 正确 + 无法发布
- **技术选型中面临'优雅但复杂'vs'粗糙但简单'的选择** → 引用 PC loser-ing 故事：Unix 选择实现简单，把复杂度推给用户，最终赢了
- **解释为什么'更差'的技术反而赢得市场** → 用 Unix/C vs Lisp 的历史案例，论证生存优势来自可移植性和社区而非技术优越性
