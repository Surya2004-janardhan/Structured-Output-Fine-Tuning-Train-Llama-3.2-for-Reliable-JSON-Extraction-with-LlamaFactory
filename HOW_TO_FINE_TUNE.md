# Manual Step-by-Step Fine-Tuning Guide

This guide explains how to manually replicate the fine-tuning process using the **LlamaFactory** Web UI with the provided data.

## Phase 1: Environment Setup
1. **Clone & Install LlamaFactory**:
   ```bash
   git clone --depth 1 https://github.com/hiyouga/LLaMA-Factory.git
   cd LLaMA-Factory
   pip install -e ".[torch,metrics]"
   ```
2. **Ensure Dependencies**: You will need PyTorch and a compatible NVIDIA driver (or use CPU with slower performance).

## Phase 2: Register the Dataset
LlamaFactory needs to know about your custom dataset.
1. Copy `data/curated_train.jsonl` to the `LLaMA-Factory/data/` folder.
2. Edit `LLaMA-Factory/data/dataset_info.json` and add this entry:
   ```json
   "invoice_po_curated": {
     "file_name": "curated_train.jsonl",
     "columns": {
       "prompt": "instruction",
       "query": "input",
       "response": "output"
     }
   }
   ```

## Phase 3: Launch the Web UI
1. Run the Gradio interface:
   ```bash
   llamafactory-cli webui
   ```
2. Open the URL provided in the terminal (usually `http://127.0.0.1:7860`).

## Phase 4: Configure Training (Web UI)
In the **"Fine-tune"** tab, set the following:
- **Model Name**: Select `Llama-3.2-3B-Instruct`.
- **Stage**: Supervised Fine-tuning.
- **Dataset**: `invoice_po_curated`.
- **Training Method**: `LoRA`.
- **LoRA Rank (r)**: `16`.
- **LoRA Alpha**: `32`.
- **Learning Rate**: `0.0002`.
- **Epochs**: `3`.
- **Batch Size**: `4`.
- **Gradient Accumulation**: `2`.

## Phase 5: Execution
1. Click **"Start Training"**.
2. Monitor the loss curve in the "Loss" panel (should decrease steadily).
3. Once finished, go to the **"Export"** tab to save your adapter weights.

## Phase 6: Evaluation
1. Go to the **"Chat"** tab.
2. Ensure your fine-tuned adapter is loaded.
3. Paste a raw invoice or PO from `eval/` and verify that the output is clean, schema-compliant JSON.

---
**Tip**: Reference `training_config.md` in this repository for the full justification of these settings.
