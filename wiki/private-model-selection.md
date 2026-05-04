---
title: "Private Model Selection"
aliases:
  - "model selection"
  - "private leaderboard"
  - "contaminated benchmarks"
tags:
  - wiki
  - "context-reliability"
domain: "context-reliability"
sources:
  - "AI Engineer Chapter 4 (Chip Huyen, 2025).md"
status: stub
confidence: high
---

Created: Monday, 4 May 2026, 14:30
Modified: `=dateformat(this.file.mtime, "DDDD, HH:mm")`

---

# Private Model Selection

**Summary**: Public benchmarks are contaminated and unreliable for finding the best model for your specific needs. Model selection should be treated as creating a private leaderboard — testing models against your actual use case, on your actual data.

**Sources**: [[raw/AI Engineer Chapter 4 (Chip Huyen, 2025).md|AI Engineering Chapter 4]]

---

## The Problem with Public Benchmarks

Public benchmarks have two critical flaws:

1. **Contaminated** — benchmark data is likely in the training data of many models, inflating scores
2. **Generic** — they measure broad capabilities, not your specific use case

Public benchmarks can help **weed out bad models** but won't help you find the **best model for your application**.

## The Solution: Private Leaderboard

Model selection = creating a private leaderboard for your needs:

1. Define your evaluation criteria (from [[foundation-model-evaluation]])
2. Test models on your actual tasks
3. Rank them by your specific metrics
4. Repeat as use cases evolve

## Public Leaderboards

Public leaderboards aggregate multiple benchmarks to rank models — but:
- How benchmarks are selected and aggregated is not transparent
- Rankings may not reflect your domain
- Still useful as a starting signal, not a final answer

## Key Insight

> "The lessons learned from public leaderboards are helpful for model selection, as model selection is akin to creating a private leaderboard to rank models based on your needs."

## Related Pages

- [[foundation-model-evaluation]]
- [[ai-as-a-judge]]
- [[build-vs-buy-ai]]
