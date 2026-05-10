---
title: "How to Get to Production Faster with Claude Managed Agents"
source: "https://www.youtube.com/live/GMIWm5y90xA"
author:
  - "Jess Yan (Anthropic)"
  - "Lance Martin (Anthropic)"
published: 2026-05-06
created: 2026-05-06
description: "Code with Claude 2026 — Session 2: Scaling agentic infrastructure, observability, Claude Managed Agents platform. Session 1 was the opening keynote on Advisory Strategy."
tags:
  - "clippings"
  - "anthropic-event"
  - "claude-managed-agents"
---

# How to Get to Production Faster with Claude Managed Agents

**Speakers**: Jess Yan (Member of Technical Staff) & Lance Martin (Member of Technical Staff), Anthropic
**Event**: Code with Claude 2026
**Date**: May 6, 2026
**Watch**: https://www.youtube.com/live/GMIWm5y90xA

---

## 1. The Problem: Agents in Production are Hard

### The Task Horizon is Expanding

Models have evolved from Opus 3 → Opus 4 → Opus 4.7, and with them the "Task Horizon" — how long an agent runs and how complex the task is.

| Model | Task Horizon | Example Task |
|-------|-------------|--------------|
| Opus 3 | Seconds | Write & test a single component |
| Opus 4 | Minutes/Hours | Debug a flaky test suite |
| Opus 4.7 | Days | Resolve a full Linear backlog overnight |
| Future (2026+) | Weeks+ | Run full M&A pipeline end-to-end |

As agents work on longer task horizons, they require:
- Much more autonomy
- Secure access to internal systems, proprietary code, identity/auth credentials
- State management, persistent memory, sophisticated tool-calling logic

### Developer Pain Points (New Research from Anthropic)

- **1 in 3** developers struggle with memory and context management
- **50%** of companies cite infrastructure concerns as their #1 production blocker
- **54%** of agents are running with **no formal observability** (running blind)

### The 80/20 Problem

> "Most developers today are spending **80% of their time building the plumbing** — the message loops, the error handling for tool failures, the state storage — and only **20% on the actual logic** of the task."

---

## 2. The Solution: Claude Managed Agents

A foundational infrastructure designed to scale with work complexity so developers don't have to build the scaffolding from scratch.

### Three Pillars

| Pillar | What It Provides |
|--------|-----------------|
| **Infrastructure & Harness** | Built-in sandboxing, credential proxies, asynchronous tool execution, permission policies, automatic retries/error recovery |
| **Developer Primitives** | Composable building blocks: define an agent, configure an environment (network allowlists, preinstalled packages), run a session, handle events |
| **Observability** | Deep session tracing, "Ask Claude in Console" feature to debug agent runs |

### The Architecture

```
Input → Objective Handler → Tool Registry → State Store → Output
```

**Tool Registry**: You provide OpenAPI specs or function definitions. Managed Agents handle authentication and retry logic if an API is flaky.

**State Store**: Built-in working memory. If a task takes 100 turns, the managed environment tracks what's been done and what's left — no need to pass full context back and forth.

**Safety Guardrails**: Constitutional AI checkpoints integrated directly into the agentic loop. Before a tool is called, the managed environment checks intent against your defined security policies.

### Getting Started Advice

> "Don't try to build a 'generalist' agent. Build a 'specialist.' Give it a narrow set of high-quality tools. Start with a task horizon of maybe an hour, and as you gain confidence in the guardrails, expand from there."

---

## 3. Event Topology — Standardized Observability

The event taxonomy for agent observability, standardized into **four categories**:

| Category | What It Captures |
|----------|-----------------|
| **User events** | Messages, interrupts, outcome definitions |
| **Agent events** | Messages, context compaction, tool use, multi-agent coordination |
| **Session events** | Status transitions, errors |
| **Span events** | Model request wrapping, outcome evaluations |

---

## 4. Live Demo 1: Data Analytics Agent "Pascal"

**Scenario**: Analyze a massive CSV dataset from a grocery chain ("Just In Thyme")

**What Pascal does**:
- Spins up a sandboxed Python environment in Claude Console
- Extracts and analyzes the data autonomously
- Runs clustering algorithms and predictive models
- Generates an interactive "Data Report" UI

**Key Findings from the data**:
- **"The Unstoppable Banana"**: Bananas carry an **85.7% reorder rate**
- **"Sunday Morning is Peak Grocery Time"**: Heatmap visualization of order volumes
- **Reorder Probability Simulator**: Interactive slider predicting reorder likelihood by customer profile

**Debugging**: Developers can jump into Claude Console, view the exact event trace of Pascal's run, and use "Ask Claude" to automatically analyze performance bottlenecks and fix script errors.

---

## 5. New Features: Just Released

Four highly anticipated features moving into Public Beta and Research Preview:

| Feature | Status | What It Does |
|---------|--------|--------------|
| **Multiagent Orchestration** | Public Beta | Claude delegates sub-tasks to specialized agents with independent context windows |
| **Outcomes** | Public Beta | Claude autonomously iterates in a loop until pre-defined exit criteria are satisfied |
| **Memory** | Public Beta | Claude reads and writes to persistent memory stores — every session gets progressively smarter |
| **Dreaming** | Research Preview | Claude reflects on past sessions and codifies learnings into foundational memories while "asleep" |

---

## 6. Live Demo 2: The "Boss Agent" — Inner + Outer Loops

An internal AI assistant that answers company-wide questions ("What are our topline metrics?", "Show me Q2 initiatives")

### Architecture

**The Inner Loop**:
1. Agent proposes a UI build
2. Runs Headless Chromium in a Sandbox
3. Executes JQuery
4. Takes a screenshot
5. Feeds outcome back to itself to verify correctness

**The Outer Loop**:
- User (or Claude CLI) provides updated instructions to steer the agent

### Performance Optimization

By using **Multiagent Orchestration** (delegating UI components to sub-agents) + **Prompt Optimization** + **"Fast Mode"**:

| Metric | Before | After |
|--------|--------|-------|
| Per-turn latency for rendering a complex chart | 37 seconds | **10 seconds** |

---

## 7. Industry Adoption

- **Asana's CTO**: Noted it drastically accelerated development of "Asana AI Teammates"
- **Notion's PM**: Highlighted how Managed Agents handle long-running sessions and memory to generate slides and spreadsheets directly inside Notion

---

## Key Takeaways for the Wiki

1. **Claude Managed Agents** = managed infrastructure for agents (sandboxing, state, retries, observability) — vs building it yourself
2. **State Store** = built-in working memory across turns
3. **Multiagent Orchestration** = delegation to sub-agents with independent context windows
4. **Outcomes** = autonomous iteration until exit criteria met
5. **Dreaming** = async reflection on past sessions, updating foundational memories
6. **Event Topology** = standardized 4-category taxonomy for agent observability
7. **"Don't build a generalist agent, build a specialist"** — start narrow, expand as trust grows