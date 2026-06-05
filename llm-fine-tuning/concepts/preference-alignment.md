---
title: Preference Alignment (偏好对齐)
created: 2026-06-03
updated: 2026-06-03
type: concept
tags: [alignment, rlhf, dpo, survey]
sources: [raw/papers/alignment-survey-2505.02666.md, raw/papers/rlhf-survey-2312.14925.md, raw/papers/rl-post-training-survey-2407.16216.md]
confidence: high
---

# Preference Alignment: LLM 偏好对齐

## 什么是 Alignment

**对齐 (Alignment)** 是指让 LLM 的行为与人类价值观、偏好和意图保持一致的过程。核心目标：模型不仅要"有能力"，还要"有用、诚实、无害"（HHH: Helpful, Honest, Harmless）。

## 对齐流水线

完整的 LLM 后训练对齐流程：

```
Pretraining → SFT (Instruction Tuning) → Preference Alignment
                                          ├── RLHF (PPO)
                                          ├── DPO (offline)
                                          └── RLVR (GRPO, verifiable rewards)
```

## 范式转移

来自综述 2505.02666 的观察：

| 旧范式 | 新范式 |
|--------|--------|
| **RL-based** (PPO + RM) | **RL-free** (DPO, KTO, SimPO 等) |
| 单任务对齐 | **多目标**对齐（安全+有用+事实性+...） |
| 单一反馈信号 | **混合信号**（人类偏好 + 可验证奖励 + AI 反馈） |

## 奖励设计视角（2505.02666）

Ji et al. 将对齐研究从**奖励设计**角度系统化：
1. **数学形式化**：奖励函数的定义和优化目标
2. **构建实践**：如何从数据中构建奖励信号（人类标注/规则/模型判断）
3. **与优化范式的交互**：奖励如何引导训练（RL 梯度 vs 分类损失）

## 主要方法对比

| 方法 | 类型 | 数据需求 | 复杂度 | 稳定性 | 代表性工作 |
|------|------|---------|--------|--------|-----------|
| PPO-RLHF | RL | 偏好对 + 奖励模型训练 | 高 | 中 | InstructGPT |
| DPO | Offline | 偏好对 | 低 | 高 | DPO (Rafailov+) |
| KTO | Offline | 单边偏好 | 低 | 高 | KTO (Ethayarajh+) |
| GRPO | RL | 可验证奖励 | 中 | 中 | DeepSeek-R1 |
| RLAIF | RL | AI 反馈 | 中 | 中 | Constitutional AI |

## 核心挑战

1. **奖励 hacking / overoptimization**: 策略学会利用奖励模型的漏洞（Goodhart's Law）
2. **偏好数据质量**: 人类标注噪声、不一致性、文化偏见
3. **分布偏移**: 训练分布 ≠ 部署分布
4. **多维度权衡**: 有用性 vs 安全性 vs 创造性的不可能三角
5. **评估困难**: 缺乏公认的对齐程度量化指标

## 新兴方向

- **Scalable Oversight**: 用 AI 辅助监督 AI
- **Constitutional AI**: 用规则而非人类偏好引导对齐
- **Multi-turn alignment**: 多轮对话场景的对齐
- **Personalized alignment**: 个性化偏好而非一刀切

## 相关概念

- [[rlhf-reinforcement-learning-human-feedback]] — RLHF 方法详解
- [[dpo-direct-preference-optimization]] — DPO 及其变体
- [[instruction-tuning]] — 对齐的前置 SFT 阶段
- [[grpo-group-relative-policy-optimization]] — RLVR 方法

## 待解决问题

- 对齐税（alignment tax）是否不可避免？
- 如何评估不同文化价值观下的对齐？
- 端到端对齐 vs 模块化对齐（哪个更优？）
