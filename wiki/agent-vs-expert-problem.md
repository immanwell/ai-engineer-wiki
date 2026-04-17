---
title: "Agent vs Expert Problem"
aliases:
  - agent-expert-gap
  - intelligence-vs-expertise
tags:
  - wiki
  - agentic-architecture
domain: certification
sources:
  - "anthropic-agents-to-skills.md"
status: stable
confidence: medium
---
Created: Friday, 16 April 2026, 21:19
Modified: `=dateformat(this.file.mtime, "DDDD, HH:mm")`

---
# Agent vs Expert Problem

**Summary**: The observation that AI agents have intelligence and general capabilities but lack the domain expertise and accumulated context needed for specialized work — a gap that skills architectures aim to fill.

**Sources**: [[raw/anthropic-agents-to-skills.md|anthropic agents to skills]]

---

## The Problem

After launching Claude Code and observing real customer usage, Anthropic identified a critical gap in current agent systems:

> "Who do you want doing your taxes? Is it going to be Mahesh, the 300 IQ mathematical genius, or is it Barry, an experienced tax professional?" — Barry Zhang

**Agents today are brilliant but miss important context upfront and don't learn over time.** They have intelligence and general capabilities, but lack the domain expertise needed for real specialized work.

This contrasts with [[skills-anthropic|skills]] which package domain expertise that agents can acquire.

## Why Intelligence Isn't Enough

| Attribute | Agents (current) | Experts |
|-----------|-----------------|---------|
| Intelligence | High | Variable |
| Domain knowledge | Generic/minimal | Deep and specific |
| Context awareness | Limited by context window | Accumulates over time |
| Learning | Static (no persistence) | Compounds with use |
| Entry context | Starts fresh | Knows team workflows |

An agent with high IQ but no tax knowledge will make different mistakes than an experienced tax professional — and those mistakes may be subtler and harder to catch.

## The Skills Solution

The [[skills-anthropic|Anthropic skills architecture]] addresses this by:
1. Packaging domain expertise into **skills** that agents can read when needed
2. Using **progressive disclosure** to keep context window efficient
3. Enabling skills to **accumulate organizational knowledge** over time

## Relationship to Agentic Architecture

This problem is core to [[agentic-architecture|agentic architecture]] questions:
- How do agents acquire domain expertise?
- How do you prevent agents from "starting fresh" every session?
- What makes an agent genuinely useful vs. theoretically capable?

## Related Pages

- [[skills-anthropic]] — Anthropic's skills architecture solution
- [[agentic-architecture]] — Foundational agent concepts
- [[context-reliability]] — Managing context in agent systems