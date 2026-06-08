---
title: "AI Application Architecture"
aliases:
  - "generative AI architecture"
  - "model gateway"
  - "guardrails"
  - "data flywheel"
  - "AI observability"
tags:
  - wiki
  - "agentic-architecture"
domain: "agentic-architecture"
sources:
  - "AI Engineer Chapter 10 (Chip Huyen, 2025).md"
status: stable
confidence: high
---

Created: Monday, 8 June 2026, 22:04
Modified: `=dateformat(this.file.mtime, "DDDD, HH:mm")`

---

# AI Application Architecture

**Summary**: A generative AI application is a system of components layered around a foundation model. Each component adds capability, safety, or speed — but also adds complexity and new failure modes. Understanding the full system is what separates engineers who ship reliable AI products from those who just call an API.

**Sources**: [[raw/AI Engineer Chapter 10 (Chip Huyen, 2025).md|AI Engineering Chapter 10]]

---

## The Common Architecture

Most production generative AI applications share a common high-level structure:

```txt
User
  ↓
Model Gateway        ← routing, auth, rate limiting, logging
  ↓
Context Construction ← RAG retrieval, memory injection, prompt assembly
  ↓
Guardrails (input)   ← safety checks, input validation, PII filtering
  ↓
Inference Service    ← model call + optimization (batching, caching, etc.)
  ↓
Guardrails (output)  ← output filtering, safety checks, formatting
  ↓
Response
  ↑
User Feedback        → analytics, data flywheel, model improvement
```

Each layer is optional but addresses a real failure mode. The architecture grows from "just call the API" to a full production system as you encounter each class of problem.

## The Components

### Model Gateway

A centralized layer in front of the model API. Handles:
- **Routing**: direct requests to the right model or provider
- **Authentication and rate limiting**: prevent abuse
- **Logging and tracing**: record all requests/responses for debugging
- **Cost attribution**: track token spend by team or feature

The gateway is often where prompt caching and A/B testing logic live.

### Context Construction

The step that assembles the full prompt before the model sees it. Involves:
- Fetching relevant documents via [[rag-retrieval|RAG]]
- Injecting [[agent-memory|memory]] from past sessions
- Filling in system prompt templates
- Applying conversation history management (see [[context-reliability]])

Context construction quality directly determines response quality — garbage in, garbage out.

### Guardrails

Safety and validation checks applied to inputs and/or outputs. Common functions:
- Block harmful or out-of-scope requests (input)
- Filter sensitive content from outputs (output)
- Enforce response format constraints
- Detect [[prompt-attacks|prompt injection]] attempts

**Key architectural note**: Guardrails have fluid placement. They can live in the inference service, the model gateway, or as a standalone component — or in all three simultaneously. The "right" placement depends on your threat model and latency budget.

### Inference Service

The layer that actually calls the model, with [[inference-optimization|optimization]] applied:
- Batching, caching, quantization
- Prompt caching for repeated prefixes
- Retry logic and fallback routing

### User Feedback Collection

The conversational interface enables richer feedback signals than traditional software:

| Feedback Type | Signal | Use |
|---------------|--------|-----|
| **Explicit** | Thumbs up/down, star rating | Direct quality signal |
| **Implicit** | Response copy, follow-up questions, session length | Engagement proxy |
| **Correction** | User edits or rewrites the AI's output | High-value training signal |
| **Abandonment** | User stops mid-conversation | Failure signal |

## Modularity with Fluid Boundaries

A key principle of AI application architecture: **components are separated for maintainability, but their boundaries are fluid.**

The same function can be implemented in multiple places:
- Guardrails: in the gateway, in the inference layer, standalone, or all three
- Context management: in the retriever, in the context constructor, or in the model gateway
- Logging: at every layer or centralized in one

This fluidity is intentional — it lets you deploy the simplest possible system first and add complexity only where needed. A single guardrail component is easier to audit than guardrail logic scattered across three layers.

## Complexity Tradeoffs

> Each additional component can make your system more capable, safer, or faster — but also increases complexity and exposes it to new failure modes.

The practical implication: **add components incrementally, as actual failure modes surface.** Don't pre-architect for hypothetical problems.

| Component Added | Capability Gained | Failure Mode Introduced |
|-----------------|-------------------|------------------------|
| RAG retrieval | Grounded, up-to-date answers | Retrieval failures, latency spikes |
| Memory injection | Personalized, stateful conversations | Memory staleness, privacy risks |
| Guardrails | Safety and compliance | False positives blocking valid requests |
| Model gateway | Routing and observability | Single point of failure |

## AI Observability

Foundation models introduce failure modes that don't exist in traditional software — observability must be redesigned accordingly.

### Traditional vs AI Failure Modes

| Traditional Software | AI Systems |
|---------------------|------------|
| Crashes, timeouts, error codes | Plausible but wrong outputs |
| Binary pass/fail | Probabilistic quality degradation |
| Deterministic behavior | Sensitive to prompt wording changes |
| Stack traces | No stack trace for "why did it say that?" |

### What to Monitor

- **Output quality metrics**: hallucination rate, task completion rate, user correction rate
- **Latency per phase**: TTFT and TPOT per model call (see [[inference-optimization]])
- **Feedback signals**: thumbs down rate, abandonment rate, correction rate
- **Cost**: token spend per feature, per user tier
- **Safety**: guardrail trigger rate, blocked request categories

### Designing for Traceability

Every request should be traceable from user input → context constructed → model called → output returned → user feedback received. Without this trace, debugging is guesswork.

## The Data Flywheel

The data flywheel is the compounding loop that makes user feedback an engineering responsibility:

```txt
Better model → better product → more users → more feedback → better training data → better model
```

This is why AI engineering is moving closer to product than traditional ML engineering. The feedback interface is not a product nicety — it is a **data collection mechanism** for continuous model improvement.

**Implication for engineers**: Feedback design decisions (what signals to collect, how to store them, how to filter noise) directly determine your future training data quality. Engineers must be involved.

## System-Level Thinking

> Many AI challenges are, at their core, system problems. A single problem might be addressed by different components working independently, or require the collaboration of multiple components.

The architectural view is what enables this thinking. Examples:
- Hallucination problem → addressable by RAG (better grounding), guardrails (output filtering), or evaluation (catching failures post-hoc)
- Latency problem → addressable by inference optimization, prompt caching, or context pruning
- Safety problem → addressable by guardrails, model finetuning, or prompt design

No single technique is the universal fix. The system view reveals which lever to pull for which problem.

## Exam Relevance

- [[agentic-architecture]] — this is the production system view of how agents are deployed
- [[context-reliability]] — context construction and management sits in this architecture
- [[tool-design-mcp]] — tools are called from within the inference layer
- [[prompt-engineering]] — prompts are assembled in the context construction layer

## Related Pages

- [[agentic-architecture]] — multi-agent patterns that this architecture hosts
- [[rag-retrieval]] — the retrieval component in context construction
- [[agent-memory]] — the memory component in context construction
- [[inference-optimization]] — what the inference service layer implements
- [[context-reliability]] — context management across the full architecture
- [[prompt-attacks]] — guardrails defend against these
- [[foundation-model-evaluation]] — evaluation metrics feed back into the data flywheel
- [[build-vs-buy-ai]] — the gateway and inference service are the main build-vs-buy decision points
