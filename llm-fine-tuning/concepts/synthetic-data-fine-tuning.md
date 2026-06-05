---
title: Synthetic Data for LLM Fine-Tuning
created: 2026-06-03
updated: 2026-06-03
type: concept
tags: [synthetic-data, data-curation, method, survey]
sources: [raw/papers/synthetic-data-survey-2503.14023.md]
confidence: high
---

# Synthetic Data for LLM Fine-Tuning

## 核心理念

用 LLM 生成**人工但任务相关**的训练样本，替代或补充真实标注数据。在标注稀缺/昂贵/敏感场景中具有关键价值。

## 三大生成策略

来自综述 2503.14023 的分类：

### 1. Prompt-based Generation（提示生成）
- 精心设计 prompt 直接生成训练样本
- 代表方法：Self-Instruct, Alpaca, Evol-Instruct
- 优点：简单直接；缺点：质量依赖 prompt 设计

### 2. Retrieval-Augmented Pipelines（检索增强）
- 检索真实样本作为锚点，引导 LLM 生成相似但不同的样本
- 提升生成数据的多样性和真实性

### 3. Iterative Self-Refinement（迭代自优化）
- 生成 → 自身评判 → 修正 → 再生成
- 代表：Constitutional AI, CoT-Self-Instruct
- 提升数据质量但增加计算开销

## 两类主流方法

| 方法 | 描述 | 代表工作 |
|------|------|---------|
| **Distillation** | 用更强模型（如 GPT-4）生成训练数据，蒸馏到小模型 | Alpaca, WizardLM, Orca |
| **Self-Improvement** | 模型自己生成数据，自己优化 | Self-Rewarding, SPIN, Self-Boosting |

## 应用领域

### Text 领域
- 低资源分类
- 问答系统
- 任何人工标注不足的场景

### Code 领域
- 代码指令微调（Code Alpaca 等）
- 代码翻译（语言迁移）
- Bug 修复
- **关键优势**：代码可通过执行反馈验证正确性（单元测试通过 = 正样本）

## 三大挑战

| 挑战 | 描述 |
|------|------|
| **事实性错误** | 生成文本包含幻觉或不准确信息 |
| **分布偏差** | 合成数据分布与真实数据不匹配，缺乏风格/领域真实感 |
| **偏见放大** | LLM 原有偏见在迭代生成中被放大 |

## 缓解策略

1. **过滤**: 后处理质量检查、规则过滤、人工审核
2. **加权**: 为合成样本分配置信度分数
3. **执行反馈**（代码特有）: 奖励通过单元测试的输出
4. **对比筛选**: 利用偏好模型剔除低质量样本

## 开放研究方向

1. **自动 Prompt 工程**: 优化生成 prompt 无需人工试错
2. **跨模态合成**: 扩展到图像-文本、视频、音频
3. **评估框架**: 更好的合成数据质量度量标准
4. **伦理与质量保障**: 在规模化中确保负责任使用

## 相关概念

- [[instruction-tuning]] — 合成数据主要用于 SFT 阶段
- [[dpo-direct-preference-optimization]] — 合成偏好数据用于 DPO
- [[data-curation]] — 数据筛选与清洗技术
