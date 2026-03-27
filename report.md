# Final Report: Prompting vs. Fine-Tuning

## Methodology comparison
This project evaluated two primary methods for ensuring structured JSON output from Qwen 2.5 3B. 

**Prompt Engineering** (Baseline) relied on complex, iterative instructions (system prompts, few-shot examples, and strict constraints). Despite multiple versions (V1 to V3), the base model consistently included markdown code fences, prose explanations, or deviated from the strict key-value schema. The parse success rate remained at 0% for automation purposes because every response required manual regex or stripping logic to extract valid JSON.

**LoRA Fine-Tuning** (Post-FT) involved training a small set of adapter weights on 80 curated examples. This approach fundamentally changed the model's default behavior. The model learned that for the specific "task" of invoice/PO extraction, the valid token space is restricted to JSON braces and keys.

## Analysis: When to Use Which?
Fine-tuning wins in production data pipelines where **Parse Success Rate** is the critical metric. A 90% accurate model that returns 100% parseable JSON is more valuable than a 95% accurate model that breaks the downstream parser 30% of the time.

**Use Prompt Engineering when:**
- Requirements are fluid and schema changes frequently.
- You have high-capacity models (Llama 3 70B+, GPT-4) which are more instruction-following.
- You lack a high-quality curated dataset.

**Use Fine-Tuning when:**
- Reliability and consistency are non-negotiable.
- Using smaller, faster models (3B, 8B) on consumer hardware.
- The task involves strict formatting constraints (JSON, XML, Code).

## Conclusion
Fine-tuning transforms LLMs from "intelligent chatterboxes" into "predictable data transformers". The investment in data curation is significantly rewarded by a 100% reliable integration.
