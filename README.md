# Structured Output Fine-Tuning: Llama 3.2 for Reliable JSON Extraction

[![LLM: Llama 3.2](https://img.shields.io/badge/LLM-Llama_3.2-blue.svg)](https://huggingface.co/meta-llama/Llama-3.2-3B-Instruct)
[![Framework: LlamaFactory](https://img.shields.io/badge/Framework-LlamaFactory-orange.svg)](https://github.com/hiyouga/LLaMA-Factory)
[![Method: LoRA](https://img.shields.io/badge/Method-LoRA-green.svg)](https://arxiv.org/abs/2106.09685)

## Overview
This repository documents the successful fine-tuning of **Llama 3.2 3B Instruct** to reliably extract structured JSON data from unstructured business documents (Invoices & Purchase Orders). By applying **LoRA** (Low-Rank Adaptation) via **LlamaFactory**, we achieved a 100% parse success rate, eliminating the prose and formatting issues common in base LLMs.

## Visual Proof

### 1. Training Convergence (Loss Curve)
![Loss Curve](screenshots/loss_curve.png)
*The loss decreased steadily over 3 epochs, indicating successful learning of the schema constraints.*

### 2. Fine-Tuned Chat Success
![Chat Success](screenshots/success_chat.png)
*The model now responds with pure, machine-parseable JSON without any markdown fences or preamble.*

## Key Features
- **Strict Schema Adherence**: Rigorous JSON schemas for Invoices and Purchase Orders.
- **High-Quality Training Set**: 80 curated examples with diverse layouts.
- **LoRA Optimization**: Efficient adaptation with Rank 16 / Alpha 32.
- **100% Parse Reliability**: Verified results with zero-shot extraction.
- **Guides**: [Local Setup Guide](HOW_TO_FINE_TUNE.md) and [Google Colab Guide](COLAB_TRAINING_GUIDE.md).

## Repository Structure & File Purpose
For a detailed explanation of every file and how they work together, see the **[Explanation Guide](explanation.md)**.

## Getting Started
1. **Explore Schema**: See `schema/invoice_schema.md`.
2. **Review Results**: See `eval/summary.md`.
3. **Try the Model**: Access the fine-tuned weights on Hugging Face (Link in report).
