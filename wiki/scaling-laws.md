---
title: "Scaling Laws"
aliases:
  - "scaling law"
  - "model scaling"
  - "compute budget"
tags:
  - wiki
  - "agentic-architecture"
  - "context-reliability"
domain: "agentic-architecture"
sources:
  - "AI Engineer Chapter 2 (Chip Huyen, 2025).md"
status: stub
confidence: high
---

Created: Wednesday, 29 April 2026, 13:12
Modified: `=dateformat(this.file.mtime, "DDDD, HH:mm")`

---

# Scaling Laws

**Summary**: Model scale is measured by three key numbers — parameters, training tokens, and FLOPs. Scaling laws determine the optimal combination given a compute budget. Scaling up has historically improved performance, but bottlenecks are emerging.

**Sources**: [[raw/AI Engineer Chapter 2 (Chip Huyen, 2025).md|AI Engineering Chapter 2]]

---

## Three Key Numbers

| Metric | What It Measures |
|---|---|
| **Parameters** | Model size — more parameters = more capacity |
| **Training Tokens** | Data the model was trained on |
| **FLOPs** | Compute required to train |

## The Scaling Law

Given a **compute budget** (how much compute you can afford to train with), the scaling law determines the **optimal number of parameters** and **optimal number of training tokens**.

Key insight: you can trade off model size vs. data size. A smaller model trained on more data can perform as well as a larger model trained on less data — within the same compute budget.

## Scaling Bottlenecks

Up until recently, scaling up a model generally made it better. The question now is: **how long will this continue to be true?**

Bottlenecks emerge when:
- Data becomes a limiting factor (running out of high-quality training data)
- Compute efficiency plateaus
- Diminishing returns on certain tasks

## Why It Matters for AI Engineering

- **Model selection**: Understanding scaling helps you choose the right model for your budget and use case
- **Context reliability**: Larger context windows ≠ better performance; scaling law helps frame this
- **Token budgets**: Compute costs scale with model size and token count

## Related Pages

- [[rlhf]]
- [[agentic-architecture]]
- [[context-reliability]]
