---
title: "AI as a Judge"
aliases:
  - "AI judge evaluation"
  - "subjective evaluation"
tags:
  - wiki
  - "context-reliability"
domain: "context-reliability"
sources:
  - "AI Engineer Chapter 3 (Chip Huyen, 2025).md"
status: stub
confidence: high
---

Created: Monday, 4 May 2026, 14:30
Modified: `=dateformat(this.file.mtime, "DDDD, HH:mm")`

---

# AI as a Judge

**Summary**: Using an AI model to subjectively evaluate the quality of another AI's output. Scores are judge-dependent and context-specific — scores from different judges are not directly comparable. Must be supplemented with exact evaluation and human evaluation.

**Sources**: [[raw/AI Engineer Chapter 3 (Chip Huyen, 2025).md|AI Engineering Chapter 3]]

---

## What It Is

AI-as-a-judge uses a model to evaluate the quality of another model's output. The judge scores responses based on criteria like helpfulness, coherence, factual accuracy, or tone.

Example: A judge rates two responses to "Explain photosynthesis" on clarity, completeness, and accuracy.

## The Problem with It

Unlike [[functional-correctness]], AI-as-a-judge is **subjective and judge-dependent**:

- Scores must be interpreted in the context of which judge was used
- Scores from different AI judges measuring the "same quality" may not be comparable
- AI judges should be iterated upon — their judgments change as they evolve
- **Not reliable as benchmarks** to track an application's changes over time

## Best Practices

- Always supplement AI-as-a-judge with:
  - Exact evaluation ([[functional-correctness]])
  - Human evaluation (humans in the loop)
- Use comparative evaluation where possible (which response is better?) rather than absolute scores
- Prefer [[preference-models]] — specialized judges trained to predict which response users prefer

## Comparative Evaluation

Rather than scoring in isolation, comparative evaluation asks: which of two models is better? Common in chess (Elo ratings) and gaining traction in AI evaluation. Requires preference signals — expensive to collect.

## Related Pages

- [[functional-correctness]]
- [[preference-models]]
- [[foundation-model-evaluation]]
