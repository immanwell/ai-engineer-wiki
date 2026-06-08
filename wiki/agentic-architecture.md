---
title: "Agentic Architecture"
aliases:
  - agentic
  - multi-agent
  - agentic-systems
tags:
  - wiki
  - agentic-architecture
domain: certification
sources:
  - "instructor-8lsy243ftffjjy1cx9lm3o2bw-public-1773274827-Claude+Certified+Architect+–+Foundations+Certification+Exam+Guide.pdf"
status: stable
confidence: high
---
Created: Friday, 15 April 2026, 22:32
Modified: `=dateformat(this.file.mtime, "DDDD, HH:mm")`

---
# Agentic Architecture

**Summary**: Designing systems where AI agents autonomously plan, reason, and execute tasks across multiple steps, often using structured outputs, nested requests, and multi-turn conversations to accomplish complex goals.

**Sources**: [[raw/instructor-8lsy243ftffjjy1cx9lm3o2bw-public-1773274827-Claude+Certified+Architect+–+Foundations+Certification+Exam+Guide.pdf|architect exam guide]]

---

## Overview

Agentic Architecture is the largest exam domain at **40%** (30 questions). It covers how to build systems where Claude acts as an autonomous agent — planning sequences of actions, using tools, handling multi-step workflows, and managing conversation context over long interactions.

## Core concepts

### The agentic loop

A agentic system typically follows this cycle:

1. **Receive** a task or message
2. **Plan** — break it into steps (Reasoning with chain-of-thought)
3. **Act** — call tools, make API calls, or generate responses
4. **Evaluate** — check if the goal is met
5. **Respond** or loop back to step 2

### Tool use patterns

- **Single tool calls** — one tool per response
- **Parallel tool calls** — multiple independent tools in one response (e.g., `tools parallel`)
- **Sequential tool calls** — tool results fed into next turn's context
- **Nested tool calls** — one tool's output triggers another tool call

### Claude Messages API

The API format that powers agentic systems:

```txt
[system, user, assistant(tool call), tool result, assistant(tool call), tool result, assistant(final)]
```

Each turn can include:
- `role`: system / user / assistant
- `content`: text, tool calls, or tool results
- `tool_calls`: structured tool invocations (id, name, input)
- `stop_reason`: for tracking tool use completion

### Structured outputs

When a tool call returns, the next assistant turn receives it as `tool_result` content — the agent continues reasoning from that context without any special wrapper needed.

### Two computers mental model (new)

| Computer | Use For |
|----------|---------|
| **Claude's sandbox** | Stateless compute, data analysis, installing libraries |
| **Your local bash** | Access to your repo, local Python env, local context |

Claude intelligently knows which to use. Sandbox for scratch pad work; local bash when it needs repo access.

### Parallelism

The API supports running multiple tool calls simultaneously. Results come back in the same order as the call array. If one fails, others still complete.

### Context management in agentic systems

- Each conversation has a maximum token limit (e.g., 200K for Claude Sonnet 4)
- Rolling context: keep recent turns, drop older ones
- System prompt provides persistent instructions across all turns
- Anthropic provides `cache_control` for long context optimization

## Multi-agent patterns

### Handoff patterns

One agent delegates to another — common in complex workflows:
- **Routing agent** — classifies the user's request and hands off to a specialized agent
- **Supervisor agent** — coordinates multiple sub-agents, aggregates results
- **Specialist agents** — each handles a specific domain (e.g., research, coding, review)

### Inter-agent communication

- Shared context windows (up to certain token budget)
- Sequential handoffs with accumulated history
- Hierarchical: supervisor → specialist → tool

## Reasoning and chain-of-thought

Claude's thinking mode (beta):
- `thinking.logs` — structured reasoning traces
- `thinking.type` — chain-of-thought, block, etc.
- Thinking content is not visible to the end user by default
- Can be suppressed with `thinking.type: "bypass"`

## Model-Level Improvements (Opus 4.7 Gains)

From the capability curve research (Code with Claude 2026, Session 5):

### Planning: Think First, Then Act

Older models acted first and thought later — like building IKEA furniture without reading instructions. Opus 4.7 takes time upfront to strategize, plan, and read before writing code. **Implication**: Give Claude time to think. Don't force it to jump straight into action.

### Error Recovery: No More Doom Loops

Older models would hit a problem → propose a solution → solution fails → spiral until context stalls out. Opus 4.7 backs out of dead ends, reads errors, and takes a different path. **Implication**: Better task performance with fewer wasted tokens — no more manual retry harnesses.

### Attention Over Long Runs

Older models lose coherence, forget system prompt instructions, and break down over long contexts. Opus 4.7 holds coherence across **1 million tokens**. **Implication**: No need to manually chunk work or babysit the context window — trust the model's sustained attention.

These three improvements connect to the capability curve: things that previously required scaffolding (retry loops, context chunking, manual planning) are now built into the model.

## Exam relevance

This domain is the most heavily tested. Expected to understand:
- When to use single vs. parallel tool calls
- How tool results become context for the next turn
- Token budget implications of long conversations
- Multi-agent routing and handoff patterns
- Structured output handling

## Related pages

- [[claude-certified-architect-foundations-exam-guide]] — exam overview
- [[tool-design-mcp]] — building tools that agents use
- [[claude-code]] — agentic coding with Claude Code
- [[context-reliability]] — managing context at scale
- [[prompt-engineering]] — instructing agents effectively
- [[ai-application-architecture]] — the production system view: how agents are deployed with gateways, guardrails, observability, and data flywheel