---
title: "The Capability Curve"
source: "https://www.youtube.com/live/GMIWm5y90xA"
author:
  - "Alex Albert (Research PM, Anthropic)"
published: 2026-05-06
created: 2026-05-10
description: "Code with Claude 2026 — Session 5: Model capability improvements across planning, error recovery, and attention. Three tips: invest in evals, simplify scaffolding, give the model room to work."
tags:
  - "clippings"
  - "anthropic-event"
---

# The Capability Curve

**Speaker**: Alex Albert (Research PM, Anthropic)
**Event**: Code with Claude 2026
**Date**: May 6, 2026
**Watch**: https://www.youtube.com/live/GMIWm5y90xA

---

## Core Theme

> "This talk isn't about any one of these models in particular. What I do want to focus on is what it means to build on something that is getting meaningfully better month over month."

The capability curve = model improvements that compound over time, absorbing work that used to require scaffolding.

---

## SweeBench Verified: The Numbers

| Model | Score | What It Means |
|-------|-------|---------------|
| Sonnet 3.7 (1 year ago) | 62% | Baseline |
| Opus 4.7 (now) | **87%** | Over 25% jump in just over a year |

- Opus 4.7 is **more than 3x as likely** to succeed on difficult PRs that Sonnet 3.7 was failing on
- SweeBench measures model's ability to autonomously complete software PRs

---

## Demo: Sonnet 4 vs Opus 4.7 on the Same Task

**Task**: Recreate Cloud.ai with a single prompt

### Sonnet 4 (1 year ago)
- Produced a generic black-and-white chat application
- Hit an error immediately — didn't even work
- Just made a nice UI, no backend functionality

### Opus 4.7 (today)
- Output looked better immediately — Cloud color scheme, dark mode
- Actually connected to the Cloud API and returned real responses
- Remembers old chat when starting a new one
- Renders inline visualizations like the real Cloud.ai
- Did it all in **fewer lines of code** — more efficient too

---

## Three Areas of Model Gains

### 1. Planning: Think First, Then Act

**Old failure mode (Sonnet 3.7)**:
- "Act first and think later" — like building IKEA furniture without reading instructions first

**New behavior (Opus 4.7)**:
- Takes time upfront to think about the problem
- Strategizes and plans before writing code
- Then dives into action

**Implication**: Give Claude time to think. Don't force it to jump straight into action — this can reduce downstream performance.

### 2. Error Recovery: No More Doom Loops

**Old failure mode**:
- Model hits a problem → proposes a solution → solution doesn't work → keeps spiraling → context stalls out → everything must be cleared

**New behavior (Opus 4.7)**:
- When hitting a problem, can backtrack out of it
- Thinks about it in a different way and takes a different path

**Implication**: Better task performance with fewer wasted tokens — no more doom loops.

### 3. Attention Over Long Runs

**Old failure mode**:
- Loses the plot over long runs
- Forgets things, stops paying attention to system prompt instructions
- Coherence breaks down

**New behavior (Opus 4.7)**:
- Holds coherence across hundreds of thousands or even a **million tokens**
- Remembers system prompt instructions
- Stays focused for the entire run

**Implication**: You don't need to babysit the context window. No need to chunk up work. Claude can operate autonomously on long runs.

---

## Customer Results

| Company | What They Saw |
|---------|--------------|
| **Vercel** | Opus 4.7's planning → writing proofs for systems code before implementing a single line |
| **WinServ** | Claude sustaining attention over their longest agentic runs |
| **Shopify** | Model going back and iteratively refining its outputs as it coded |

---

## Tip 1: Start with Evals

> "If you can measure something, you can improve on it."

**Three rules for good evals**:

1. **Measure something close to your product distribution** — not academic benchmarks
   - Bad example: coding agent evaled on academic coding benchmarks
   - Good example: coding agent evaled on traffic similar to what your users actually do

2. **Ensure evals are not saturated** — as models get smarter, evals need to get harder to continue getting signal from frontier models

3. **Test on the newest frontier models** — sometimes the best optimization is simply swapping in the latest model

> "I found that sometimes the best optimization you can make to your app is simply swapping in the latest model."

---

## Tip 2: Take a Second Look at Your Scaffolding

**What "scaffolding" means**: code, prompts, skills, tool setups — everything surrounding the model directing it toward its goals.

**The insight**: With newer models, you might not need some of the things you needed before.

- Maybe instead of a multi-step workflow, you can let the model work on a task in one thread
- **Often you can boost your performance by removing instead of adding things onto your scaffolding**

**Also revisit prompts** — prompts build up model over model and become "a hideous mess of different rules and instructions." With every new model, take a second look and cut things that might not be needed anymore.

---

## Tip 3: Give the Model Room to Work

### Allow adaptive thinking

- Let Claude choose when to think
- Use `adaptive thinking` and dial the amount of thinking and actions via the `effort` parameter

### Allow more controlled tool access

- Not saying let it do anything — there are ways to let Claude execute on more systems safely
- **Example: Claude Code Auto Mode**
  - Runs classifiers over tool calls Claude is proposing
  - Determines if a tool call needs explicit human approval or not
  - Allows Claude to run in the background for longer and work more autonomously

### Close the loop for your agent

- Design systems so Claude can inspect its own outputs and iterate on them
- Example: give a coding agent a computer use tool so it can click around and QA test what it writes
- "Models are continuously getting better at verifying and iterating on their outputs, so it's important to allow it the affordances to do so."

---

## The Capability Curve Explained

The "capability curve" is the compounding effect of model improvements over time. Things that previously required manual scaffolding become built into the model as it improves:

| Era | Model | Scaffolding needed |
|-----|-------|-------------------|
| Build everything yourself | Sonnet 3.7 | Retry routers, manual context chunking, verification loops |
| Remove scaffolding | Opus 4.7 | Less — model handles error recovery, planning, attention |
| Future | ??? | Even less? |

**The rule**: Every year, compensating code becomes obsolete. Invest in connecting code instead.

This connects to the key rule from Session 4:
- **Compensating for model unreliability** → half-life of months → leave to Anthropic
- **Connecting your model to your world** → compounding code that belongs to you

---

## Key Takeaways

1. **SweeBench: 62% → 87%** in a year. Opus 4.7 is 3x more likely to succeed on difficult PRs.
2. **Planning**: New models think before acting — give Claude time to strategize.
3. **Error recovery**: No more doom loops — model backtracks and tries different paths.
4. **Attention**: Coherence across 1M tokens — no babysitting the context window.
5. **Start with evals**: Measure your actual product distribution, not academic benchmarks.
6. **Simplify scaffolding**: Often removing things boosts performance more than adding.
7. **Give Claude room**: Adaptive thinking, controlled tool access, loop-closing affordances.
8. **The capability curve**: Model improvements absorb scaffolding work over time.

---

## Existing Wiki Connections

- [[the-expanding-toolkit]] — Session 4: compensating code vs connecting code; tools that ship with model
- [[advisory-strategy]] — Session 4: Sonnet+Opus pattern as architectural response to capability curve
- [[foundation-model-evaluation.md]] — evaluation-driven development; private leaderboards
- [[claude-code]] — Auto Mode, effort parameter, adaptive thinking
- [[functional-correctness]] — binary pass/fail evaluation (SweeBench-style)