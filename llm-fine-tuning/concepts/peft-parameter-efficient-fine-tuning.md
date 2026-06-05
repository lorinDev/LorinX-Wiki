---
title: PEFT (Parameter-Efficient Fine-Tuning)
created: 2026-06-03
updated: 2026-06-03
type: concept
tags: [peft, lora, full-finetune, survey]
sources: [raw/papers/peft-survey-2403.14608.md]
confidence: high
---

# PEFT: Parameter-Efficient Fine-Tuning

## 核心定义

PEFT 指在微调预训练大模型时，仅调整**少量参数**以适配下游任务，从而大幅降低计算和存储开销。

## 主要方法分类

来自综述 2403.14608 的分类框架：

### 1. 低秩分解 (Low-Rank Decomposition)
- **LoRA**: 注入 $BA$ 低秩矩阵 → [[lora-low-rank-adaptation]]
- **DoRA**: 权重分解为幅度+方向，对方向做 LoRA
- **AdaLoRA**: 自适应分配每层的秩

### 2. Adapter 系列
- **Serial Adapter**: 在 Transformer 层间插入小网络
- **Parallel Adapter**: 与原始层并行的适配模块
- **AdapterFusion**: 组合多个 adapter 的知识

### 3. Prompt/Prefix Tuning
- **Prefix Tuning**: 学习可训练的连续前缀向量
- **P-Tuning v2**: 在每层添加可学习 prompt token
- **Prompt Tuning**: 仅在输入层添加软 prompt

### 4. 混合方法
- **QLoRA**: 量化 + LoRA → [[qlora-quantized-lora]]
- **IA3**: 仅学习缩放向量（最轻量）
- **UniPELT**: 统一框架组合多种 PEFT 方法

## 性能-效率权衡（来自综述）

| 方法 | 可训练参数 | 性能 | 推理延迟 |
|------|-----------|------|---------|
| Full Fine-tuning | 100% | ★★★★★ | 无额外 |
| LoRA | <1% | ★★★★☆ | 无（可合并） |
| Adapter | 1-3% | ★★★★ | 有 |
| Prompt Tuning | <0.1% | ★★★ | 无 |
| QLoRA | <1% | ★★★★☆ | 无（可合并） |

## 系统实现考量

综述 2403.14608 的特点：不仅覆盖算法，还分析**真实系统实现成本**：
- GPU 显存占用的精确建模
- 不同 PEFT 方法在不同硬件平台的适配
- 多租户场景下的 adapter 切换效率

## 发展趋势

1. **量化 + PEFT**: QLoRA 后的各种 2-bit/3-bit 微调
2. **自动化秩分配**: AdaLoRA 等根据层重要性动态分配秩
3. **MoE + PEFT**: 混合专家模型下的参数高效微调
4. **多模态 PEFT**: 扩展到视觉、语音等领域

## 相关概念

- [[lora-low-rank-adaptation]] — 最广泛使用的 PEFT 方法
- [[qlora-quantized-lora]] — 量化 PEFT
- [[full-finetuning]] — 全参数微调对比
- [[instruction-tuning]] — PEFT 在 SFT 中的应用

## 待解决问题

- 不同 PEFT 方法的最优选择缺乏理论指导
- 多种 PEFT 模块的组合和交互
- PEFT 对模型安全性的影响评估
