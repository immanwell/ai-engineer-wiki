---
title: "Superset Workflow"
aliases:
  - "coding workflow"
  - "token allocation"
tags:
  - wiki
  - "agentic-architecture"
domain: "agentic-architecture"
sources:
  - "Superset Workflow Kiet (2024).md"
status: stub
confidence: medium
---

Created: Friday, 24 April 2026, 21:26
Modified: `=dateformat(this.file.mtime, "DDDD, HH:mm")`

---

# Superset Workflow

**Summary**: AI-assisted development reframed as a manufacturing pipeline with 5 stages (trigger, plan, coding, review, merge). The bottleneck determines throughput — not the coding stage. Token allocation should follow the bottleneck, not default to coding.

**Sources**: [[raw/Superset Workflow Kiet (2024).md|Superset Workflow]]

---

## The 5-Stage Pipeline

```
Trigger → Plan → Coding → Review → Merge
```

| Stage | Driver | Notes |
|---|---|---|
| **Trigger** | Agent | Sentry/GitHub events auto-create PRs, agents triage issues |
| **Plan** | Human | Good docs, strong context (observational memory), Markdown human-driven |
| **Coding** | Agent | Parallelization via worktrees, branching, VMs |
| **Review** | Human | Often the bottleneck — unit tests as contracts critical |
| **Merge** | Human | Canary approach: merge to separate branch, smoke tests, promote only verified |

## The Core Insight

> "Throughput is the minimum of every single piece of the workflow — everything is only as fast as your slowest step."

Most teams pour tokens into coding and get decreasing value. The answer: find the bottleneck and scale agent-driven parts around it, not ahead of it.

Superset's case: 400 open PRs, review step is the choke point.

## Key Frameworks

### From *The Goal* (Lean Manufacturing)
- Define throughput (measurable proxy: merged PRs)
- Identify bottlenecks
- Measure actual throughput as the minimum of every workflow stage

### Token Allocation Problem
Teams throw tokens at coding and get decreasing incremental value. The bottleneck (often review) determines where tokens should actually go.

## Related Pages

- [[pocock-software-fundamentals]] — rate of feedback as speed limit
- [[claude-code]] — parallelization via worktrees, coding stage
- [[agent-friendly-codebase]] — unit tests as contracts at review stage
- [[deep-modules]] — clean interfaces so agents can navigate coding stage