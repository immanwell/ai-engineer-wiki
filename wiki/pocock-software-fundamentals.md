---
title: "Software Fundamentals in the AI Age"
aliases:
  - "Matt Pocock fundamentals"
tags:
  - wiki
  - "agentic-architecture"
domain: "agentic-architecture"
sources:
  - "Matt Pocock Software Fundamentals AI Age (2025).md"
status: stub
confidence: high
---

Created: Thursday, 23 April 2026, 19:08
Modified: `=dateformat(this.file.mtime, "DDDD, HH:mm")`

---

# Software Fundamentals in the AI Age

**Summary**: Matt Pocock argues that software fundamentals — deep modules, feedback loops, ubiquitous language, TDD — matter more than ever with AI coding. AI amplifies codebase quality: clean code creates virtuous cycles, bad code creates compounding disaster.

**Sources**: [[raw/Matt Pocock Software Fundamentals AI Age (2025).md|Matt Pocock Software Fundamentals]]

---

## Core Thesis

> "Bad code is the most expensive asset you can have in an AI-powered workflow."

The "specs to code" movement — write a spec, let AI generate code, re-run compiler — fails because it treats code as cheap. The opposite is true: AI amplifies whatever codebase it touches. Good code + AI = compounding leverage. Bad code + AI = compounding disaster.

## The 6 Failure Modes

### 1. The AI Didn't Build What You Wanted
Communication barrier between human and AI. Frederick Brooks' "design concept" — the invisible theory of what you're building — must be shared. Pocock's fix: "Grill Me" skill — AI interviews you endlessly until alignment is reached.

### 2. The AI Is Too Verbose
AI uses elaborate language for simple ideas. Fix: Domain-Driven Design's "ubiquitous language" — a shared markdown glossary of terms that appears in code, expert conversations, and prompts.

### 3. The Right Thing Doesn't Work
Execution fails even with alignment. Fix: Tight feedback loops — TypeScript, browser access, automated tests. The rate of feedback is your speed limit.

### 4. (Implied)
AI produces huge code dumps before thinking to type-check or test. Fix: TDD — write a test first, make it pass, then refactor.

### 5. (Implied)
Outrunning your headlights — AI goes too far before checking.

### 6. Your Brain Can't Keep Up
Cognitive overload from shipping more code than ever. Fix: Deep modules — design interfaces from outside, delegate internals to AI.

## Core Concepts

### Deep Modules (John Ousterhout)
Deep modules hide significant functionality behind simple interfaces. Shallow modules expose little functionality through complex interfaces. AI works best with deep modules because it can treat internals as a gray box.

### Feedback Loops Are the Speed Limit
The Pragmatic Programmer: rate of feedback is your speed limit. LLMs don't use feedback loops effectively by default — they produce huge code dumps before thinking to check. TDD forces small deliberate steps.

### Ubiquitous Language (Domain-Driven Design)
Shared terminology across code, expert conversations, and prompts. Makes AI think and communicate more concisely.

### Strategic vs Tactical Roles
AI = tactical programmer (sergeant executing ground-level changes). Human = strategic role (design, alignment, architecture).

## Related Pages

- [[agent-friendly-codebase]]
- [[software-taste]]
- [[deep-modules]]
- [[ai-native-engineer]]
