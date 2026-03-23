# Training Configuration & Justification

## Model & Method
- **Base Model**: Llama-3.2-3B-Instruct
- **Fine-tuning Method**: LoRA (Low-Rank Adaptation)
- **Framework**: LlamaFactory (Gradio Web UI)

## Hyperparameters

| Parameter | Value | Justification |
| :--- | :--- | :--- |
| **LoRA Rank (r)** | 16 | Chosen to provide enough capacity to learn the specific JSON schema constraints without excessive memory overhead. |
| **LoRA Alpha** | 32 | Following the common practice of `2 * Rank`, which acts as a scaling factor for the adapter weights. |
| **Learning Rate** | 2e-4 | A standard starting point for LoRA on 3B models; large enough to converge in few epochs but small enough to avoid catastrophic forgetting. |
| **Epochs** | 3 | Sufficient for the model to learn the structured format from 80 examples. More epochs risk overfitting to the specific synthetic values. |
| **Batch Size** | 4 | Maximize GPU utilization while fitting within standard 8GB-12GB VRAM limits. |
| **Dataset** | `curated_train.jsonl` | 80 high-quality, manually curated (synthetic) examples. |

## Observations
The training is expected to show a smooth decrease in loss. Given the structured nature of the target output, the model should quickly pick up the JSON formatting (braces, quotes, colons) within the first epoch.
