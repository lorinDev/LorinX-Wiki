---
title: RLHF (Reinforcement Learning from Human Feedback)
created: 2026-06-03
updated: 2026-06-03
type: concept
tags: [rlhf, alignment, method]
sources: [raw/papers/rlhf-survey-2312.14925.md, raw/papers/rl-post-training-survey-2407.16216.md]
confidence: high
---

# RLHF: Reinforcement Learning from Human Feedback

## 核心定义

RLHF 是一种用**人类反馈替代工程化奖励函数**的强化学习方法。它建立在前身 PbRL (Preference-based RL) 基础上，处于 AI 与 HCI 交叉领域。

**标准 RLHF 流水线（LLM 场景）：**
1. **SFT (Supervised Fine-Tuning)**: 在高质量指令-回答对上微调
2. **Reward Model (RM) 训练**: 收集人类偏好（chosen vs rejected），训练打分模型
3. **PPO 优化**: 用奖励模型引导 RL 策略更新，加 KL 散度惩罚防止偏离太远

## 发展历程

RLHF 最早起源于**控制与机器人**领域，而后在 LLM 对齐中取得突破性成功。

| 里程碑 | 时间 | 意义 |
|--------|------|------|
| PbRL 早期工作 | ~2017 | 奠定偏好学习基础 |
| InstructGPT (OpenAI) | 2022 | RLHF 大规模应用于 LLM |
| ChatGPT | 2022.11 | RLHF 对齐的商业化成功 |
| RLHF 综述 | 2023.12 | 系统化整理领域 |
| RL Post-Training 综述 | 2024.07 | 统一框架含 RLVR |

## 统一策略梯度框架 (2407.16216)

Wang et al. (2024) 将预训练、SFT、RLHF、RLVR 统一到一个策略梯度框架内，分解为：
- **Prompt 采样** 策略
- **Response 采样** 策略
- **梯度系数** 定义

这使得能直接在统一视角下比较 PPO、GRPO、DPO 等方法。

## RL vs RL-free 范式转移

> 见 [[preference-alignment#paradigm-shift]]

关键趋势（来自 2505.02666）：
- **从 RL-based 到 RL-free**: DPO 及其变体免除了显式 RL 训练
- **从单任务到多目标**: 安全+有用+诚实等多维度对齐
- **RLVR 的崛起**: 在数学、代码等可验证场景，GRPO 等 RL 方法重获优势

## RLHF 的局限性

1. **奖励 hacking**: 模型可能学到利用奖励模型的漏洞
2. **人类偏好噪声**: 标注者不一致、文化偏见
3. **计算成本高**: PPO 需要同时在策略上采样和优化
4. **分布偏移**: 训练后的策略可能偏离奖励模型置信域

## RLVR (RL with Verifiable Rewards)

近期趋势（DeepSeek-R1 等）：对可自动验证的任务（数学正确性、代码通过测试），用客观奖励替代人类偏好：
- **GRPO** (Group Relative Policy Optimization)
- **PPO** 变体适应可验证奖励
- 详见 [[grpo-group-relative-policy-optimization]]

## 相关概念

- [[dpo-direct-preference-optimization]] — RL-free 替代方案
- [[preference-alignment]] — 偏好对齐全景
- [[instruction-tuning]] — SFT 阶段的指令微调
- [[reward-modeling]] — 奖励模型设计

## 待解决问题

- 如何组合 human feedback + verifiable rewards
- 多轮交互中的 RLHF
- 不同文化价值观的对齐
- RLHF 的可复现性和标准化评估
