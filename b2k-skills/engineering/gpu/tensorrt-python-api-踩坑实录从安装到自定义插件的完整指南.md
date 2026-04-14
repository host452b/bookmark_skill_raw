---
name: "TensorRT Python API 踩坑实录：从安装到自定义插件的完整指南"
description: "TensorRT 官方文档对初学者不友好，缺乏可运行的代码示例"
url: "https://suborbit.net/posts/tensorrt-tutorial/"
category: "engineering/gpu"
content_type: "technical-article"
tags: ["tensorrt", "gpu", "inference", "quantization", "python-api"]
key_claims:
  - "TensorRT 官方文档对初学者不友好，缺乏可运行的代码示例"
  - "ONNX 导入是最简单的 Engine 构建方式，但 Network API 更灵活"
taste_signals:
  aesthetic: ["实用主义", "踩坑记录"]
  intellectual: ["从官方文档不足出发自建教程"]
  values: ["降低入门门槛", "代码示例驱动"]
reuse_contexts:
  - situation: "第一次使用 TensorRT Python API"
    how: "按此教程从安装到推理走一遍"
  - situation: "需要 TensorRT INT8 量化"
    how: "参考 calibrator 实现和校准流程"
quality_score:
  depth: 4
  originality: 3
  practicality: 5
  writing: 3
---

## Summary

作者因官方文档晦涩难懂，结合博客和源码整理了 TensorRT Python API 的实用教程。覆盖安装（Windows/Linux/pip）、Engine 构建（ONNX 导入 + Network API 手动搭建）、推理执行、INT8 量化校准、动态形状、自定义插件。是中文社区最完整的 TensorRT Python 入门资源之一。

## Key Insights
- TensorRT 官方文档太晦涩，缺示例
- 从安装开始：pip/zip/tar 三种方式
- 构建 Engine：ONNX 导入（简单）vs Network API（灵活）
- 推理：分配显存 → 拷贝输入 → 执行 → 拷贝输出
- 进阶：INT8 量化需要 calibrator + 校准数据集
- 高级：动态形状 + 自定义插件（IPluginV2）

## Concrete Examples
- trt.Builder → trt.NetworkDefinition → trt.OnnxParser 三步构建 Engine
- INT8Calibrator 继承 trt.IInt8EntropyCalibrator2，实现 get_batch/read/write_calibration_cache
- 自定义插件需实现 IPluginV2DynamicExt 的 7 个方法

## When To Reference
- **第一次使用 TensorRT Python API** → 按此教程从安装到推理走一遍
- **需要 TensorRT INT8 量化** → 参考 calibrator 实现和校准流程
