---
title: "AI Tutor"
aliases:
  - "mathematics tutor"
  - "AI powered study coach"
  - "Coach Salish"
tags:
  - wiki
  - product
domain: "product"
sources:
  - "AI Engineer Chapter 1 (Chip Huyen, 2025).md"
  - "At Duolingo, humans and AI work together to create a high-quality learning experience.md"
  - "Coach Salish Gem.md"
  - "Khan Academy Khanmigo Demo (Sal Khan, 2024).md"
status: stub
confidence: medium
---

Created: Thursday, 23 April 2026, 06:37
Modified: `=dateformat(this.file.mtime, "DDDD, HH:mm")`

---

# AI Tutor — Product Blueprint

**Summary**: An AI-powered personalized study coach for the Ugandan NCDC curriculum, combining Khanmigo's Socratic tutoring architecture, Duolingo's personalization framework, and Coach Salish's persona-driven engagement layer — built as a Skill.md driven agent with real tool execution.

**Sources**: [[raw/AI Engineer Chapter 1 (Chip Huyen, 2025).md|AI Engineering Ch1]] · [[raw/At Duolingo, humans and AI work together to create a high-quality learning experience.md|Duolingo AI]] · [[raw/Coach Salish Gem.md|Coach Salish Gem]] · [[raw/Khan Academy Khanmigo Demo (Sal Khan, 2024).md|Khanmigo Demo]]

---

## Product Overview

**Type**: EdTech / AI Tutor
**Curriculum**: Uganda NCDC (National Curriculum Development Centre)
**Target Users**: All primary and secondary students in Uganda, with dashboards for teachers and parents/guardians
**Primary Moat**: UG-specific curriculum + persona characters + real tool execution

## Reference Implementations

### Khanmigo (Khan Academy)
Reference: [Khan Academy Khanmigo Demo](https://youtu.be/rnIgnS8Susg)

What it does:
- Socratic tutoring — guides students to answers without giving them away
- Works across all subjects and content types
- "Recorded and viewable by your teacher" — safety built in
- Teacher dashboards: lesson plans, exit tickets, student oversight
- Parent/guardian visibility — not a black box
- Connects to student interests for personalized relevance

What it lacks:
- No persona/character layer
- No UG curriculum specificity
- No custom character selection for kids

### Duolingo (Bicknell & Pajak, 2022)
Four stages of course creation:

| Stage | Human | AI | Notes |
|---|---|---|---|
| Curriculum Design | High | Low | NCDC humans do this |
| Raw Content Creation | High | Medium | Lesson content, examples |
| Exercise Creation | Medium | High | Practice problems |
| Lesson Personalization | Low | **Highest** | **AI's sweet spot** |

Lesson personalization (Stage 4) is where AI adds the most value — per-learner adaptation based on tracked gaps.

### Coach Salish Gem
The working prototype — a Gemini Gem for tutoring Asma (P6, 16 years old).

What worked:
- Socratic tutoring protocol (never give answers)
- Subject-specific methods (place value chart, "physical" science approach)
- Session structure: Equipment Check → Gameplay → Verification
- Gamification: Boss Battles, Challenges, Burnout Guard
- Detailed student profile with curriculum context

What broke:
- Gmail integration — Gemini can't send emails on command
- Google Calendar — check at session start, never fired
- Google Docs appends — required manual steps, not automatic
- JSON data export — instructions only, no execution

**The core problem**: Gems run in a black box with no real tool execution. Coach Salish needed an agent pipeline, not a chat interface.

---

## Architecture

### Skill.md as the Source of Truth

The tutor persona, rules, student profile, and workflows go into a `skill.md` file. This drives an agent (not a chat interface) that has real tool execution.

```
skill.md (persona, rules, profile) → Agent (Claude) → Real tools (Gmail, Calendar, Docs)
```

### Persona Layer (Coach Salish Pattern)

Each student chooses a character tutor (e.g., Salish, Ben10, Kaylus). The character maintains consistent persona across all interactions. This is the engagement differentiator — kids stay motivated through character loyalty.

Characters are built as Skills with:
- Persistent personality and tone
- Subject-specific teaching methods
- Engagement hooks (zombies, challenges, etc.)

### The Learning Loop

```
Phase 1: Equipment Check → Assess prior knowledge
Phase 2: Turn-Based Gameplay → One question at a time
Phase 3: Collab Cam → Student explains concept in their own words
Phase 4: Boss Battle → Quiz to verify mastery
```

### Tool Execution (What Coach Salish Needed)

The agent must execute:
- **Gmail**: Session wrap report to guardian, weekly school report to teacher
- **Google Calendar**: Check schedule at session start, populate weekly lineup
- **Google Docs**: Append to Strategy Guide (cheat codes), Battle Log (quiz feedback)
- **JSON export**: Structured data for student profile, gaps, progress

### NCDC Curriculum Integration

The skill.md knows:
- Current class and term
- School calendar (UG terms)
- Subject topics per level
- Student profile and struggle areas

This is loaded dynamically — not hardcoded in prompts.

---

## Business Model

| Tier | Price | Features |
|---|---|---|
| Free | Ads + Groq | 30 min/day, basic characters |
| Individual | Paid | Best models, no limits, all characters, dashboards |
| School/Group | Paid | Bulk subscriptions, teacher/admin dashboards |

- Family plan: 3+ children at reduced rate
- School-wide: teacher + student access

---

## Open Questions

1. **Agent vs API keys** — Use API keys for reasoning models (Claude, GPT-4), Groq for fast inference on simple paths, and an agent framework for multi-step tutoring interactions
2. **Skills for character personas** — Each tutor character is a separate Skill with its own system prompt
3. **User research** — Questionnaire for pain points (student vs teacher vs parent)
4. **Video generation** — Remotion for on-demand concept explanation videos

---

## Related Pages

- [[tax-preparer]]
- [[generative-ai-use-cases]]
- [[ai-engineering-ch1]]
