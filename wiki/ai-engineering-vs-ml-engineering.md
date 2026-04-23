---
title: "AI Engineering vs ML Engineering"
aliases:
  - "AI engineering vs machine learning engineering"
tags:
  - wiki
  - "agentic-architecture"
domain: "agentic-architecture"
sources:
  - "AI Engineer Chapter 1 (Chip Huyen, 2025).md"
status: stub
confidence: medium
---

Created: Thursday, 23 April 2026, 06:37
Modified: `=dateformat(this.file.mtime, "DDDD, HH:mm")`

---

# AI Engineering vs ML Engineering

**Summary**: AI engineering evolved from ML engineering but differs in key ways: the model is a composed component (not trained from scratch), probabilistic outputs require systematic evaluation, and human-AI interaction is part of the product.

**Sources**: [[raw/AI Engineer Chapter 1 (Chip Huyen, 2025).md|AI Engineering Chapter 1]]

---

## What's the Same

Many principles from ML engineering still apply to AI engineering — data quality, evaluation, monitoring, etc.

## What's Different

### The Model as Component
In ML engineering, you often train the model. In AI engineering, you **compose with foundation models** — you don't train them, you build applications on top of them.

### Probabilistic Outputs Require Systematic Evaluation
Traditional ML models have deterministic-ish outputs. Foundation models are probabilistic — ChatGPT and Gemini are "fun to talk to" partly because of this, but it also causes hallucinations and inconsistency. **Systematic evaluation pipelines are non-negotiable.**

### Human-AI Interaction Is Part of the Product
In ML engineering, the model is often hidden behind a traditional interface. In AI engineering, the conversational interface means **human-AI interaction is designed into the product**, not bolted on.

### The Pace of Change
ML engineering was relatively stable. AI engineering is moving at extraordinary speed — new techniques, discoveries, and engineering feats happen constantly. This makes frameworks more important than any specific tool.

## Practical Implications

- You need **evaluation pipelines before you need prompt tricks**
- You need **judgment about when to build vs buy** (use a model API vs host your own)
- You need **architecture thinking** — RAG, agents, finetuning are all composition choices

## Exam Relevance

- [[agentic-architecture]] — composition patterns
- [[context-reliability]] — evaluation and reliability as core concerns

## Related Pages

- [[ai-engineering-discipline]]
- [[ai-engineering-ch1]]
