---
title: "Functional Correctness"
aliases:
  - "exact evaluation"
  - "functional evaluation"
tags:
  - wiki
  - "context-reliability"
domain: "context-reliability"
sources:
  - "AI Engineer Chapter 3 (Chip Huyen, 2025).md"
  - "AI Engineer Chapter 4 (Chip Huyen, 2025).md"
status: stub
confidence: high
---

Created: Monday, 4 May 2026, 14:30
Modified: `=dateformat(this.file.mtime, "DDDD, HH:mm")`

---

# Functional Correctness

**Summary**: Exact evaluation — binary pass/fail on whether an AI system produces the correct output or behavior. The simplest evaluation approach, contrasted with subjective AI-as-a-judge evaluation.

**Sources**: [[raw/AI Engineer Chapter 3 (Chip Huyen, 2025).md|AI Engineering Chapter 3]] · [[raw/AI Engineer Chapter 4 (Chip Huyen, 2025).md|AI Engineering Chapter 4]]

---

## What It Is

Functional correctness is exact evaluation — does the system do what it was supposed to do? Binary pass/fail.

Examples:
- Code compilation: does it run without errors?
- Unit tests: do all assertions pass?
- Math problems: is the answer correct?
- Factual retrieval: does the answer match the known fact?

## Why It Matters

- Simplest evaluation approach — clear pass/fail
- Easy to automate
- Complements subjective evaluation: AI-as-a-judge needs to be validated against functional metrics

## Limitations

Not all tasks have a single correct answer. Open-ended tasks — essay quality, conversational appropriateness, creative writing — cannot be evaluated functionally.

For those, you need:
- [[ai-as-a-judge]] — subjective evaluation with AI judges
- Human evaluation — humans in the loop

## Related Pages

- [[ai-as-a-judge]]
- [[foundation-model-evaluation]]
