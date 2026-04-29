---
title: "Transformer Limitations"
aliases:
  - "transformer architecture limits"
  - "what transformers cant do"
tags:
  - wiki
  - "agentic-architecture"
domain: "agentic-architecture"
sources:
  - "AI Engineer Chapter 2 (Chip Huyen, 2025).md"
status: stub
confidence: medium
---

Created: Wednesday, 29 April 2026, 13:12
Modified: `=dateformat(this.file.mtime, "DDDD, HH:mm")`

---

# Transformer Limitations

**Summary**: The transformer architecture (dominating language-based foundation models) was designed to address specific problems — but has inherent limitations. Understanding what transformers can't do well is key to designing agentic systems that work around them.

**Sources**: [[raw/AI Engineer Chapter 2 (Chip Huyen, 2025).md|AI Engineering Chapter 2]]

---

## The Architecture

The transformer architecture has been the dominating architecture for language-based foundation models. It was designed to solve specific problems with sequence modeling — particularly long-range dependencies and parallelization.

## Known Limitations

### 1. Context Length Limits
Transformers process tokens within a fixed context window. Beyond that window, the model cannot "see" earlier tokens. This directly impacts [[context-reliability]] — long conversations or large codebases can exceed what the model can attend to.

### 2. Hallucinations from Probabilistic Sampling
The probabilistic nature of transformer outputs (inference involves sampling) means models can produce confident but incorrect outputs. [[RLHF]] mitigates this but doesn't eliminate it.

### 3. Computationally Expensive at Inference
Self-attention scales quadratically with sequence length. Longer contexts = more compute = higher latency. This affects real-time agentic applications.

### 4. Limited Symbolic Reasoning
Transformers learn statistical patterns from training data. They can approximate reasoning but don't perform true logical deduction reliably. This is why agents need tools — the model alone can't reliably execute multi-step logical plans.

### 5. Data Efficiency
Massive amounts of data are required to train competitive models. Low-resource languages and specialized domains suffer because transformers require enormous, diverse datasets to perform well.

## Implications for Agentic Architecture

- Agents built on transformers need **robust error handling** — the model will hallucinate or lose context
- Tool use is a workaround for symbolic reasoning limitations
- Long-horizon tasks require memory systems because the context window is fixed
- Evaluation is critical because transformers can fail silently on edge cases

## Related Pages

- [[agentic-architecture]]
- [[context-reliability]]
- [[rlhf]]
