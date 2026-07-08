---
title: "Claude Code Loops"
aliases:
  - "designing loops"
  - "loop types"
  - "turn-based loop"
  - "goal-based loop"
  - "proactive loops"
tags:
  - wiki
  - "claude-code"
domain: "claude-code"
sources:
  - "Getting started with loops (ClaudeDevs).md"
status: stable
confidence: high
---

Created: Wednesday, 8 July 2026, 12:57
Modified: `=dateformat(this.file.mtime, "DDDD, HH:mm")`

---

# Claude Code Loops

**Summary**: The Claude Code team defines a **loop** as an agent repeating cycles of work until a stop condition is met. Loops come in four types — turn-based, goal-based, time-based, and proactive — distinguished by how they are triggered, how they stop, which primitive they use, and what task they suit. Start with the simplest loop; escalate only when the task demands it.

**Sources**: [[raw/Getting started with loops (ClaudeDevs).md|Getting started with loops (ClaudeDevs)]] (written by delba_oliveira)

---

## What a Loop Is

> "Loops are agents repeating cycles of work until a stop condition is met."

Loops are categorized along four axes:

1. **How they are triggered** — user prompt, time interval, or event
2. **How they are stopped** — Claude's judgment, a defined goal, a turn cap, or manual cancel
3. **What Claude Code primitive is used** — skills, `/goal`, `/loop`, `/schedule`, dynamic workflows
4. **What task is most appropriate** — matching the loop to the shape of the work

**Guiding principle**: Not all tasks require complex loops. Start with the simplest solution and use these patterns selectively.

## The Four Loop Types

### 1. Turn-Based Loops

| Property | Detail |
|----------|--------|
| **Triggered by** | A user prompt |
| **Stop criteria** | Claude judges it has completed the task or needs more context |
| **Best for** | Shorter tasks not part of a regular process or schedule |
| **Manage usage** | Write specific prompts; improve verification with skills to reduce turns |

Every prompt starts a manual loop where you direct each turn. Claude gathers context → takes action → checks its work → repeats if needed → responds. This is the **agentic loop**. You then manually check the work and write the next prompt.

**Key lever**: Encode your manual verification steps as a `SKILL.md` so Claude can check more of its own work end-to-end. Include tools/connectors so Claude can see, measure, or interact with the result. *The more quantitative the checks, the easier it is for Claude to self-verify.*

Example — a `verify-frontend-change` skill that starts the dev server, interacts with the new control, screenshots before/after, checks the browser console for zero new errors, and runs a Core Web Vitals audit via Chrome DevTools MCP before declaring the change done.

### 2. Goal-Based Loops (`/goal`)

| Property | Detail |
|----------|--------|
| **Triggered by** | A manual prompt in real time |
| **Stop criteria** | Goal achieved OR maximum number of turns reached |
| **Best for** | Tasks with verifiable exit criteria |
| **Manage usage** | Set specific completion criteria and explicit turn caps ("stop after 5 tries") |

When one turn isn't enough, `/goal` extends how long Claude iterates by defining what *done* looks like. Each time Claude tries to stop, an **evaluator model** checks your condition and sends it back to work until the goal is met or the turn cap is hit. This prevents Claude from ending early on its own "good enough" judgment.

**Deterministic criteria work best** — number of tests passed, a score threshold cleared.

```bash
/goal get the homepage Lighthouse score to 90 or above, stop after 5 tries.
```

### 3. Time-Based Loops (`/loop` and `/schedule`)

| Property | Detail |
|----------|--------|
| **Triggered by** | A specified time interval |
| **Stop criteria** | You cancel it, or the work completes (PR merges, queue empties) |
| **Best for** | Recurring work, or interfacing with external systems/environments |
| **Manage usage** | Set longer intervals, or react to events rather than time |

Some work is recurring — the task stays the same, only the inputs change (e.g. summarizing Slack every morning). Other work depends on external systems you check on an interval and react to (e.g. a PR that may get review comments or fail CI).

```bash
/loop 5m check my PR, address review comments, and fix failing CI
```

- **`/loop`** runs on *your computer* — turn it off and it stops.
- **`/schedule`** moves the loop to the *cloud* by creating a routine.

### 4. Proactive Loops

| Property | Detail |
|----------|--------|
| **Triggered by** | An event or schedule, with no human in real time |
| **Stop criteria** | Each task exits when its goal is met; the routine runs until you turn it off |
| **Best for** | Recurring streams of well-defined work: bug reports, issue triage, migrations, dependency upgrades |
| **Manage usage** | Route routines to smaller/faster models; use the most capable model only for judgment calls |

Proactive loops **compose** the other primitives plus **auto mode** and **dynamic workflows** (research preview) into long-running autonomous work:

1. **`/schedule`** — run a routine that checks for new reports
2. **`/goal`** + **skills** — define what done looks like and how to verify it
3. **Dynamic workflows** — orchestrate agents that triage, fix, and review
4. **Auto mode** — run without stopping to ask for permission

```bash
/schedule every hour: check the project-feedback channel for bug reports.
/goal: don't stop until every report found this run is triaged, actioned,
and responded to. When fixing a bug, use a workflow to explore three
solutions in parallel worktrees and have a judge adversarially review them.
```

The model-routing advice here (small/fast models for routine steps, capable model for judgment) mirrors the [[advisory-strategy|Advisory Strategy]] — Executor for the bulk, Advisor for the hard calls.

## Maintaining Code Quality

The quality of a loop's output depends on the **system around it**:

- **Keep the codebase clean** — Claude follows existing patterns and conventions
- **Give Claude a way to verify its own work** — encode what "good" looks like with skills
- **Make docs easy to reach** — framework/library docs carry up-to-date best practices
- **Use a second agent for code review** — a reviewer with fresh context is less biased than the main agent (built-in `/code-review` skill, or Code Review for GitHub)

**Systemic fix over one-off fix**: When a result misses the standard, don't just fix that instance — encode the lesson so *every* future iteration improves. This is the same compounding idea behind [[skills-anthropic|skills as institutional memory]].

## Managing Token Usage

Loops should have clear boundaries:

- **Choose the right primitive and model** — small tasks don't need multiple agents; some tasks can use cheaper/faster models
- **Define clear success and stop criteria** — specific enough that Claude arrives sooner (but not too soon)
- **Pilot before a large run** — dynamic workflows can spawn *hundreds* of agents; gauge on a small slice first
- **Use scripts for deterministic work** — running a script is cheaper than reasoning through steps each time (e.g. a PDF form-filling script shipped in a skill)
- **Don't run routines more often than needed** — match the interval to how often the watched thing actually changes
- **Review usage** — `/usage` breaks down recent usage by skills, subagents, MCPs; `/goal` with no args shows turns and tokens so far; `/workflows` shows each agent's token usage (and lets you stop any agent)

## Summary Table

| Loop | You hand off | Use it when | Reach for |
|------|-------------|-------------|-----------|
| **Turn-based** | The check | You're exploring or deciding | Custom verification skills |
| **Goal-based** | The stop condition | You know what done looks like | `/goal` |
| **Time-based** | The trigger | Work happens outside your project on a schedule | `/loop`, `/schedule` |
| **Proactive** | The prompt | Work is recurring and well-defined | All of the above + dynamic workflows |

**Getting started**: Look at work where *you* are the bottleneck and ask which piece you could hand off — can you write the verification check? Is the goal clear enough? Does the work arrive on a schedule? Run the loop, observe where it stalls or over-reaches, and iterate.

## Exam Relevance

Directly tests [[claude-code]] domain knowledge:
- The four loop types and their trigger/stop distinctions
- Which primitive (`/goal`, `/loop`, `/schedule`, skills, dynamic workflows) fits which task
- Token/quality management as a system-design responsibility

## Related Pages

- [[claude-code]] — parent page: configuration, hooks, `/schedule`, Auto Mode
- [[advisory-strategy]] — small-model-for-bulk / capable-model-for-judgment routing
- [[skills-anthropic]] — skills as the verification and institutional-memory layer inside loops
- [[agent-orchestration-patterns]] — dynamic workflows and multi-agent orchestration
- [[the-capability-curve]] — "give the model room to work" underpins goal/proactive loops
- [[agentic-architecture]] — the underlying agentic loop that all four types extend
