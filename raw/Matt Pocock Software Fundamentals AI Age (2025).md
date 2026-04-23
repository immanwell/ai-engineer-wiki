---
title: "Software Fundamentals in the AI Age"
source: "https://youtu.be/v4F1gFy-hqg"
author:
  - Matt Pocock
published: 2025
created: Thursday, 23 April 2026, 19:08
description: "Matt Pocock — Why software fundamentals matter more than ever with AI coding. 6 failure modes of specs-to-code workflows, deep modules, feedback loops, and ubiquitous language."
tags:
  - clippings
---

## The Thesis: Fundamentals Beat Hype

Matt Pocock opens with a provocative claim: software fundamentals matter more than ever in the AI age. As a teacher running a course called "Claude Code for Real Engineers," he had to build a curriculum around AI coding—a moving target where everything changes constantly. The prevailing "specs to code" movement suggests you can write a specification, let AI generate code, and simply re-run the compiler when things break. But Pocock tried this and watched it spiral into disaster: each iteration produced worse code until the codebase became pure garbage. The movement assumes code is cheap, but Pocock argues bad code is actually the most expensive it's ever been, because a brittle codebase prevents you from capturing any of AI's real value.

## Why Code Quality Determines AI Success

The core insight comes from John Ousterhout's *Philosophy of Software Design*: bad code is complex code—anything that makes a system hard to understand and modify. The Pragmatic Programmer adds the concept of software entropy, where every change made in isolation degrades the overall design. This is exactly what happens when you endlessly re-run the compiler without thinking about structure. AI performs extraordinarily well in good codebases and flounders in bad ones. The better your codebase, the better your feedback loops, which means you can give better signals to the LLM—creating a virtuous cycle rather than a death spiral into spaghetti code.

## Failure Mode One: The AI Didn't Build What You Wanted

When the ai produces something entirely different from your intent, there's a fundamental communication barrier. Frederick Brooks' *The Design of Design* introduces the "design concept"—an invisible, ephemeral theory of what you're building that exists between collaborators. When you and the AI don't share this concept, miscommunication is guaranteed. Pocock developed a skill called "Grill Me": the AI interviews you endlessly, questioning every branch of the design tree and resolving dependencies one by one until shared understanding is reached.

## Failure Mode Two: The AI Is Too Verbose

Verbose AI output feels like talking across purposes—the model uses elaborate language to communicate what a simpler explanation could cover. This mirrors the domain expert problem: when developers lack shared terminology with subject matter experts, everything requires translation. Pocock turned to Domain-Driven Design and its concept of a "ubiquitous language"—a markdown file of shared terms derived from the same domain model that appears in code, conversations with experts, and prompts alike.

## Failure Mode Three: The Right Thing Doesn't Work

When alignment is perfect but execution fails, feedback loops become essential: TypeScript for static typing, browser access for frontend LLM work, and automated tests. Even with these loops in place, LLMs don't use them effectively by default—they produce huge code dumps before thinking to type-check or test, what the Pragmatic Programmer calls "outrunning your headlights." The rate of feedback is your speed limit. The solution is TDD: write a test first, make it pass, then refactor.

## Deep Modules: The Architecture That Makes AI Work

John Ousterhout defines the gold standard as deep modules. Deep modules hide significant functionality behind simple interfaces; you don't need to understand their internals to use them. Shallow modules do the opposite: not much functionality exposed through complex interfaces that force you to navigate dozens of tiny blobs. Deep module codebases let you treat implementation as a gray box—you design the interface carefully, test at the boundary, and let the AI handle the internals within tested constraints.

## Failure Mode Six: Your Brain Can't Keep Up

The final failure mode hits when feedback loops work and you're shipping more code than ever, but cognitive load becomes unbearable. Deep modules solve this by letting you design from the outside—you own the interface and purpose, while delegating interior implementation to the AI. Kent Beck's principle applies here: invest in the design of the system every single day.

## Key Quotes

> "Rate of feedback is your speed limit" — The Pragmatic Programmer

> "Bad code is the most expensive asset you can have in an AI-powered workflow."

> "Think of AI as a tactical programmer—a sergeant executing ground-level changes—while you occupy the strategic role above it."
