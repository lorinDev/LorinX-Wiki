---
title: LoRA (Low-Rank Adaptation)
created: 2026-06-03
updated: 2026-06-03
type: concept
tags: [lora, peft, full-finetune, method]
sources: [raw/papers/lora-2106.09685.md]
confidence: high
---

# LoRA: Low-Rank Adaptation

## 核心思想

LoRA 是一种**参数高效微调 (PEFT)** 方法，核心假设是：预训练大模型在适配下游任务时，权重更新矩阵是**低秩 (low-rank)** 的。因此不需要更新全部参数，只需注入可训练的低秩分解矩阵。

**数学形式：** 对于预训练权重 $W_0 \in \mathbb{R}^{d \times k}$，LoRA 将其更新约束为：

$$W = W_0 + \Delta W = W_0 + BA$$

其中 $B \in \mathbb{R}^{d \times r}$，$A \in \mathbb{R}^{r \times k}$，且秩 $r \ll \min(d, k)$。

- $W_0$ 冻结，仅训练 $A$ 和 $B$
- 推理时 $BA$ 可合并回 $W_0$，**无额外推理延迟**

## 关键论文

| 论文 | 时间 | 贡献 |
|------|------|------|
| [LoRA](https://arxiv.org/abs/2106.09685) (Hu et al.) | 2021.06 | 提出 LoRA 方法，验证低秩假设 |

## 主要优势

1. **参数量暴降**：相比 GPT-3 175B 全量微调，可训练参数减少 **10,000×**
2. **显存节省**：GPU 显存需求降低 **3×**
3. **零推理延迟**：与 adapter 不同，LoRA 矩阵可合并回原权重
4. **多任务切换**：只需换 LoRA 权重，不换基座模型
5. **性能不降**：在 RoBERTa、DeBERTa、GPT-2/3 上达到或超过全量微调

## 理论支撑

论文通过实验证明：语言模型适配下游任务时的权重更新确实存在**秩缺失 (rank-deficiency)**，即高维权重矩阵的有效更新维度远小于矩阵维度。这从理论上解释了为何低秩逼近足够。

## 变体与衍生

- [[qlora-quantized-lora]] — 量化 + LoRA，4-bit 精度下微调 65B 模型
- DoRA (Weight-Decomposed Low-Rank Adaptation, 2024) — 将权重分解为幅度+方向，对方向做 LoRA
- AdaLoRA — 自适应分配秩到不同层

## 相关概念

- [[peft-parameter-efficient-fine-tuning]] — PEFT 方法总览
- [[qlora-quantized-lora]] — 量化 LoRA
- [[full-finetuning]] — 全参数微调对比

## 待解决问题

- 最优秩 $r$ 的选择依赖任务，尚无通用准则
- 不同层对秩的需求不同（AdaLoRA 尝试解决）
- 与 [[dpo-direct-preference-optimization]] 等对齐方法的结合仍在探索
