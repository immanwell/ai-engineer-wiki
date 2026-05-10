---
title: "Designing Memory Systems for Self-Learning Agents"
source: "https://www.youtube.com/live/GMIWm5y90xA"
author:
  - "Mahes (Product Manager, Platform Team, Anthropic)"
published: 2026-05-06
created: 2026-05-10
description: "Code with Claude 2026 — Session 3: Memory as a primitive for agents, file system-based memory model, Dreaming (research preview), multi-agent memory considerations"
tags:
  - "clippings"
  - "anthropic-event"
  - "agent-memory"
---

# Designing Memory Systems for Self-Learning Agents

**Speaker**: Mahes (Product Manager, Platform Team, Anthropic)
**Event**: Code with Claude 2026
**Date**: May 6, 2026
**Watch**: https://www.youtube.com/live/GMIWm5y90xA

---

## 1. Why Memory is the Next Primitive

Anthropic has launched increasingly higher-level primitives:

| Primitive | What It Gives Agents |
|----------|----------------------|
| **MCP** | Access to external tools and data |
| **Skills** | Agents pick up new capabilities designed by other agents or humans |
| **Memory** | Continuous self-learning and context management over long horizon tasks |

> "Memory is the next primitive. It's the thing that I think will get us to self-learning agents that evolve and improve based on the tasks they're working on and their own experience."

### What Agents Can Learn from Memory

- **About tasks**: success criteria, common mistakes, strategies that work or don't work
- **About environments**: codebases they interact with, files and assets to keep updated
- **From other agents**: shared learnings, what's going wrong elsewhere in a system

### Real-World Result

**Roktun** reported: 90% drop in first-pass mistakes in internal knowledge agents because agents caught mistakes and shared learnings with the next iteration of agents. Also led to better token efficiency, lower costs, and better latency.

---

## 2. Memory in Cloud Managed Agents (Public Beta)

### Design Principle: File System Model

> "We came to the conclusion: why can't we go the same direction with memory as we did with skills? Memory models memory as a file system to Claude — a series of files with a specific hierarchy and format that Claude can manage and update on its own."

Claude uses familiar tools (`bash`, `grep`) to manage memory — same tools that make it good at agentic coding.

**Opus 4.7 improvement**: State-of-the-art at file system-based memory. Better at discerning what content is worth remembering, what structure to use, how many files to split memory into.

### Multi-Agent Memory Considerations

When hundreds or thousands of agents share the same memory state:

**Permission scopes**: Mix and match session memory access
- **Read-only** memory store: Organization-wide knowledge, best practices, runbooks
- **Read-write** memory store: Working memory, specific and frequently updated per task

**Optimistic concurrency**: Content hash checks before overwriting — prevents one agent from clobbering another's memory update

### Enterprise Controls

| Feature | What It Provides |
|---------|-------------------|
| **Version history** | Full audit log of every memory update |
| **Attribution metadata** | Which agent made an update, when, which session |
| **Standalone API** | Build bespoke memory systems outside managed agents — PII scanning, cleanup, external storage |

---

## 3. The Three Layers of a Frontier Memory System

| Layer | What It Covers |
|-------|----------------|
| **Storage** | Where data is actually stored, metadata, attribution |
| **Structure/Content** | File system hierarchy for memory; skills as procedural memory |
| **Process** | How often memory is updated, what triggers updates, what sources inform changes |

The Memory API solves the storage and structure layers. But scaling to multi-agent systems revealed limitations:

- Sessions missed learnings other agents had already figured out
- Common mistakes and shared patterns across agents weren't being shared
- Agents were siloed into their specific task — couldn't efficiently keep a large memory store up to date holistically

---

## 4. Dreaming (Research Preview)

**What it is**: A batch asynchronous process that runs separately from agent sessions. Looks for patterns and mistakes across recent agent transcripts and automatically produces organized, up-to-date memory content.

### How It Works

```txt
Periodic trigger (cron) or event trigger (agents spin down)
↓
Dreaming job runs
↓
Looks through recent transcripts for:
  - Common mistakes (failed tool calls, repeated errors)
  - Strategies that are working
  - Shared patterns across agents
↓
Produces updated memory state (diff)
↓
Optional: manual review via API
↓
Apply to memory store
↓
Future agents benefit from consolidated learnings
```

### Key Properties

1. **Out of band**: Happens outside the context of an agent working on a specific task
   - No latency added to the hot path
   - Can look at multiple agents simultaneously to find shared patterns a single agent wouldn't notice from its own limited perspective

2. **Separates objectives**: Memory quality is a separate objective from task completion — agents stay focused on their task while dreaming handles memory organization

3. **Scales compute**: Uses additional compute upfront to create a well-organized, up-to-date index that all downstream agents can use efficiently
   - Analogous to test-time compute: spending more tokens upfront → better final outcomes
   - Like a search index: upfront effort to produce high-quality index → fast, efficient retrieval at query time

### Performance Result

**Harvey** (legal benchmark): **6x increase in task completion rate** when deploying Dreaming on a realistic legal scenario.

---

## 5. SRE Agent Demo Walkthrough

**Scenario**: SRE agent monitors alerts, spins up triage agents as needed.

**Each agent has multiple memory stores**:

| Memory Store | Access | Content |
|-------------|--------|---------|
| Org-wide knowledge | Read-only | Runbooks, SLO guidelines, contact owners |
| SRE + codebase | Read-write | Agents learn and update as they investigate |

**In action**:
1. P1 alert fires from dispatch service
2. SRE agent investigates (checks CPU, traffic patterns, recent PRs)
3. Agent writes learnings to memory store
4. Same alert fires again minutes later — **different agent** spins up
5. First thing it does: reads the note in memory → short-circuits investigation, saves time

**Immediate gains**:
- Token efficiency (not re-investigating the same thing)
- Intelligence gain (knows what else to investigate)

### Enterprise Features Shown

- **Version history**: Every update logged with timestamp, agent ID, session ID
- **Precondition hash**: Optimistic concurrency check before overwriting

---

## 6. The Full Picture: Frontier Memory System

```txt
Memory (Real-time Read/Write)          Dreaming (Batch Async Enrichment)
       ↓                                         ↓
  Immediate learnings               Comprehensive pattern detection
  Per-session context               Organization, deduplication, verification
  Hot path                         Upstream investment → downstream efficiency
       ↓                                         ↓
  Shared memory store ←—————————— Updated memory state (diff)
                   
Future agents automatically benefit from previous day's experience
```

> "Over the next couple of months, we're going to start seeing agents that run for days or many hours at a time. Memory is going to be a really important part of that system and what makes it ultimately possible."

---

## Key Takeaways for the Wiki

1. **Memory = file system** — Claude manages it with `bash` and `grep` tools
2. **Permission scopes** — read-only vs read-write for different memory stores
3. **Optimistic concurrency** — content hash prevents overwriting concurrent agent updates
4. **Version history + attribution** — audit log, which agent, which session, which timestamp
5. **Dreaming = out-of-band batch process** — 6x task completion improvement in Harvey's legal benchmark
6. **Three layers**: storage → structure/content → process
7. **Memory + Dreaming = frontier memory system** — real-time read/write + async batch enrichment

---

## Existing Wiki Connections

- [[agent-memory.md]] — already has reflection and memory concepts; this session adds concrete implementation details
- [[claude-managed-agents.md]] — Memory and Dreaming are features in the managed agents API
- [[agentic-architecture.md]] — memory as a primitive alongside MCP and Skills