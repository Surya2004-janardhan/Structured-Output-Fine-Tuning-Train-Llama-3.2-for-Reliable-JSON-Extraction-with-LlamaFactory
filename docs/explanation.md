# Project Explanation: Top-to-Bottom Workflow

This document provides a comprehensive walkthrough of the technical methodology and flows implemented in this project.

## 1. Project Objective
The goal is to solve the **Reliability Problem** in LLM-based data extraction. General LLMs often return prose, markdown fences, or inconsistent keys. Fine-tuning with LoRA converts these "formatting preferences" into "hard constraints".

## 2. Technical Workflow
The project follows a 5-phase execution flow:

### Flow A: Schema Design (The Blueprint)
Before any data curation, we established the "Ground Truth".
- **Functions**: Defined mandatory keys, data types, and null-handling logic.
- **Output**: `schema/invoice_schema.md` and `schema/po_schema.md`.

### Flow B: Data Curation (The Foundation)
We curated 80 examples sourced from datasets like CORD and SROIE.
- **Methodology**: 
  - 50 Invoices, 30 Purchase Orders.
  - Ensuring diversity in layout, currency, and multi-line items.
  - Manual review logged in `data/curation_log.md`.
- **Output**: `data/curated_train.jsonl`.

### Flow C: Baseline & Prompting (The Control)
Establishing how the base model performs without fine-tuning.
- **Methodology**: 20 held-out documents tested against a "Gold Standard" prompt.
- **Insight**: Even with strict prompting, base models struggle with consistent machine-parseable JSON.

### Flow D: Fine-Tuning (The Training)
Using LlamaFactory to inject the schema knowledge into the model weights using LoRA.
- **Hyperparameters**:
  - **Rank 16**: Enough capacity for structural learning.
  - **Alpha 32**: Scaling factor for weights.
  - **Learning Rate 2e-4**: Balanced convergence.
- **Visuals**: Confirmed via `screenshots/loss_curve.png`.

### Flow E: Evaluation & Analysis (The Verdict)
Final verification (in progress) comparing the fine-tuned model against the baseline.
- **Metric**: Parse Success Rate (percentage of responses that are valid JSON + schema-compliant).

## 3. Directory & File Purpose
| Directory | Purpose |
| :--- | :--- |
| `schema/` | Defines the REST API or database-ready JSON structure. |
| `data/` | The raw "experience" the model learns from. |
| `training_config.md` | The "recipe" for the training process. |
| `eval/` | Proof of performance improvement. |

## 4. How We Do It All
We use **Supervised Fine-Tuning (SFT)**. By presenting the model with hundreds of examples where the only correct behavior is responding with a specific JSON object, the model's likelihood for those tokens (keys and braces) increases dramatically relative to prose tokens. This "specialization" ensures that the model treats JSON formatting as its primary task.
