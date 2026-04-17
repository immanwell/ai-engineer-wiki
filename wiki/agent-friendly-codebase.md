---
title: "Agent-Friendly Codebase"
aliases:
  - "building codebases for AI agents"
  - "agentic codebase design"
tags:
  - wiki
  - "agentic-architecture"
  - "context-reliability"
domain: "agentic-architecture"
sources:
  - "mihail-eric-junior-engineers-crisis.md"
status: stub
confidence: medium
---

Created: Friday, 17 April 2026, 02:51
Modified: `=dateformat(this.file.mtime, "DDDD, HH:mm")`

---

# Agent-Friendly Codebase

**Summary**: Eric argues that agents operate on explicitly defined contracts (primarily tests), require consistent documentation, and amplify errors quickly when codebases are messy — making clean, well-tested, consistently styled code essential for reliable agentic systems.

**Sources**: [[raw/mihail-eric-junior-engineers-crisis.md|Mihail Eric Stanford talk]]

---

## Core Principles

### Tests as Contracts

Agents can only operate on explicitly defined contracts. **Tests define software correctness** — without sufficient test coverage, there are no contracts for agents to follow.

This has major implications for [[context-reliability]]:
- Poor test coverage → no explicit correctness criteria → agents make assumptions
- Agents need clear pass/fail signals to know if they're on track

### Documentation Must Match Code

Readmes must stay consistent with code. When they diverge, **agent paralysis ensues** — agents cannot determine which interpretation to trust.

### Spaghetti Code Compounds Errors

Eric's most important warning: *"Agents can compound errors very quickly. If an agent has one misunderstanding in a code, it can double down and create another error, it'll magnify it."*

This happens when agents iterate across multiple features:
- Step 1: agent misunderstands something
- Step 2: agent doubles down on that misunderstanding
- Result: errors magnify quickly through the workflow

### First Version Must Be Airtight

The first version of code an agent sees must be:
- **Well-tested** — contracts are explicit
- **Consistently formatted** — linting and style checks pass
- **Built on consistent design patterns** — when parts of a codebase create the same object using different APIs, even human developers would be confused, so agents will be too

## Practical Implications

For [[claude-code]] and agentic systems:
1. Invest in test coverage before adding agentic workflows
2. Keep documentation in sync with code changes
3. Use linting/style tools consistently
4. Standardize design patterns before multi-agent complexity

## Exam Relevance

- [[context-reliability]] — error compounding, explicit contracts
- [[agentic-architecture]] — preparing a codebase for agents

## Related Pages

- [[mihail-eric-junior-engineers-crisis]]
- [[ai-native-engineer]]
- [[context-reliability]]
