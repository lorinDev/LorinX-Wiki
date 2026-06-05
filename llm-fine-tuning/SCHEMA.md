# Wiki Schema

## Domain
LLM 微调论文知识库 — 收录大语言模型微调相关的论文、技术报告、博客文章。
覆盖 SFT、RLHF、DPO、LoRA/PEFT、指令微调、偏好对齐、数据合成等领域。

## Conventions
- 文件名: 英文小写 + 连字符 (e.g., `lora-low-rank-adaptation.md`)
- 每页以 YAML frontmatter 开头 (见下方模板)
- 页面间用 `[[wikilinks]]` 链接 (每页至少 2 个出链)
- 更新页面时务必更新 `updated` 日期
- 每篇新页面必须添加到 `index.md` 对应分类下
- 每次操作必须追加到 `log.md`
- **溯源标记:** 综合 3+ 来源的页面, 在段落末尾添加 `^[raw/papers/xxx.md]` 标记
- 语言: 页面内容用中文撰写, 术语和论文标题保留英文

## Frontmatter
```yaml
---
title: 页面标题
created: YYYY-MM-DD
updated: YYYY-MM-DD
type: entity | concept | comparison | query | summary
tags: [from taxonomy below]
sources: [raw/papers/source-name.md]
confidence: high | medium | low
contested: true
contradictions: [other-page-slug]
---
```

## raw/ Frontmatter
```yaml
---
source_url: https://arxiv.org/abs/xxxx.xxxxx
ingested: YYYY-MM-DD
sha256: <hex digest of body content below frontmatter>
---
```

## Tag Taxonomy
添加新 tag 前必须先更新此列表。

### 方法 (Methods)
- `sft` — 监督微调
- `rlhf` — 基于人类反馈的强化学习
- `dpo` — 直接偏好优化及其变体
- `lora` — Low-Rank Adaptation 及 PEFT 方法
- `full-finetune` — 全参数微调
- `instruction-tuning` — 指令微调
- `alignment` — 对齐 (安全、价值观)
- `distillation` — 知识蒸馏
- `quantization` — 量化 + 微调 (QLoRA 等)
- `continual-pretraining` — 继续预训练
- `curriculum-learning` — 课程学习

### 模型 (Models)
- `llm` — 大语言模型
- `vlm` — 视觉语言模型
- `code-model` — 代码模型
- `embedding-model` — 嵌入模型
- `open-source` — 开源模型
- `closed-source` — 闭源模型

### 数据 (Data)
- `dataset` — 数据集
- `synthetic-data` — 合成数据
- `data-curation` — 数据筛选/清洗
- `data-augmentation` — 数据增强

### 评估 (Evaluation)
- `benchmark` — 基准评测
- `ablation` — 消融实验
- `evaluation` — 评估方法

### 论文类型 (Paper Type)
- `survey` — 综述
- `method` — 新方法/算法
- `empirical` — 实证研究
- `theoretical` — 理论分析
- `system` — 系统工程

### 元信息 (Meta)
- `comparison` — 对比分析
- `timeline` — 时间线/发展脉络
- `controversy` — 争议讨论
- `trend` — 趋势观察

## Page Thresholds
- **创建新页面** 当某实体/概念出现在 2+ 篇论文中 或 是一篇论文的核心
- **更新已有页面** 当新论文提到已覆盖的内容
- **不创建页面** 对一笔带过的提及或领域外内容
- **拆分页面** 当页面超过 ~200 行 — 拆为子主题
- **归档页面** 当内容已被完全取代 — 移至 `_archive/`

## Entity Pages
模型、数据集、机构、关键人物的页面。包含:
- 概述 / 是什么
- 关键信息 (发布时间、规模、作者机构)
- 与其他实体的关系 ([[wikilinks]])
- 来源引用

## Concept Pages
方法、技术的页面。包含:
- 定义 / 核心思想
- 发展脉络 (代表性论文时间线)
- 当前认知状态
- 待解决问题
- 相关概念 ([[wikilinks]])

## Comparison Pages
方法对比。包含:
- 比较对象和目的
- 对比维度 (表格优先)
- 结论或综合分析
- 来源

## Update Policy
当新信息与已有内容冲突时:
1. 检查日期 — 新来源通常优先
2. 如确有矛盾, 同时标注两方观点及日期来源
3. 在 frontmatter 标记 `contradictions: [page-name]`
4. Lint 报告中标出, 等待人工审核
