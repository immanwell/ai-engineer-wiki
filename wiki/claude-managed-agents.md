---
title: "Claude Managed Agents"
aliases:
  - "managed agents"
  - "claude platform infrastructure"
tags:
  - wiki
  - "agentic-architecture"
domain: "agentic-architecture"
sources:
  - "How to Get to Production Faster with Claude Managed Agents.md"
status: stub
confidence: high
---

Created: Sunday, 10 May 2026, 17:42
Modified: `=dateformat(this.file.mtime, "DDDD, HH:mm")`

---

# Claude Managed Agents

**Summary**: Managed infrastructure for agentic workflows — handles sandboxing, state management, retries, credential proxies, and observability so developers focus on task logic instead of building plumbing. Built around three pillars: Infrastructure & Harness, Developer Primitives, and Observability.

**Sources**: [[raw/How to Get to Production Faster with Claude Managed Agents.md|Code with Claude 2026 — Managed Agents Session]]

---

## The Problem: 80% Plumbing

> "Most developers today are spending **80% of their time building the plumbing** — the message loops, the error handling for tool failures, the state storage — and only **20% on the actual logic** of the task."

Agentic workflows in production require:
- State management across long task horizons
- Persistent memory
- Sophisticated tool-calling logic
- Security and credential handling
- Observability

Most developers build this scaffolding from scratch for every agent.

## The Solution: Three Pillars

### 1. Infrastructure & Harness

| Capability | What It Provides |
|------------|-----------------|
| **Sandboxing** | Isolated execution environments |
| **Credential proxies** | Secure access without embedding secrets |
| **Asynchronous tool execution** | Non-blocking tool calls |
| **Permission policies** | Fine-grained access control |
| **Automatic retries** | Resilient to transient failures |
| **Error recovery** | Built-in error handling |

### 2. Developer Primitives

Composable building blocks:
1. Define an agent (its tools and objectives)
2. Configure an environment (network allowlists, preinstalled packages)
3. Run a session
4. Handle events

You define **what** the agent does; the platform handles **how** it runs reliably.

### 3. Observability

- **Deep session tracing** — every step of the agent's reasoning visible
- **"Ask Claude in Console"** — debug agent runs by asking Claude to analyze performance bottlenecks

## The Architecture

```txt
Input → Objective Handler → Tool Registry → State Store → Output
```

### Tool Registry

You provide OpenAPI specs or function definitions. The managed environment handles:
- Authentication
- Retry logic if an API is flaky

### State Store

The agent's **built-in working memory**. If a task takes 100 turns:

> "You don't need to pass that full context back and forth yourself; the managed environment keeps track of what's been done and what's left to do."

This is the managed version of what `agent-memory.md` describes as working memory — but built in, not DIY.

### Safety Guardrails

Constitutional AI checkpoints integrated directly into the agentic loop. Before any tool is called, the managed environment validates intent against your security policies.

## Event Topology

Standardized **4-category observability taxonomy**:

| Category | What It Captures |
|----------|-----------------|
| **User events** | Messages, interrupts, outcome definitions |
| **Agent events** | Messages, context compaction, tool use, multi-agent coordination |
| **Session events** | Status transitions, errors |
| **Span events** | Model request wrapping, outcome evaluations |

This gives every agent a consistent way to expose what it's doing — making debugging and monitoring consistent across agents.

## New Features (Public Beta & Research Preview)

| Feature | Status | What It Does |
|---------|--------|--------------|
| **Multiagent Orchestration** | Public Beta | Claude delegates sub-tasks to specialized agents with independent context windows |
| **Outcomes** | Public Beta | Claude autonomously iterates until pre-defined exit criteria are satisfied |
| **Memory** | Public Beta | Claude reads/writes to persistent memory — every session gets progressively smarter |
| **Dreaming** | Research Preview | Claude reflects on past sessions and codifies learnings into foundational memories while idle |

## Industry Adoption

- **Asana**: Drastically accelerated development of "Asana AI Teammates"
- **Notion**: Generates slides and spreadsheets directly inside Notion via long-running sessions and memory

## Key Advice: Build Specialists

> "Don't try to build a 'generalist' agent. Build a 'specialist.' Give it a narrow set of high-quality tools. Start with a task horizon of maybe an hour, and as you gain confidence in the guardrails, expand from there."

## Exam Relevance

- [[agentic-architecture]] — broader agentic patterns and loops
- [[agent-memory]] — State Store as managed working memory
- [[advisory-strategy]] — Multiagent Orchestration vs Executor+Advisor are distinct patterns

## Related Pages

- [[agentic-architecture]] — general agentic patterns
- [[agent-memory]] — memory systems for agents
- [[advisory-strategy]] — Executor+Advisor pattern (distinct from Multiagent Orchestration)
- [[ai-tutor]] — potential use case: managed agents for persistent tutoring sessions