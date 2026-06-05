---
title: QLoRA (Quantized LoRA)
created: 2026-06-03
updated: 2026-06-03
type: concept
tags: [lora, quantization, peft, method]
sources: [raw/papers/qlora-2305.14314.md]
confidence: high
---

# QLoRA: Quantized Low-Rank Adaptation

## 核心思想

QLoRA 将 **4-bit 量化**与 **LoRA** 结合，通过冻结量化后的预训练模型，反向传播梯度到 LoRA 适配器层，实现在**单张 48GB 消费级 GPU 上微调 65B 参数模型**。

## 三大创新

### 1. 4-bit NormalFloat (NF4)
- 针对**正态分布权重**信息论最优的 4-bit 数据类型
- 利用预训练权重近似正态分布的特性
- 比标准 4-bit 整数/浮点格式量化精度更高

### 2. Double Quantization（双重量化）
- 对量化常数（scaling factors）**自身再量化**
- 进一步压缩平均内存占用

### 3. Paged Optimizers（分页优化器）
- 类似操作系统分页机制，管理 GPU 显存尖峰
- 防止长序列训练时的 OOM（内存溢出）

## Guanaco 模型家族

QLoRA 微调的最佳模型家族，关键结果：
- **Vicuna 基准**: 超越所有先前开源模型
- **vs ChatGPT**: 达到 ChatGPT 性能的 **99.3%**
- **训练成本**: 仅需单 GPU **24 小时**
- **数据效率**: 小规模高质量指令数据集即可达到 SOTA

## 实验规模

- 微调 **>1,000** 个模型
- 覆盖 LLaMA、T5 架构
- 模型规模：33B ~ 65B
- 8 个指令微调数据集

## 关键发现

### 评估洞见
1. **GPT-4 评估可作为人工评估的廉价替代** — GPT-4 判断与人类评估高度相关
2. **现有 chatbot 基准不可信** — 无法准确反映模型实际性能
3. **数据质量 > 数据数量** — 小规模高质量数据优于大规模低质量数据

### Guanaco 弱点（柠檬挑选分析）
- 在某些推理任务上仍弱于 ChatGPT
- 需要针对性改进的训练数据

## 与 LoRA 的关系

QLoRA = 4-bit 量化基座 + LoRA 适配器。核心训练逻辑与 LoRA 一致，只是在量化精度下工作。详见 [[lora-low-rank-adaptation]]。

## 实践影响

QLoRA 使得个人研究者和小团队也能微调大模型，降低了 LLM 微调的门槛。代码和 CUDA kernel 均已开源，集成在 Hugging Face PEFT 库中。

## 相关概念

- [[lora-low-rank-adaptation]] — LoRA 方法
- [[peft-parameter-efficient-fine-tuning]] — PEFT 方法总览
- [[quantization-techniques]] — 量化技术
