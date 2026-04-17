---
title: "Agent Orchestration Patterns"
aliases:
  - agent-orchestrator
  - multi-agent-coordination
  - human-control-plane
tags:
  - wiki
  - agentic-architecture
domain: certification
sources:
  - "paperclip-agent-orchestrator.md"
status: stable
confidence: medium
---
Created: Friday, 16 April 2026, 23:11
Modified: `=dateformat(this.file.mtime, "DDDD, HH:mm")`

---
# Agent Orchestration Patterns

**Summary**: Patterns for coordinating multiple AI agents to complete complex tasks, including hierarchical delegation, human-in-the-loop oversight, and vendor-neutral workflow composition.

**Sources**: [[raw/paperclip-agent-orchestrator.md|paperclip agent orchestrator]]

---

## Overview

Agent orchestration patterns describe how multiple AI agents are coordinated to accomplish tasks beyond a single agent's capability or scope. These patterns address delegation, quality assurance, and maintaining human accountability throughout execution.

See [[agentic-architecture]] for the foundational agentic loop concepts.

## Key Patterns

### Hierarchical Delegation (Org Chart Pattern)

Agents are structured like a corporate hierarchy:

1. **CEO agent** — top-level orchestrator that receives tasks and delegates
2. **Executive agents** (CTO, CMO, etc.) — domain-specific coordinators
3. **Individual contributor agents** — specialized workers (coders, writers, analysts)

The CEO agent knows how to hire new agents and install new skills — it can grow the team dynamically. Higher-level agents delegate; lower-level agents execute and report back.

**Contrast with flat multi-agent systems**: Rather than all agents being equal peers, the hierarchy provides clear ownership, accountability, and natural task routing.

**Paperclip example**: The creator ("dotta") created an issue for a Remotion video, assigned it to the CEO agent, which then hired a video writer and installed the Remotion best practices skill. The CEO coordinated without the human needing to manage individual contributors directly.

### Human Control Plane

The human remains involved from higher-level design through execution, ensuring taste and accountability are built into workflows. This is not "set and forget" autonomy — the human sets standards, reviews outputs, and maintains accountability.

Key characteristics:
- Human approves major decisions (e.g., hiring new agents)
- Human sets preferences that agents encode as organizational skills
- Human reviews outputs at quality gates

**Paperclip phrase**: "human control plane for AI labor" — the human is the ultimate accountable party.

### QA Review Gates

Before work completes, a dedicated QA agent verifies the output by:
- Opening websites, filling forms, clicking buttons (using [[tool-design-mcp|agent browser skill]])
- Checking against defined acceptance criteria
- Returning work for revision if it fails

This creates a workflow that is **vendor-neutral** — unlike [[claude-code|Claude Code hooks]] which work differently across IDEs (Claude Code, Cursor, etc.), orchestration workflows abstract away the IDE-specific tooling.

### Routines (Reusable Task Templates)

Routines are parameterized, reusable workflows that can be:
- **Scheduled** — run on a cron-like schedule
- **Manual** — triggered on demand
- **Event-driven** — triggered by external events (e.g., PR merged to master)

Template variables allow dynamic inputs (e.g., branch names passed at execution time).

### Skills Auto-Discovery

Agents can dynamically discover and install new capabilities at runtime. Integration with systems like skills.sh allows agents to locate and add skills without manual configuration.

**Paperclip example**: "install the Remotion best practices skill" — the CEO agent found and installed the skill automatically.

## Spend Management

Multi-agent systems can track costs per agent and per project, supporting:
- Monthly spend budgets
- Subscription-based usage
- Pay-per-inference models

This enables cost governance at the organizational level — not just individual API calls.

## Model Selection at Each Layer

Not every agent needs frontier model pricing. Using router systems (e.g., OpenRouter), lower-stakes agents can use cheaper models (e.g., Qwen 3.6 Plus) while reserving Claude or GPT for higher-stakes decisions.

## Relationship to Agentic Architecture

These orchestration patterns extend the core [[agentic-architecture|agentic loop]] concepts:

| Concept | Where it fits |
|---------|---------------|
| Hierarchical delegation | Multi-agent handoff patterns |
| Human control plane | Human-in-the-loop design |
| QA review gates | Tool use quality patterns |
| Routines | Structured output and workflow composition |
| Skills auto-discovery | [[tool-design-mcp]] integration |

## Exam Relevance

The exam covers multi-agent handoffs and supervisor patterns. Understanding hierarchical orchestration helps with questions about:
- When to use a routing agent vs. supervisor pattern
- How to maintain accountability in multi-agent systems
- Token budget implications of agent delegation chains

## Related Pages

- [[agentic-architecture]] — foundational agentic loop and handoff patterns
- [[tool-design-mcp]] — building tools that agents use
- [[claude-code]] — Claude Code as an agentic coding tool
- [[context-reliability]] — managing context in multi-agent workflows
