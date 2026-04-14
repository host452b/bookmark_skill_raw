---
url: "https://suborbit.net/posts/tensorrt-tutorial/"
original_title: "TensorRT踩坑教程 - 银河渡舟"
date_processed: 2026-04-14T01:00:00Z
tags: ["tensorrt", "gpu", "inference", "quantization", "python-api"]
---

# TensorRT Python API 踩坑实录：从安装到自定义插件的完整指南

> **原文链接:** https://suborbit.net/posts/tensorrt-tutorial/

## 摘要

作者因官方文档晦涩难懂，结合博客和源码整理了 TensorRT Python API 的实用教程。覆盖安装（Windows/Linux/pip）、Engine 构建（ONNX 导入 + Network API 手动搭建）、推理执行、INT8 量化校准、动态形状、自定义插件。是中文社区最完整的 TensorRT Python 入门资源之一。

## 逻辑推导链
- TensorRT 官方文档太晦涩，缺示例
- 从安装开始：pip/zip/tar 三种方式
- 构建 Engine：ONNX 导入（简单）vs Network API（灵活）
- 推理：分配显存 → 拷贝输入 → 执行 → 拷贝输出
- 进阶：INT8 量化需要 calibrator + 校准数据集
- 高级：动态形状 + 自定义插件（IPluginV2）

## 具体案例与数据
- trt.Builder → trt.NetworkDefinition → trt.OnnxParser 三步构建 Engine
- INT8Calibrator 继承 trt.IInt8EntropyCalibrator2，实现 get_batch/read/write_calibration_cache
- 自定义插件需实现 IPluginV2DynamicExt 的 7 个方法

## 容易忽略的细节
- TensorRT 8.6.1 开始支持 pip install tensorrt（仅 Linux）
- Windows 需要手动配环境变量
- context.execute_async_v3 是新版推理接口
