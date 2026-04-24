---
title: "Khanmigo Scaling Case Study"
aliases:
  - "khanmigo scale"
tags:
  - wiki
  - "agentic-architecture"
domain: "agentic-architecture"
sources:
  - "Khanmigo Scaling Case Study (Shawn Jansepar, 2024).md"
status: stub
confidence: high
---

Created: Friday, 24 April 2026, 13:57
Modified: `=dateformat(this.file.mtime, "DDDD, HH:mm")`

---

# Khanmigo Scaling Case Study

**Summary**: Khan Academy's Director of AI and Learning (Shawn Jansepar) on scaling Khanmigo to 200K users — math agent architecture (CoT + RAG), Writing Coach, AI-first org transformation, and technical hurdles. Validates the AI tutor model at real scale.

**Sources**: [[raw/Khanmigo Scaling Case Study (Shawn Jansepar, 2024).md|Khanmigo Scaling Case Study]]

---

## Scale

- ~200,000 Khanmigo learners and teachers
- ~50% from school districts serving under-resourced communities
- Post-pandemic gap: average 8th grader is 1.1 grade levels behind

## Socratic Method as North Star

Khan Academy's North Star is emulating human tutors. Khanmigo asks leading questions rather than giving answers. Concrete differentiation from ChatGPT: when a student incorrectly distributed -4, ChatGPT validated the wrong answer. Khanmigo caught the specific mistake and guided the student back.

## Math Agent Architecture

A specialized math agent handles complex problems with:
- **Chain of Thought prompting** — reasons through how a student arrived at an answer before tutoring
- **RAG** — retrieves additional context
- **Autonomy** to use calculators or Python
- **Accuracy dashboard** — monitors quality over time
- AI catches ~70% of mistakes vs human labels

## Writing Coach

Breaks essay writing into stages: outlining → drafting → revision. Khanmigo provides feedback at each stage and refuses to write content for students. Teachers can review full conversation history to verify student work is genuine.

## AI-First Organization Transformation

From "Creative Selection" (iPhone development):
- Pair builders with domain experts who deeply understand customers
- Run demos to identify what works, end demos that don't

**New core values:**
- "Trust your intuition"
- "Resist perfectionism to deliver wow"

**Code quality tiering:** Prototype code and shipped code follow different standards.

**AI Platform Team:** Owns AI developer experience, prompt engineering interfaces, and model routing — bridges infrastructure and product.

## Technical Hurdles and Solutions

| Problem | Solution |
|---|---|
| Math tutoring accuracy | Math agent + CoT prompting + RAG + accuracy dashboard |
| Prompt spaghetti | Component architecture, MVI test suite |
| Scale/performance/cost | Multi-model routing, Azure donation, dynamic scaling |

## Key Quote

> "We're really not just trying to use AI for AI's sake" — every AI implementation must serve the mission of helping students discover a different relationship with education.

## Related Pages

- [[ai-tutor]]
- [[socratic-tutoring]]
- [[ai-engineering-discipline]]
