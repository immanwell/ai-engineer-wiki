---
title: "Evaluation-Driven Development"
aliases:
  - "EDD"
  - "evaluation first"
  - "build with evaluation"
tags:
  - wiki
  - "context-reliability"
domain: "context-reliability"
sources:
  - "AI Engineer Chapter 4 (Chip Huyen, 2025).md"
  - "Chip Huyen’s Evaluation-Driven Development (EDD) framework from AI Engineering.md"
status: stub
confidence: high
---

Created: Tuesday, 5 May 2026, 00:12
Modified: `=dateformat(this.file.mtime, "DDDD, HH:mm")`

---

# Evaluation-Driven Development

**Summary**: EDD is a framework where evaluation definitions lead the entire AI development lifecycle — model selection, design, deployment, and iteration all follow from what "good" means for your specific use case. TDD for AI.

**Sources**: [[raw/AI Engineer Chapter 4 (Chip Huyen, 2025).md|AI Engineering Chapter 4]] · [[raw/Chip Huyen’s Evaluation-Driven Development (EDD) framework from AI Engineering.md|Evaluation-Driven Development (EDD) Framework — Medium]]

---

## The Core Idea

Traditional software defines success upfront: does it return the correct value? Meet the latency budget? Scale?

AI systems are **probabilistic, not deterministic** — the same input produces different outputs. EDD flips the approach: define what "good" looks like *first*, then let those definitions guide everything else.

This is analogous to TDD (Test-Driven Development), but for AI:
- **TDD**: Write tests → write code → refactor
- **EDD**: Define evaluation criteria → select models → build → monitor

## The Four Evaluation Pillars

Chip Huyen outlines four dimensions for meaningful AI evaluation:

| Pillar | What It Measures |
|--------|-----------------|
| **Domain-Specific Capability** | How well the AI handles tasks in your specific domain |
| **Generation Quality** | Coherence, relevance, factuality, fluency of outputs |
| **Instruction-Following** | How precisely the model follows prompts and user instructions |
| **Latency & Cost Trade-offs** | Performance vs. computational cost — important for production |

### Domain-Specific Capability

The model must be smart **where it matters for your use case**. A medical scan reviewer needs different capabilities than a code assistant.

Example: A UG mathematics tutor needs to handle NCDC curriculum — not general reasoning benchmarks.

### Generation Quality

How well the model generates content. Key dimensions:
- **Coherence** — logically consistent?
- **Relevance** — stays on topic?
- **Factuality** — verifiable truths?
- **Fluency** — natural language?

### Instruction-Following

Can the model stick to the task? Generic LLMs often ignore formatting instructions, produce paragraphs instead of bullet points, or drop clauses.

### Latency & Cost Trade-offs

A 99% accurate model that costs 10x more and runs 10x slower may be worse than a 95% accurate one. Trade-offs must be evaluated in context.

## Model Selection Workflow

EDD applies evaluation to the model selection process itself:

1. **Initial Filtering** — Eliminate models by hard constraints (language support, licensing, hardware)
2. **Benchmarking** — Compare shortlisted models on existing benchmarks (MMLU, TruthfulQA, domain-specific)
3. **Hands-On Prototyping** — Test with *your actual data* — no benchmark simulates your users
4. **Continuous Monitoring** — Track drift, failure patterns, and edge cases in production

This is where [[private-model-selection]] fits — public benchmarks alone are insufficient; EDD demands testing on your actual use case.

## Building Evaluation Pipelines

EDD requires pipelines that are automated, interpretable, and maintainable.

### System-Level vs Component-Level

- **System-Level** — end-to-end: does the chatbot resolve the query?
- **Component-Level** — per component: is the NER tagging correctly? Is summarization preserving intent?

Both levels needed. You can't fix what you don't measure.

### Sampling Strategies

You can't test every output. Choose wisely:
- **Random sampling** — unbiased picture
- **Stratified sampling** — coverage of edge cases and priority segments
- **Error-focused sampling** — review worst-performing examples in detail

### Meta-Evaluation

Evaluate the evaluation itself:
- Are metrics measuring what matters?
- Are human annotators consistent?
- Are tests covering real-world complexity?

Example: High ROUGE scores but user complaints = ROUGE isn't capturing what matters.

## Relationship to Other Concepts

- [[foundation-model-evaluation]] — the umbrella topic; EDD is the framework
- [[functional-correctness]] — exact evaluation (one pillar of EDD)
- [[ai-as-a-judge]] — a specific evaluation method within EDD
- [[private-model-selection]] — EDD applied to model selection (Step 3: hands-on prototyping)
- [[build-vs-buy-ai]] — EDD's latency/cost pillar informs this decision

## Key Insight

> "Better is not generic — it's contextual. In every AI product, you must define what 'better' means for your users, your domain, and your values." — adapted from Chip Huyen

EDD brings structure to what would otherwise be trial-and-error. It makes AI systems not just technically competent, but **fit for purpose**.

## Related Pages

- [[foundation-model-evaluation]] — evaluation as first step in systematic AI engineering
- [[private-model-selection]] — private leaderboard approach driven by EDD principles
- [[functional-correctness]] — exact evaluation within EDD
- [[ai-as-a-judge]] — subjective evaluation within EDD
- [[build-vs-buy-ai]] — latency/cost trade-offs within EDD
