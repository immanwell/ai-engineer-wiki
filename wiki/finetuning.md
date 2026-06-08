---
title: "Finetuning"
aliases:
  - "PEFT"
  - "LoRA"
  - "parameter-efficient finetuning"
  - "model finetuning"
tags:
  - wiki
  - "context-reliability"
domain: "context-reliability"
sources:
  - "AI Engineer Chapter 7 (Chip Huyen, 2025).md"
status: stable
confidence: high
---

Created: Monday, 8 June 2026, 21:42
Modified: `=dateformat(this.file.mtime, "DDDD, HH:mm")`

---

# Finetuning

**Summary**: Finetuning adapts a foundation model's weights to a specific task or domain. The main decisions are: whether to finetune at all (vs RAG), whether to do full finetuning or parameter-efficient finetuning (PEFT), and which PEFT method to use (LoRA is the dominant choice).

**Sources**: [[raw/AI Engineer Chapter 7 (Chip Huyen, 2025).md|AI Engineering Chapter 7]]

---

## When to Finetune

Finetuning is not the first tool to reach for. The typical decision flow:

```txt
Failure mode identified
       ↓
Try prompt engineering first (cheapest)
       ↓
Try RAG if knowledge is the gap
       ↓
Try finetuning if behavior/style/format is the gap
```

**Finetune when**:
- The model's output style, tone, or format needs consistent adjustment
- You need the model to follow task-specific conventions that prompts can't reliably enforce
- Latency or cost from long system prompts is a problem
- Domain vocabulary is so specialized that retrieval doesn't help

**Use RAG when**:
- The gap is factual knowledge (documents, policies, recent events)
- The knowledge changes frequently
- You can't get enough training data for finetuning

These aren't mutually exclusive — many production systems use both.

## RAG vs Finetuning

| Dimension | RAG | Finetuning |
|-----------|-----|------------|
| **Knowledge gap** | External facts, documents | Behavior, style, format |
| **Data freshness** | Updates instantly | Requires retraining |
| **Training data needed** | None | Annotated examples |
| **Infrastructure** | Vector DB + retriever | GPU compute for training |
| **Latency** | Higher (retrieval step) | Lower (no retrieval) |
| **Cost** | Higher per query | Higher upfront, cheaper per query |

## Full Finetuning vs PEFT

### Full Finetuning

Updates all model weights. Was the original approach, derived from pre-training workflows.

**Problem**: As models grew to billions of parameters, full finetuning became impractical for most practitioners. The memory requirement scales with the number of trainable parameters — too expensive for most teams.

### PEFT (Parameter-Efficient Fine-Tuning)

Achieves strong performance by updating only a small subset of the model's parameters.

**Why it works**: Most of a model's learned knowledge is preserved in the original weights. Only a targeted layer or adapter needs to change to adapt behavior.

**Key benefit**: Dramatically reduced memory footprint — enables finetuning on consumer hardware.

## LoRA — The Dominant PEFT Method

LoRA (Low-Rank Adaptation) works by injecting small, trainable matrices alongside the frozen pre-trained weight matrices.

### How It Works

Instead of updating a large weight matrix W directly, LoRA decomposes the update into two smaller matrices:

```txt
W_updated = W_original + (A × B)
```

Where A and B are low-rank matrices (far fewer parameters than W). Only A and B are trained — W stays frozen.

**Low-rank factorization**: The key insight is that the meaningful adaptation for most tasks lives in a low-dimensional subspace. You don't need to update every weight to shift behavior.

### Why LoRA Is Popular

- **Parameter-efficient**: Only the small A and B matrices are trainable — 10–1000x fewer parameters than full finetuning
- **Data-efficient**: Works with smaller annotated datasets
- **Modular**: LoRA adapters are separate files that sit on top of the base model
- **Easy to serve**: One base model can serve many LoRA adapters — swap adapters per user or task at inference time
- **Composable**: Multiple LoRA adapters can be merged or combined

## Quantized Training

An alternative route to reducing memory footprint: instead of reducing the *number* of trainable parameters, reduce the *precision* of each value.

> **Note**: Quantized *training* (reducing precision during training to save GPU memory) is distinct from inference *quantization* (reducing precision at serving time to reduce cost and latency). Both use the same underlying technique but serve different goals. See [[inference-optimization]] for the serving-time version.

- Full precision: 32-bit floats (FP32)
- Mixed precision: 16-bit (FP16, BF16) — minimal accuracy loss, ~2x memory savings
- Quantized: 8-bit or 4-bit — more aggressive compression, some accuracy tradeoff

Quantized training can be combined with PEFT — QLoRA (Quantized LoRA) is a common stack for finetuning large models on limited hardware.

## Model Merging

Model merging combines multiple finetuned models into one model that outperforms each individual model.

**Use cases**:
- **On-device deployment**: Merge task-specific adapters into one compact model
- **Model upscaling**: Combine specialist models to approach generalist capability
- **Multi-domain**: Merge models finetuned on different domains into a unified model

The key insight is that if multiple LoRA adapters were trained from the same base, their parameter updates can often be arithmetically combined.

## The Data Problem

A recurring practitioner observation: **finetuning is easy; getting data for finetuning is hard**.

- High-quality instruction data is expensive to annotate
- Data quality matters more than quantity for finetuning
- Synthetic data (AI-generated instruction pairs) is now a mainstream solution — but requires its own evaluation pipeline

See [[dataset-engineering]] for the full framework: three criteria (quality/coverage/quantity), data by training phase, synthetic data techniques, and the non-automatable parts of annotation.

## Exam Relevance

This chapter is not a primary exam domain, but connects to:
- [[context-reliability]] — RAG vs finetuning is a retrieval architecture decision
- [[prompt-engineering]] — prompting is always tried before finetuning
- [[rlhf]] — SFT (a form of full finetuning) is the first step in RLHF

## Related Pages

- [[rag-retrieval]] — the main alternative to finetuning for knowledge gaps
- [[rlhf]] — SFT is full finetuning applied to alignment
- [[build-vs-buy-ai]] — finetuning is a build decision with real infrastructure costs
- [[foundation-model-evaluation]] — evaluate before and after finetuning to measure delta
- [[private-model-selection]] — finetuned models need their own private leaderboard
