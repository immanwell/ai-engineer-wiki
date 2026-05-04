---
title: "Foundation Model Evaluation"
aliases:
  - "evaluating foundation models"
  - "AI system evaluation"
tags:
  - wiki
  - "context-reliability"
domain: "context-reliability"
sources:
  - "AI Engineer Chapter 2 (Chip Huyen, 2025).md"
  - "AI Engineer Chapter 3 (Chip Huyen, 2025).md"
  - "AI Engineer Chapter 4 (Chip Huyen, 2025).md"
status: stable
confidence: high
---

Created: Wednesday, 29 April 2026, 13:12
Modified: `=dateformat(this.file.mtime, "DDDD, HH:mm")`

---

# Foundation Model Evaluation

**Summary**: Evaluation for foundation models is foundational to systematic AI engineering. Chip Huyen dedicates two chapters (3 and 4) to it. The first step is establishing a solid evaluation pipeline to detect failures and unexpected changes.

**Sources**: [[raw/AI Engineer Chapter 2 (Chip Huyen, 2025).md|AI Engineering Chapter 2]]

---

## Why It Matters

Working with AI models requires building your workflows around their **probabilistic nature**. Unlike traditional software, AI outputs are not deterministic — the same input can produce different outputs.

Without evaluation:
- Hallucinations go undetected
- Model changes silently degrade performance on specific tasks
- No systematic way to detect regressions when updating prompts or models

## The "Systematic AI Engineering" Framework

Chip frames systematic AI engineering as building workflows that are **at least systematic if not deterministic**. Evaluation is the first step.

## Evaluation Methods (Chapter 3)

Two complementary approaches:

| Method | Type | Use Case |
|--------|------|----------|
| [[functional-correctness]] | Exact — binary pass/fail | Code compilation, math, factual retrieval |
| [[ai-as-a-judge]] | Subjective — judge-dependent scores | Open-ended: tone, helpfulness, coherence |

**Best practice**: Use both together. AI-as-a-judge must be validated against functional metrics. Supplement with human evaluation for high-stakes outputs.

## Comparative Evaluation

Beyond absolute scores: which model is better? Requires preference signals (expensive to collect). Common in chess (Elo ratings). [[ai-as-a-judge]] — prefer comparative over absolute scoring.

## Model Selection (Chapter 4)

Public benchmarks are **contaminated** (data likely in training) and **generic** (not your use case). Model selection = creating a **private leaderboard**:
1. Define evaluation criteria
2. Test models on your actual tasks
3. Rank by your specific metrics

Public leaderboards are useful starting signals, not final answers.

## Build vs Buy (Chapter 4)

| Factor | Model API (Buy) | Self-Host (Build) |
|--------|----------------|-------------------|
| Data Privacy | Leaves infrastructure | Stays local |
| Performance | Managed, frontier access | Custom optimization |
| Control | Limited | Full |
| Cost | Pay-per-use | GPU infrastructure |
| Expertise | None needed | ML team required |

7 axes: data privacy, data lineage, performance, functionality, control, cost, safety/compliance.

## Why It Matters

Working with AI models requires building workflows around their **probabilistic nature**. Without evaluation:
- Hallucinations go undetected
- Model changes silently degrade performance
- No way to detect regressions from prompt or model updates

## Related Pages

- [[functional-correctness]] — exact evaluation
- [[ai-as-a-judge]] — subjective evaluation with AI judges
- [[private-model-selection]] — private leaderboard approach
- [[build-vs-buy-ai]] — hosting vs API decision framework
- [[rlhf]] — post-training alignment
- [[context-reliability]] — token management
