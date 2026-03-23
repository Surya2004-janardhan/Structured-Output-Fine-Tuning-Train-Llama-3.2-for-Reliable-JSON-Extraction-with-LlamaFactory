# Project Plan: Structured Output Fine-Tuning Llama 3.2

The objective is to fine-tune Llama 3.2 to extract JSON data from invoices and purchase orders with high reliability and parsing success rate.

## Phase 1: Infrastructure & Schema (Design & Setup)
- Develop project structure for systematic tracking.
- Formalize JSON schemas for Invoices and Purchase Orders.
- Create `schema/invoice_schema.md` and `schema/po_schema.md` with explicit field definitions.

## Phase 2: Dataset Curation
- Gather raw invoice and PO text from Hugging Face datasets (CORD, SROIE, DocVQA).
- Manually curate 80 training examples (50 invoices, 30 POs) with gold labels.
- Verify each example against schema and document decisions in `data/curation_log.md`.
- Compile final `data/curated_train.jsonl`.

## Phase 3: Baseline & Prompt Experimentation
- Define a 20-document evaluation set (held-out from training).
- Conduct baseline evaluation of Llama 3.2 3B using standard prompting.
- Run a prompt engineering experiment on the 3 worst-performing documents.
- Document parse success rates and prompting efforts in `eval/` and `prompts/`.

## Phase 4: Parameter-Efficient Fine-Tuning (LoRA)
- Utilize LlamaFactory Web UI for fine-tuning.
- Set LoRA hyperparameters (rank, alpha, learning rate) and justify them in `training_config.md`.
- Execute training, monitor loss, and capture configuration/loss curve screenshots.

## Phase 5: Verification, Analysis & Submission
- Evaluate the fine-tuned model against the 20-document test set.
- Comparison: Populate `eval/before_vs_after.md` with side-by-side metrics.
- Failure Analysis: Deep dive into 5 remaining failures (`eval/failures/`).
- Final Report: Synthesize findings on Fine-tuning vs. Prompting in `report.md`.
- Final audit for structural integrity against submission requirements.
