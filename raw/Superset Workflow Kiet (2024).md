---
title: "Superset Workflow"
source: "https://youtu.be/8AfjxJu_ViI"
author: Kiet
published: 2024
created: Friday, 24 April 2026, 21:26
description: "Kiet — AI-assisted development as a manufacturing pipeline: 5 stages (trigger, plan, coding, review, merge), throughput as bottleneck, and token allocation across the workflow."
tags:
  - clippings
---

## The Core Problem: Tokens Don't Equal Value

Everyone agrees "more tokens equals more profits," but many teams are throwing massive amounts of tokens at coding and getting decreasing incremental value. The question becomes: where should you actually spend your tokens?

Kiet combines coding with lean manufacturing — specifically the Toyota production system from the book *The Goal*.

## Software Development as a Manufacturing Line

The full software development cycle as a manufacturing pipeline with 5 stages:

```
Trigger → Plan → Code → Review → Merge
```

**Trigger** (Green — agent-driven): Customer feedback, bugs, any event requiring code change. Companies wire Sentry and GitHub events to automatically create PRs using workflows, cron jobs, and agents that triage issues, create unit tests, and open PRs when tests fail.

**Plan** (Human-driven): Some planning before code changes. Requires good documentation, strong context (Chroma and Mastra's observational memory work are mentioned), and keeping Markdown files human-driven so agents can follow the design.

**Coding** (Green — agent-driven): Where most teams are spending all their tokens. Has massive parallelization potential through Git worktrees, branching strategies, and VMs.

**Review** (Human bottleneck): Human review required. Well-maintained unit tests that encapsulate business logic are critical — agents that mock up fake tests miss the point. Agent review rounds using tooling to visually drive the product, read logs, and self-validate are already in use.

**Merge** (Human-controlled): Auto-merging everything is risky. Better approach: merge recklessly into a separate branch, let agents run smoke tests on a cron schedule, only promote verified changes to clean main.

## Superset's Own Case

Superset can generate many PRs from triggers, has a human-driven plan loop, blows through coding with 400 open PRs on GitHub — then hits a wall at review where everything drops off.

The bottleneck is clear: **review step is killing throughput.**

## The Goal Framework (Lean Manufacturing)

From *The Goal*:
- Define throughput (a measurable proxy — e.g., merged PRs)
- Identify bottlenecks
- Measure actual throughput as the minimum of every workflow stage

## Key Quote

> "Throughput is the minimum of every single piece of the workflow — everything is only as fast as your slowest step."