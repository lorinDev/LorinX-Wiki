# Wiki Log

> 所有 wiki 操作的时序记录。只追加, 不修改。
> 格式: `## [YYYY-MM-DD] action | subject`
> Actions: ingest, update, query, lint, create, archive, delete
> 超过 500 条时轮转: 重命名为 log-YYYY.md, 新建 log.md

## [2026-06-03] create | Wiki initialized
- Domain: LLM 微调论文知识库 (Fine-tuning papers for Large Language Models)
- 创建目录结构: SCHEMA.md, index.md, log.md
- 子目录: raw/{articles,papers,transcripts,assets}, entities, concepts, comparisons, queries, _archive
- Tag 体系: 方法(11) + 模型(6) + 数据(4) + 评估(3) + 论文类型(5) + 元信息(4) = 33 tags
- 准备就绪, 待摄入首批论文

## [2026-06-03] ingest × 10 | Initial paper batch
摄入 10 篇核心论文:
- LoRA (2106.09685) — 奠基 PEFT 方法
- QLoRA (2305.14314) — 量化微调突破
- DPO (2305.18290) — RL-free 对齐奠基
- DPO Survey (2410.15595) — DPO 变体全览
- RLHF Survey (2312.14925) — RLHF 全面综述
- RL Post-Training Survey (2407.16216) — 统一策略梯度框架
- Instruction Tuning Survey (2308.10792) — SFT 全流程综述
- PEFT Survey (2403.14608) — PEFT 算法+系统
- Synthetic Data Survey (2503.14023) — 合成数据方法
- Alignment Survey (2505.02666) — 奖励设计视角对齐

## [2026-06-03] create × 9 | Concept & comparison pages
创建 8 个概念页: lora, qlora, dpo, rlhf, instruction-tuning, peft, synthetic-data, preference-alignment
创建 1 个对比页: rlhf-vs-dpo
更新 index.md 含完整目录
