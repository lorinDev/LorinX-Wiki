---
title: Instruction Tuning (SFT)
created: 2026-06-03
updated: 2026-06-03
type: concept
tags: [instruction-tuning, sft, alignment, method, dataset]
sources: [raw/papers/instruction-tuning-survey-2308.10792.md]
confidence: high
---

# Instruction Tuning (SFT)

## 核心定义

**指令微调 (Instruction Tuning, IT)**，与**监督微调 (SFT)** 在实践中常混用，是指在 `(instruction, output)` 对上进一步训练预训练 LLM，弥合"下一词预测"目标与"遵循人类指令"目标之间的差距。

## 方法论全景（来自综述 2308.10792）

### 1. 数据集构建
- **人工标注**: 质量高但成本大（InstructGPT, LLaMA-2-chat）
- **模型生成**: 用强模型（GPT-4）生成指令-回答对（Self-Instruct, Alpaca）
- **混合策略**: 人工种子 + 模型扩展（WizardLM 的 Evol-Instruct）
- **多轮对话**: OpenAssistant, ShareGPT 等众包数据

### 2. 训练策略
- **全参数 SFT**: 更新所有参数（较小模型常用）
- **LoRA/QLoRA SFT**: 参数高效微调（大模型首选）
- **多任务混合**: 在多个数据集上联合训练以提升泛化

### 3. 影响因素
| 因素 | 发现 |
|------|------|
| 数据质量 | **质量 > 数量**；小规模高质量数据优于大规模噪声数据 |
| 数据多样性 | 任务类型多样性提升泛化能力 |
| 指令复杂度 | 复杂指令（多步推理）有助于提升推理能力 |
| 模型规模 | 存在阈值效应，需足够大的模型才能有效利用指令微调 |

### 4. 多模态/跨领域
- 视觉指令微调（LLaVA 等）
- 代码指令微调（Code Alpaca 等）
- 领域专用指令微调（医疗、法律）

## 陷阱与批评

1. **数据污染**: 训练集可能包含评测集数据
2. **过拟合**: 过度微调导致通用能力下降（catastrophic forgetting）
3. **幻觉放大**: SFT 可能强化而非修正模型的幻觉
4. **表面模式学习**: 模型可能学到风格/格式而非真正理解指令

## 与后续阶段的衔接

SFT 通常是 LLM 对齐流水线的**第一阶段**：
```
Pretraining → SFT (Instruction Tuning) → Preference Alignment (RLHF/DPO)
```

SFT 提供基础的指令遵循能力，后续 RLHF/DPO 再基于偏好进行精细对齐。

## 相关概念

- [[rlhf-reinforcement-learning-human-feedback]] — SFT 后的对齐阶段
- [[dpo-direct-preference-optimization]] — RL-free 对齐替代
- [[synthetic-data-fine-tuning]] — 合成 SFT 数据
- [[lora-low-rank-adaptation]] — 参数高效 SFT 方法
- [[qlora-quantized-lora]] — 量化 SFT
