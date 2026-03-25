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

## Troubleshooting

### Error: "Your setup doesn't support bf16/gpu"
If you see this error when clicking "Start Training", it means LlamaFactory is trying to use an NVIDIA GPU with BF16 precision, but your hardware doesn't support it (or you are running on CPU).

**How to fix:**
1. **Change Compute Type**: In the "Fine-tune" tab, look for **"Compute Type"** or **"Precision"**. Change it from `bf16` to **`fp16`** or **`fp32`**.
2. **Enable CPU Mode**: If you don't have a discrete NVIDIA GPU, look for a **"Use CPU"** checkbox or set the device to **`cpu`**.
3. **Advanced**: If using a config file, set `bf16: false` and `fp16: true` (for older GPUs) or `fp16: false` (for CPU).

### Error: "OSError: You are trying to access a gated repo"
Llama 3.2 is a gated model. You must request access and authenticate to download it.

**How to fix (401 Unauthorized):**
1. **Request Access**: Visit [huggingface.co/meta-llama/Llama-3.2-3B-Instruct](https://huggingface.co/meta-llama/Llama-3.2-3B-Instruct) and click "Request Access".
2. **Create a Token**: Go to [huggingface.co/settings/tokens](https://huggingface.co/settings/tokens) and create a "Read" token.
3. **Login in Terminal**:
   ```bash
   source myenv/bin/activate
   huggingface-cli login
   ```
   Paste your token when prompted.
4. **Restart LlamaFactory**: Once logged in, restart the `llamafactory-cli webui` command.

**How to fix (403 Forbidden - "Awaiting Review"):**
If you see the message **"Your request to access model is awaiting a review from the repo authors"**:
- This means you have successfully requested access but **Meta hasn't approved it yet**.
- **Action**: You must wait for an email from Hugging Face confirming your access is granted. This usually takes from 10 minutes to a few hours.
- Once you receive the "Access granted" email, the 403 error will disappear and the download will start automatically.



