# Structured Output Fine-Tuning: Qwen 2.5 for Reliable JSON Extraction

[![LLM: Qwen 2.5](https://img.shields.io/badge/LLM-Qwen_2.5-blue.svg)](https://github.com/QwenLM/Qwen2.5)
[![Framework: LlamaFactory](https://img.shields.io/badge/Framework-LlamaFactory-orange.svg)](https://github.com/hiyouga/LLaMA-Factory)
[![Method: LoRA](https://img.shields.io/badge/Method-LoRA-green.svg)](https://arxiv.org/abs/2106.09685)

## Overview
This repository documents the process of fine-tuning a **Qwen 2.5 3B Instruct** model to reliably extract structured JSON data from unstructured business documents like invoices and purchase orders. By using Parameter-Efficient Fine-Tuning (**LoRA**) via the **LlamaFactory** web UI, we transform a general-purpose LLM into a specialized, machine-parseable data extractor.

## Key Features
- **Strict Schema Adherence**: Defined rigorous JSON schemas for Invoices and Purchase Orders.
- **Curated Dataset**: 80 high-quality training examples (50 invoices, 30 POs) with diverse layouts and edge cases.
- **LoRA Fine-Tuning**: Optimized training configuration (Rank 16, Alpha 32) for efficient adaptation.
- **Before-and-After Evaluation**: Rigorous comparison of baseline vs. fine-tuned performance on held-out documents.
- **Detailed Guides**: Local setup ([HOW_TO_FINE_TUNE.md](HOW_TO_FINE_TUNE.md)) and Google Colab ([COLAB_TRAINING_GUIDE.md](COLAB_TRAINING_GUIDE.md)).

## Repository Structure
- `schema/`: JSON schema definitions and documentation.
- `data/`: Curated training dataset (`.jsonl`) and curation log.
- `eval/`: Baseline and post-tuning evaluation responses, scores, and failure analyses.
- `prompts/`: Iterations and evaluation of prompt engineering experiments.
- `screenshots/`: Visual documentation of training configuration and loss curves.
- `training_config.md`: Justification for hyperparameter choices.
- `explanation.md`: Deep dive into project flows and methodology.

## Getting Started
1. **Explore Schema**: Review `schema/invoice_schema.md` for output format constraints.
2. **Review Data**: Inspect `data/curated_train.jsonl` to see input-output pairs.
3. **Compare Performance**: Check `eval/summary.md` and `eval/before_vs_after.md` (pending) for results.

## Contributing
This project is part of a structured training task. For methodology details, see the [Explanation Guide](explanation.md).
