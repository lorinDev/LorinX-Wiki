---
title: RLHF vs DPO 方法对比
created: 2026-06-03
updated: 2026-06-03
type: comparison
tags: [comparison, rlhf, dpo, alignment]
sources: [raw/papers/dpo-2305.18290.md, raw/papers/rlhf-survey-2312.14925.md]
confidence: high
---

# RLHF vs DPO: 偏好优化方法对比

## 对比目的

选择 LLM 对齐阶段的优化方法：传统 RLHF (PPO) 还是 DPO 及其变体。

## 方法本质

| 维度 | RLHF (PPO) | DPO |
|------|-----------|-----|
| 优化框架 | 强化学习（在线策略梯度） | 分类损失（离线） |
| 奖励模型 | **需要** 单独训练 | **不需要**（隐式） |
| KL 约束 | 显式 KL 惩罚项 | 内化在损失函数中 |
| 训练稳定性 | 需要调参（KL 系数等） | 开箱即用 |
| 采样需求 | 训练时需在线生成 | 仅用离线偏好对 |

## 计算开销

| | RLHF (PPO) | DPO |
|--|-----------|-----|
| 额外模型 | 奖励模型（与策略同规模） + 值网络（可选） | 无 |
| 训练时推理 | 需要（rollout 采样） | **不需要** |
| GPU 显存 | 高（同时加载策略+RM+优化器） | 低 |
| 实现复杂度 | 高（RL 训练循环 + 多组件协调） | **低**（等价于标准分类） |

## 性能表现

| 任务 | 胜出 | 备注 |
|------|------|------|
| 情感控制 | **DPO** | DPO 在精确控制情感方向时优于 PPO |
| 摘要 (TL;DR) | 持平 | 两者性能相当 |
| 单轮对话 | DPO ≥ PPO | DPO 匹配或超越 |
| 数学/代码推理 | **RLVR** (GRPO) | DPO 弱于 RL with verifiable rewards |
| 多轮对话 | 争议 | 缺乏决定性结论 |

## 何时用 RLHF (PPO/GRPO)

- **有可验证奖励信号**（数学正确性、测试通过）— 使用 GRPO 等 RLVR 方法
- 需要**探索策略空间**（在线采样引入多样性）
- 奖励模型已训练好，切换成本低

## 何时用 DPO

- 有现成的**偏好数据集**
- 追求**实现简单**、快速迭代
- 资源受限（单 GPU）
- 不需要在线探索（离线偏好对足够）

## 混合策略

最新趋势：**不二选一**，而是组合：
1. DPO 做初期快速对齐（成本低）
2. RLVR (GRPO) 在可验证任务上做精细化优化
3. Iterative DPO: 在线采样 + DPO，兼顾探索和效率

## 相关概念

- [[dpo-direct-preference-optimization]] — DPO 详细分析
- [[rlhf-reinforcement-learning-human-feedback]] — RLHF 详细分析
- [[preference-alignment]] — 偏好的全景

## 结论

没有"绝对更好"的方法。选择取决于：
- **是否有可验证奖励**（有 → RLVR；无 → DPO/RLHF）
- **偏好数据形式**（成对 → DPO；单边 → KTO）
- **资源预算**（低 → DPO；高 → RLHF）
- **任务复杂度**（简单 → DPO；需探索 → RLHF）

实践中，DPO 因其简洁性已成为大多数项目的默认选择，但在 DeepSeek-R1 等工作带动下，RLVR 在推理任务中重新崛起。
