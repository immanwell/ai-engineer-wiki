---
title: "The Capability Curve"
aliases:
  - "capability curve"
  - "riding the curve"
tags:
  - wiki
  - "anthropic-event"
  - "agentic-architecture"
domain: "agentic-architecture"
sources:
  - "The Capability Curve.md"
status: stable
confidence: high
---
Created: Sunday, 10 May 2026, 20:45
Modified: `=dateformat(this.file.mtime, "DDDD, HH:mm")`

---

# The Capability Curve

**Speaker**: Alex Albert (Research PM, Anthropic)
**Event**: Code with Claude 2026 — Session 5
**Date**: May 6, 2026
**Watch**: https://www.youtube.com/live/GMIWm5y90xA

**Summary**: Model capability improvements across planning, error recovery, and attention are absorbing scaffolding work that used to require manual implementation. Three actionable tips: invest in evals, simplify scaffolding, give the model room to work.

**Sources**: [[raw/The Capability Curve.md|The Capability Curve — Code with Claude 2026]]

---

## The Core Idea

> "This talk isn't about any one of these models in particular. What I do want to focus on is what it means to build on something that is getting meaningfully better month over month."

The capability curve = model improvements that compound over time, absorbing work that used to require scaffolding:

| Era | Model | Scaffolding needed |
|-----|-------|-------------------|
| Build everything yourself | Sonnet 3.7 | Retry routers, manual context chunking, verification loops |
| Remove scaffolding | Opus 4.7 | Less — model handles error recovery, planning, attention |
| Future | ??? | Even less? |

**The rule**: Every year, compensating code becomes obsolete. Invest in connecting code instead.

---

## SweeBench Verified: Hard Numbers

| Model | Score | What it means |
|-------|-------|---------------|
| Sonnet 3.7 (1 year ago) | 62% | Baseline |
| Opus 4.7 (now) | **87%** | Over 25% jump in a year |

- Opus 4.7 is **more than 3x as likely** to succeed on difficult PRs that Sonnet 3.7 was failing on
- SweeBench measures model's ability to autonomously complete software PRs

---

## Demo: Same Task, 12 Months Apart

**Task**: Recreate Cloud.ai with a single prompt

**Sonnet 4 (old)**:
- Produced generic black-and-white chat application
- Hit an error immediately — didn't even work
- Just made a nice UI, no backend

**Opus 4.7 (new)**:
- Output looked better immediately — Cloud color scheme, dark mode
- Actually connected to the Cloud API and returned real responses
- Remembers old chat when starting a new one
- Renders inline visualizations
- Did it in **fewer lines of code** — more efficient too

---

## Three Areas of Model Gains

### 1. Planning: Think First, Then Act

**Old behavior (Sonnet 3.7)**:
- "Act first and think later" — like building IKEA furniture without reading instructions first

**New behavior (Opus 4.7)**:
- Takes time upfront to think about the problem
- Strategizes and plans before writing code
- Then dives into action

**Implication**: Give Claude time to think. Don't force it to jump straight into action — this can reduce downstream performance.

### 2. Error Recovery: No More Doom Loops

**Old behavior**:
- Model hits a problem → proposes a solution → doesn't work → keeps spiraling → context stalls → everything must be cleared

**New behavior (Opus 4.7)**:
- Backs out of dead ends
- Thinks about it differently and takes a different path

**Implication**: Better task performance with fewer wasted tokens.

### 3. Attention Over Long Runs

**Old behavior**:
- Loses the plot, forgets things, stops paying attention to system prompt
- Coherence breaks down across long contexts

**New behavior (Opus 4.7)**:
- Holds coherence across **1 million tokens**
- Remembers system prompt instructions throughout
- Stays focused for entire runs

**Implication**: No need to babysit the context window. Claude operates autonomously on long runs.

---

## Tip 1: Refresh Your Evals

> "If you can measure something, you can improve on it."

**Three rules**:

1. **Measure your actual product distribution** — not academic benchmarks
   - Bad: coding agent evaled on academic coding benchmarks
   - Good: coding agent evaled on traffic similar to what your users actually do

2. **Ensure evals are not saturated** — as models get smarter, evals need to get harder to continue getting signal

3. **Test on the newest frontier models** — sometimes the best optimization is simply swapping in the latest model

> "I found that sometimes the best optimization you can make to your app is simply swapping in the latest model."

---

## Tip 2: Shrink Your Scaffolding

**What is scaffolding**: code, prompts, skills, tool setups — everything surrounding the model directing it toward its goals.

**The insight**: With newer models, you might not need things you needed before.

- Instead of a multi-step workflow, let the model work in one thread
- **Often you can boost performance by removing instead of adding**
- Revise prompts that became "a hideous mess of different rules and instructions" across model generations

---

## Tip 3: Give the Model Room to Work

### Allow adaptive thinking

- Let Claude choose when to think
- Use adaptive thinking and the `effort` parameter to dial thinking vs. actions

### Allow more controlled tool access

- **Example: Claude Code Auto Mode**
  - Runs classifiers over tool calls Claude proposes
  - Determines if a tool call needs human approval or can proceed
  - Lets Claude run in the background longer and more autonomously

### Close the loop for your agent

- Design systems so Claude can inspect its own outputs and iterate
- Example: give a coding agent a computer use tool so it can click around and QA test what it writes
- "Models are continuously getting better at verifying and iterating on their outputs — allow it the affordances to do so."

---

## Customer Results

| Company | What they saw |
|---------|--------------|
| **Vercel** | Opus 4.7 writing proofs for systems code before implementing a single line |
| **WinServ** | Claude sustaining attention over their longest agentic runs |
| **Shopify** | Model iteratively refining its own outputs as it coded |

---

## Key Takeaways

1. **SweeBench: 62% → 87%** in a year. Opus 4.7 is 3x more likely to succeed on difficult PRs.
2. **Planning**: New models think before acting — give Claude time to strategize.
3. **Error recovery**: No more doom loops — model backtracks and takes different paths.
4. **Attention**: Coherence across 1M tokens — no babysitting the context window.
5. **Evals first**: Measure your actual product distribution, not academic benchmarks.
6. **Simplify scaffolding**: Removing things often boosts performance more than adding.
7. **Give Claude room**: Adaptive thinking, controlled tool access, loop-closing affordances.
8. **The capability curve**: Model improvements absorb scaffolding work over time.

---

## Related Pages

- [[the-expanding-toolkit]] — Session 4: compensating code vs connecting code
- [[advisory-strategy]] — Sonnet+Opus pattern as response to capability curve
- [[foundation-model-evaluation]] — evaluation-driven development, private leaderboards
- [[claude-code]] — Auto Mode, effort parameter, adaptive thinking
- [[functional-correctness]] — binary pass/fail evaluation (SweeBench-style)
- [[agentic-architecture]] — agentic loop, planning, error recovery, sustained attention