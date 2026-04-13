---
name: "donnemartin/system-design-primer: Learn how to des"
description: "Generally, you should aim for **maximal throughput** with **acceptable latency**."
url: "https://github.com/donnemartin/system-design-primer"
category: "design/visual"
content_type: "tool-repo"
tags: ["design", "visual"]
key_claims:
  - "Generally, you should aim for **maximal throughput** with **acceptable latency**."
  - "- CDN costs could be significant depending on traffic, although this should be weighed with additional costs you would incur not using a CDN."
  - "Servers should be stateless: they should not contain any user-related data like sessions or profile pictures"
taste_signals:
reuse_contexts:
  - situation: "需要 donnemartin/system-design-prim 类工具"
    how: "直接使用或参考其实现方式"
quality_score:
  depth: 4
  originality: 3
  practicality: 4
  writing: 4
---

## Summary

*[English](/donnemartin/system-design-primer/blob/master/README.md) ∙ [日本語](/donnemartin/system-design-primer/blob/master/README-ja.md) ∙ [简体中文](/donnemartin/system-design-primer/blob/master/README-zh The application uses the cache as the main data store, reading and writing data to it, while the cache is responsible for reading and writing to the database:

## Memorable Quotes
> "**Help [translate](/donnemartin/system-design-primer/blob/master/TRANSLATIONS.md) this guide!**"
> "Another way to look at performance vs scalability:"

## Concrete Examples
- - Fetching complicated resources with nested hierarchies requires multiple round trips between the client and server to render single views, e.g. fetching content of a blog entry and the comments on t

## When To Reference
- **需要 donnemartin/system-design-prim 类工具** → 直接使用或参考其实现方式
