---
source_url: https://arxiv.org/abs/2305.14314
ingested: 2026-06-03
---
# QLoRA: Efficient Finetuning of Quantized LLMs

- **Authors**: Tim Dettmers, Artidoro Pagnoni, Ari Holtzman, Luke Zettlemoyer
- **Published**: May 2023
- **Venue**: NeurIPS 2023
- **License**: CC BY 4.0

## One-Liner
Backpropagates gradients through a frozen 4-bit quantized model into LoRA adapters; finetunes a 65B model on a single 48GB GPU.

## Key Results
- Guanaco: 99.3% of ChatGPT on Vicuna benchmark
- 24 hours fine-tuning on single GPU
- >1,000 models fine-tuned across LLaMA, T5, 8 datasets
- GPT-4 evaluation is cheap proxy for human evaluation
