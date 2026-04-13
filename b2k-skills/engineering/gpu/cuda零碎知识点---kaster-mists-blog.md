---
name: "CUDA零碎知识点 - Kaster Mist's Blog"
description: "在学习CUDA过程中会遇到很多问题，而这些问题过于零碎，无法进行系统化的分类，所以这篇文章主要记录平时遇到的CUDA使用的知识点。"
url: "https://kastermist.com/posts/cuda/cuda%E9%9B%B6%E7%A2%8E%E7%9F%A5%E8%AF%86%E7%82%B9/"
category: "engineering/gpu"
content_type: "technical-article"
tags: ["engineering", "gpu"]
key_claims:
  - "在学习CUDA过程中会遇到很多问题，而这些问题过于零碎，无法进行系统化的分类，所以这篇文章主要记录平时遇到的CUDA使用的知识点。"
taste_signals:
reuse_contexts:
  - situation: "讨论 thread hierarchy[](#thread-hierarchy)"
    how: "引用核心论点和案例"
quality_score:
  depth: 4
  originality: 1
  practicality: 3
  writing: 4
---

## Summary

在学习CUDA过程中会遇到很多问题，而这些问题过于零碎，无法进行系统化的分类，所以这篇文章主要记录平时遇到的CUDA使用的知识点。

## Key Insights
- thread hierarchy[](#thread-hierarchy)
- GPU硬件中的对应关系[](#gpu%E7%A1%AC%E4%BB%B6%E4%B8%AD%E7%9A%84%E5%AF%B9%E5%BA%94%E5%85%B3%E7%B3%BB)
- c++中与GPU有关的操作[](#c%E4%B8%AD%E4%B8%8Egpu%E6%9C%89%E5%85%B3%E7%9A%84%E6%93%8D%E4%BD%9C)
- include &lt;thrust/device_vector.h&gt;
- include &lt;thrust/host_vector.h&gt;
- include &lt;iostream&gt;

## Memorable Quotes
> "一个thread block的thread都在同一个multiprocessor core上，共享一个有限的内存资源。目前的GPU上一个thread block最多可以有1024个threads."
> "- **一个warp内的线程**：在硬件支持下，warp内的32个线程会一起调度，并且在同一个指令上执行不同的数据。尽管硬件层面可能会将这些线程分批处理，但从逻辑上它们是同时执行的。"

## Concrete Examples
- 此外，我们也可以直接对device_vector进行赋值，比如`thrust::device_vector&lt;int&gt; d_vec = {1, 1, 1};`，但是在host端我们仍然无法直接访问device_vector的值。

## When To Reference
- **讨论 thread hierarchy[](#thread-hierarchy)** → 引用核心论点和案例
