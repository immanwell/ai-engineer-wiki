---
title: "Advisory Strategy"
aliases:
  - "executor advisor pattern"
  - "sonnet opus architecture"
tags:
  - wiki
  - "agentic-architecture"
domain: "agentic-architecture"
sources:
  - "Code with Claude 2026 Opening Keynote.md"
status: stub
confidence: high
---

Created: Wednesday, 6 May 2026, 21:41
Modified: `=dateformat(this.file.mtime, "DDDD, HH:mm")`

---

# Advisory Strategy

**Summary**: An agentic architecture pattern where a fast, cheap model (Executor) handles the main loop while a more capable model (Advisor) is called on-demand for complex decisions. Achieves frontier model quality at 5x lower cost.

**Sources**: [[raw/Code with Claude 2026 Opening Keynote.md|Code with Claude 2026 Opening Keynote]]

---

## The Core Problem It Solves

Running a large, expensive model (Opus) for every turn is too slow and costly. But using only small, fast models (Sonnet/Haiku) risks failures on complex tasks.

**Classic dilemma**: Fast + cheap = unreliable on hard tasks. Reliable on hard tasks = slow + expensive.

The Advisory Strategy breaks this tradeoff.

## How It Works

```
┌─────────────────────────────────────────────────────────┐
│                      SHARED CONTEXT                      │
│  (conversation history, tool results, session state)    │
└─────────────────────────────────────────────────────────┘
           ↑                                    ↓
           │  strategic advice          on-demand tool call
           │                                    │
    ┌──────────────┐                    ┌──────────────┐
    │  ADVISOR     │                    │   EXECUTOR   │
    │  (Opus 4.7)  │                    │ (Sonnet 4.6) │
    │              │                    │              │
    │  Large, slow │                    │ Fast, cheap  │
    │  high reasoning                    │ every turn  │
    │  called on-demand                   │             │
    └──────────────┘                    └──────────────┘
           ↑                                    ↓
           │                              executes actions
           │                              writes to shared context
```

**Executor (Sonnet 4.6)**:
- Handles every turn rapidly
- Reads and writes to shared context
- Drives the main agentic loop
- When it hits complexity → calls Advisor

**Advisor (Opus 4.7)**:
- Sits in background, not called every turn
- Receives the full shared context when called
- Returns strategic advice to the Executor
- Uses its full reasoning capability only when needed

**Trigger conditions for Advisor call**:
- Executor encounters ambiguous instruction
- Task requires deep multi-step reasoning
- Executor gets stuck or uncertain
- High-stakes decision needed

## Performance Results

Anthropic shared internal benchmarks:

| Configuration | Accuracy | Cost per Run |
|---------------|----------|--------------|
| Opus 4.7 alone | 59.6% | $0.94 |
| Sonnet 4.6 + Opus 4.7 (Advisory) | **63.4%** | **$0.88** |

Both better accuracy **and** lower cost. The Advisory Strategy doesn't just save money — it actually improves outcomes.

**Why?** The Executor moves fast and doesn't get stuck in over-thinking. The Advisor only steps in when it adds genuine value.

## The "Dreaming" Variant

A related capability introduced at the same keynote: agents can asynchronously review past sessions, surface patterns, and automatically update their memories to improve future performance — even when not actively running.

This lets agents learn from experience across sessions without human intervention.

## Relationship to Freemium Architecture

The Advisory Strategy maps directly to freemium product tiers:

| Tier | Executor | Advisor | Use Case |
|------|----------|---------|----------|
| Free | Sonnet (every turn) | — | Routine queries, simple tasks |
| Paid | Sonnet (every turn) | Opus (on-demand) | Complex edge cases, ambiguous inputs |

**The Advisor is only invoked when the Executor signals it needs help** — this keeps costs manageable while delivering high quality on hard tasks.

For consumer AI products, this is a natural freemium pattern:
- Free users get fast, cheap responses for most queries
- Paid users get the Advisor for complex tasks — barely noticeable additional cost at scale

## Exam Relevance

- [[agentic-architecture]] — multi-agent patterns, tool use, shared context
- [[context-reliability]] — managing shared context across agent handoffs

## Related Pages

- [[agentic-architecture]] — broader multi-agent patterns
- [[ai-native-engineer]] — building reliable agentic workflows incrementally
- [[context-reliability]] — shared context management
- [[ai-tutor]] — freemium architecture for the AI Tutor product
- [[build-vs-buy-ai]] — cost considerations for API vs self-host