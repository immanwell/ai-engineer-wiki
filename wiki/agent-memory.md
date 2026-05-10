---
title: "Agent Memory Systems"
aliases:
  - "agent memory"
  - "reflection"
  - "memory management"
tags:
  - wiki
  - "agentic-architecture"
domain: "agentic-architecture"
sources:
  - "AI Engineer Chapter 6 (Chip Huyen, 2025).md"
status: stub
confidence: high
---

Created: Sunday, 10 May 2026, 17:25
Modified: `=dateformat(this.file.mtime, "DDDD, HH:mm")`

---

# Agent Memory Systems

**Summary**: Agents accumulate information that exceeds context windows — a memory system is required to manage and retrieve all of it. Effective agents use reflection and memory to track progress, learn from past actions, and stay coherent across long interactions.

**Sources**: [[raw/AI Engineer Chapter 6 (Chip Huyen, 2025).md|AI Engineering Chapter 6]]

---

## Why Agents Need Memory

Both RAG and agents deal with information that exceeds the model's context length. But while RAG solves this for retrieval, agents face a more complex problem:

- Agents take **multiple steps** over extended periods
- Each step builds on prior steps
- The model must remember: what was attempted, what worked, what's left to do

Without memory, an agent re-reads the entire conversation history on every turn — wasting context and potentially losing coherence.

## Memory System Components

### 1. Working Memory
Short-term — the current conversation context. What the model can "see" right now.

### 2. Episodic Memory
What happened in past sessions — prior interactions, patterns of failures, learned preferences.

### 3. Semantic Memory
Background knowledge the agent has built up — general facts, domain knowledge, previously learned patterns.

## Reflection

Reflection is the agent's ability to **review its own past actions** and learn from them.

From the Claude 2026 keynote, "Dreaming" is a form of asynchronous reflection — agents review past sessions, surface patterns, and update their memories even when not actively running.

**How reflection improves agents:**
- Recognize recurring failure patterns → avoid repeating them
- Identify successful strategies → apply them more often
- Build a cumulative model of the user's preferences

## Progress Tracking

Agents need to track:
- What step they're on in a multi-step task
- What's been completed vs. what's pending
- What intermediate results were produced

Without explicit progress tracking, agents lose their place in long workflows — especially problematic when tasks span multiple sessions.

## Security Implications

More automation = more catastrophic failures (from Ch6):

> "The more automated the agent becomes, the more catastrophic its failures."

Memory systems compound this — if an agent learns something incorrect and persists it, every subsequent interaction compounds the error. This means:

- Memory must be validated before being used
- Agents need the ability to "unlearn" or override bad memory
- Read-only memories (immutable past sessions) may be safer than writable ones

## The Agentic Loop with Memory

```txt
Task → Plan (with memory of similar past tasks) → Act → Reflect → Update Memory → Loop
```

The key distinction from simple tool use: the agent **learns** across interactions, not just within a single session.

## Related Pages

- [[agentic-architecture]] — the agentic loop and tool use patterns
- [[context-reliability]] — token management and context optimization
- [[advisory-strategy]] — memory shared between Executor and Advisor
- [[prompt-attacks]] — security risks of tools and agents (Ch5)
- [[ai-tutor]] — memory applied to student session continuity