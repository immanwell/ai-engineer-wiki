---
title: "RLHF"
aliases:
  - "Reinforcement Learning from Human Feedback"
  - "post-training"
  - "preference finetuning"
tags:
  - wiki
  - "context-reliability"
domain: "context-reliability"
sources:
  - "AI Engineer Chapter 2 (Chip Huyen, 2025).md"
status: stub
confidence: high
---

Created: Wednesday, 29 April 2026, 13:12
Modified: `=dateformat(this.file.mtime, "DDDD, HH:mm")`

---

# RLHF — Reinforcement Learning from Human Feedback

**Summary**: RLHF (Reinforcement Learning from Human Feedback) is a post-training technique that aligns model outputs with human preferences. It follows SFT (Supervised Finetuning) and is part of why AI assistants like Claude behave helpfully and safely.

**Sources**: [[raw/AI Engineer Chapter 2 (Chip Huyen, 2025).md|AI Engineering Chapter 2]]

---

## What It Is

RLHF is the second step in post-training (after SFT). It addresses the problem that:
- Pre-training uses self-supervision — models learn patterns but not *what humans want*
- SFT teaches the model to produce helpful responses, but the model still doesn't fully understand human preference

Human preference is diverse and impossible to capture in a single mathematical formula, so existing solutions are far from foolproof.

## The Training Workflow

```
Pre-training → SFT (Supervised Finetuning) → RLHF (Preference Finetuning)
```

### Pre-training
Self-supervised on large corpus — learns language patterns, facts, reasoning

### SFT (Supervised Finetuning)
Model trained on curated demonstrations of good responses

### RLHF
1. Collect human preference data (pairs of responses ranked)
2. Train a reward model to predict which response humans prefer
3. Use the reward model to finetune the base model via RL

## Why It Matters

- RLHF is why AI assistants follow instructions, admit mistakes, and refuse harmful requests
- Without RLHF, models optimize for "next token prediction" — not "being helpful"
- RLHF is imperfect — human preference is diverse and hard to capture completely

## Hallucinations and RLHF

One limitation: RLHF doesn't fully solve hallucinations. The model's probabilistic nature (from sampling) means it can still produce plausible but incorrect outputs even after alignment.

## Related Pages

- [[foundation-model-evaluation]]
- [[context-reliability]]
- [[scaling-laws]]
