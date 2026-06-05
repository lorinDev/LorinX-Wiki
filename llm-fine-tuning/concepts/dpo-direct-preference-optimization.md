---
title: DPO (Direct Preference Optimization)
created: 2026-06-03
updated: 2026-06-03
type: concept
tags: [dpo, rlhf, alignment, method]
sources: [raw/papers/dpo-2305.18290.md, raw/papers/dpo-survey-2410.15595.md]
confidence: high
---

# DPO: Direct Preference Optimization

## 核心思想

DPO 通过重新参数化 RLHF 中的奖励模型，**直接从偏好数据中优化策略**，无需显式训练奖励模型，也无需强化学习。将 RLHF 问题转化为**简单的分类损失**。

**核心洞察：** 语言模型本身就隐含了一个奖励函数，可直接从中提取最优策略的闭式解。

## 问题背景

传统 RLHF 三步流水线：
1. 收集人类偏好数据（chosen vs rejected）
2. 训练奖励模型 (Reward Model)
3. 用 PPO 强化学习优化策略

DPO 直接跳过步骤 2 和 3 中的 RL 部分。

## 技术优势

| 维度 | RLHF (PPO) | DPO |
|------|-----------|-----|
| 奖励模型 | 需要单独训练 | **不需要** |
| 训练方式 | 强化学习（采样+优化） | **分类损失** |
| 稳定性 | 可能崩溃/奖励过拟合 | **稳定** |
| 超参调优 | 复杂（KL 惩罚系数等） | **简单** |
| 计算开销 | 训练时需采样生成 | **轻量** |

## 实验结果

- **情感控制**: DPO **超越** PPO-based RLHF
- **摘要 & 单轮对话**: 匹配或超越现有方法
- **实现复杂度**: 大幅降低

## 主要变体（来自 DPO 综述 2410.15595）

根据综述的分类：
- **IPO** (Azar et al., 2023) — Identity Preference Optimization，解决过拟合
- **KTO** (Ethayarajh et al., 2024) — Kahneman-Tversky Optimization，只需单边偏好
- **CPO** (Xu et al., 2024) — Contrastive Preference Optimization
- **SimPO** (Meng et al., 2024) — Simple Preference Optimization，用序列平均对数概率
- **Cal-DPO** (NeurIPS 2024) — Calibrated DPO，校准的偏好优化
- **sDPO, CPL** 等更多变体

综述论文 [[raw/papers/dpo-survey-2410.15595]] 从四个维度分类：理论分析、变体、数据集、应用。

## 局限性

- 偏好数据集质量和分布偏移仍是挑战
- 与 RLVR 方法（GRPO 等）相比，在可验证奖励场景（数学/代码）中可能不如 RL 方法
- 过优化问题（overoptimization）依然存在

## 相关概念

- [[rlhf-reinforcement-learning-human-feedback]] — RLHF 对比
- [[preference-alignment]] — 偏好对齐全景
- [[grpo-group-relative-policy-optimization]] — GRPO 方法

## 待解决问题

- DPO vs RLVR（GRPO/PPO）的最优适用场景划分
- 多轮对话中的偏好优化
- 在线 vs 离线 DPO 的权衡
- 合成偏好数据的生成策略（见 [[synthetic-data-fine-tuning]]）
