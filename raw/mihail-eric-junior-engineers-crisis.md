# The Crisis Facing Junior Software Engineers

**Source:** Stanford Talk by Mihail Eric (Stanford Adjunct Lecturer)
**URL:** https://youtu.be/wEsjK3Smovw
**Date:** April 2026
**Duration:** 14m 20s
**Word Count:** ~3,300 words

---

## Summary

Mihail Eric describes a "perfect storm" hitting new software developers: post-2021 overhiring followed by mass layoffs, a 2-3x increase in CS graduates over 15 years, and employers now preferring fewer AI-native hires over more traditional candidates. One Berkeley graduate he spoke with applied to 1,000 positions and heard back from only two. Eric predicts this generation will be the first to face the full force of this shift, needing both strong fundamentals and genuine AI fluency to stand out.

## What Makes an AI-Native Engineer

The AI-native engineer combines traditional programming foundations with strong competency in agentic workflows. Eric cautions against mimicking Boris from Claude who runs 10 agents simultaneously—starting that way is the wrong approach entirely. Instead, he recommends building one agent workflow reliably before adding a second, then a third, always ensuring each isolated task is well understood before expanding. The core skill is context switching: watching multiple "eager, savvy intern" agents work simultaneously, remembering where each left off, and meaningfully pushing each task forward. Eric notes this mirrors what makes a good human manager, and the best multi-agent practitioners are often those with prior experience managing human developers.

## Building an Agent-Friendly Codebase

Agents can only operate on explicitly defined contracts—primarily tests that define software correctness. Without sufficient test coverage, there are no contracts for agents to follow. Readmes must stay consistent with code; when they diverge, agents paralysis ensues as they cannot determine which interpretation to trust. Spaghetti code emerges when agents iterate across multiple features and compound errors magnify quickly—if an agent misunderstands something in step one, it doubles down on that error in step two. Eric emphasizes that the first version of code an agent sees must be airtight: well-tested, consistently formatted with linting and style checks, and built on consistent design patterns. When parts of a codebase create the same object using different APIs, even human developers would be confused—so agents will be too.

## From Functional to Exceptional Software

Taste separates good software from great software, and it develops in what Eric calls "the last mile"—after achieving 100% on an assignment, choosing to build something more complex because you want to solve a problem, not just get a grade. The students who excelled most built startups around their class projects, continuing long after the course ended because they saw genuine potential. Eric describes how even teams at Anthropic constantly rewrite Claude using Claude itself, treating their own product as a laboratory for experimentation. He reinforces to students that while he can offer guidance, each developer must "beat their head against the wall" personally to develop genuine intuition for what works.

## Why Junior Engineers Still Matter

Senior developers often resist AI tools because 20 years of ingrained habits make them stubborn about alternatives. Junior developers arrive as "sponges"—everything is possible to them, unconstrained by internalized beliefs about how industries work. Eric calls this "good naivety," perfectly suited for startup founders willing to tackle problems others see as unsolvable. Developers also bring what Eric describes as "arrogance"—the confidence that any problem has a software solution, and the willingness to dig into internals when things break rather than simply moving away. This combination of nimbleness, experimentation, and stubborn problem-solving makes junior developers uniquely suited to adopt AI-native skills fastest, even if employment feels harder to obtain initially. Harvard Business School professor Rem Coning adds that the future belongs to those who can allocate intelligence effectively—embedding AI directly into products to remove humans from the loop entirely.

## Key Quotes

> "Build it one at a time. Make sure that you first understand what has to be done and then know where the lines are between those items of work." — Mihail Eric

> "Agents can compound errors very quickly. If an agent has one misunderstanding in a code, it can double down and create another error, it'll magnify it." — Mihail Eric

## Timestamps

- 0:50 — Introduction / Overview of the crisis
- ~5:00 — What Makes an AI-Native Engineer
- ~8:00 — Building an Agent-Friendly Codebase
- ~11:00 — From Functional to Exceptional Software
- ~13:00 — Why Junior Engineers Still Matter
