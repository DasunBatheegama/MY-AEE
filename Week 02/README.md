# Week 02: LLM Fine-tuning Workshop

> **QLoRA fine-tuning sprint: 4-bit quantization + LoRA on a medical AI assistant, with LLM-as-Judge evaluation and GGUF export.**

[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![Hugging Face](https://img.shields.io/badge/HuggingFace-Transformers-yellow.svg)](https://huggingface.co/)
[![Google Gemini](https://img.shields.io/badge/Eval-Gemini-blue.svg)](https://aistudio.google.com/)

---

## What You'll Build

- Baseline inference on a pretrained instruction-tuned model
- QLoRA fine-tuning (4-bit quantization + Low-Rank Adaptation) on medical instruction data
- Evaluation with LLM-as-Judge (Gemini) and ROUGE-L metrics
- Safety guardrail testing with LLM-based evaluation
- **Bonus**: GGUF export for local deployment

---

## Materials

| Resource | Description |
|----------|-------------|
| `llm finetuning workshop.ipynb` | Interactive workshop template (fill in as you go) |
| `llm finetuning full workshop - completed.ipynb` | Completed reference notebook |
| `week 02 - LLM Finetuning Workshop - Guide.pdf` | PDF walkthrough and guide |

This is a **3-hour hands-on sprint** — start with the template notebook and use the completed version as reference.

---

## Quick Start

```bash
cd "Week 02"

# 1. Environment
cp .env.sample .env
# Fill in: HF_TOKEN, GOOGLE_API_KEY

# 2. Install dependencies (from notebook cell 0)
# Dependencies are installed inline in the notebook

# 3. Launch
jupyter notebook
# Open "llm finetuning workshop.ipynb"
```

> **Note**: A GPU is strongly recommended (Google Colab T4/A100, or local CUDA GPU). CPU-only will be very slow.

---

## API Keys

| Provider | Variable | Get Key | Purpose |
|----------|----------|---------|---------|
| Hugging Face | `HF_TOKEN` | [huggingface.co/settings/tokens](https://huggingface.co/settings/tokens) | Model access and uploads |
| Google AI | `GOOGLE_API_KEY` | [aistudio.google.com](https://aistudio.google.com/app/apikey) | LLM-as-Judge evaluation (Gemini) |

---

## Workshop Sections

| # | Section | What You'll Do |
|---|---------|----------------|
| 1 | Environment setup | GPU check, seeds, Hugging Face login |
| 2 | Configuration | Single source of truth for all hyperparameters |
| 3 | Dataset loading | Medical instruction dataset with fallback |
| 4 | Baseline inference | Run the pretrained model before fine-tuning |
| 5 | QLoRA fine-tuning | 4-bit quantization + LoRA adapters |
| 6 | Post-finetune inference | Compare outputs against baseline |
| 7 | Evaluation | LLM-as-Judge (Gemini) + ROUGE-L metrics |
| 8 | Guardrails | Safety evaluation with LLM-based testing |
| 9 | **Bonus**: GGUF export | Convert to GGUF for local/offline deployment |

---

## Key Concepts

- **QLoRA**: Combines 4-bit quantization (NF4) with Low-Rank Adaptation — fine-tune large models on consumer GPUs
- **LoRA**: Adds small trainable rank-decomposition matrices to frozen model weights
- **LLM-as-Judge**: Uses a stronger model (Gemini) to evaluate fine-tuned outputs on correctness, relevance, and safety
- **ROUGE-L**: Longest common subsequence metric for text generation quality
- **GGUF**: Quantized model format for efficient local inference (llama.cpp compatible)

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| **"CUDA out of memory"** | Reduce batch size, use gradient checkpointing, or switch to a smaller model |
| **"No GPU available"** | Use Google Colab (free T4) or set runtime to GPU in Colab settings |
| **HF model gated** | Accept the model license on huggingface.co, then set `HF_TOKEN` |
| **Slow training** | Expected on CPU — use GPU. On Colab free tier, expect ~30-60 min for fine-tuning |
| **GGUF export fails** | Ensure `llama-cpp-python` is installed; may need `CMAKE_ARGS` for your platform |

---

**Contact:** hi@zuucrew.ai · *Built with Zuu Crew*
