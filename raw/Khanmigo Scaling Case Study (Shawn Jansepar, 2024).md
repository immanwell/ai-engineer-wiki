---
title: "Scaling AI in Education with Khanmigo"
source: "https://youtu.be/3E7VAZaTG9M"
author:
  - Shawn Jansepar
published: 2024
created: Friday, 24 April 2026, 13:57
description: "Shawn Jansepar (Khan Academy Director of AI and Learning) — Case study on scaling Khanmigo: 200K learners, math agent architecture, Writing Coach, AI-first org transformation, and technical hurdles."
tags:
  - clippings
---

## Overview

Shawn Jansepar presents Khan Academy's case study on scaling Khanmigo. Khan Academy is a nonprofit serving 140 million registered users, 7 billion learning minutes in 2021-2022, and 1.5 million highly active learners. They have ~200,000 paid Khanmigo users, roughly half through school districts serving higher percentages of free and reduced lunch students. AI-first transformation driven by rapid prototyping and iteration.

## Scale Proof

- 200,000 Khanmigo learners and teachers
- ~50% from school districts serving under-resourced communities
- Post-pandemic: average 8th grader is 1.1 grade levels behind — Khan Academy sees AI as democratizing one-on-one tutoring at scale

## Socratic Method as North Star

Khan Academy's North Star: emulating human tutors. Khanmigo asks leading questions rather than giving answers. In a comparison, ChatGPT incorrectly validated a student's wrong work on distributing -4. Khanmigo caught the specific mistake and guided the student back.

## Math Agent Architecture

For math accuracy, Khan Academy built:
- A **math agent** with autonomy to use calculators or Python for complex problems
- **Chain of Thought prompting** — writes out how a student might have arrived at an answer before tutoring
- **RAG** — additional context via retrieval
- **Math accuracy dashboard** — monitors tutoring quality over time
- **Math accuracy benchmark dataset** — AI catches ~70% of mistakes vs human labels

## Writing Coach

Breaks essay writing into stages: outlining, drafting, revision. Khanmigo provides feedback at each step and refuses to write content for students. Teachers have full access to conversation history to verify student work was genuine, not AI-generated.

## Teacher Trust Mechanism

- Conversation history for teachers to validate student work
- Detecting text that "showed up out of nowhere"
- Similar guardrails for coding
- Classroom snapshots: class progress, skills reports
- Ability to generate progress reports for families
- Moderation features for inappropriate conversations

## AI-First Organization Transformation

Khan Academy drew from "Creative Selection" (iPhone development):
- Pair builders with domain experts
- Run demos to identify what works
- End demos that don't

**New core values added:**
- "Trust your intuition"
- "Resist perfectionism to deliver wow"

**Code quality tiering:** Prototype code follows different standards than code shipped to all users.

**AI Platform Team:** Bridge between infrastructure and product teams — owns AI developer experience, prompt engineering interfaces, and AI routing.

## Technical Hurdles

### 1. Tutoring Accuracy
- Chain of Thought prompting
- RAG for additional context
- Model-graded evaluations (still ~70% accuracy vs human labels)

### 2. Prompt Engineering
- Evolved from spaghetti code to component architecture
- Clearly defined inputs and outputs
- Active MVI test suite

### 3. Scale / Performance / Cost
- Multiple models with fallback to shared capacity
- Perceived performance improvements in UI
- Microsoft Azure LLM compute donation
- Next: load balancing between OpenAI and Azure, evaluating smaller models, dynamic compute scaling

## Key Quote

> "We're really not just trying to use AI for AI's sake" — Khan Academy's philosophy: every AI implementation serves the mission of helping students who thought they were bad at math or hated learning discover a different relationship with education.
