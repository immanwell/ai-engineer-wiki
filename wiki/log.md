---
title: "LLM Wiki Log"
tags:
  - wiki
  - log
domain: certification
status: stable
confidence: high
---
Created: Friday, 15 April 2026, 12:13
Modified: `=dateformat(this.file.mtime, "DDDD, HH:mm")`

---
# LLM Wiki — Log

Append-only record of all wiki operations.

## 2026-04-15

**Source ingested**: `instructor-8lsy243ftffjjy1cx9lm3o2bw-public-1773274827-Claude+Certified+Architect+–+Foundations+Certification+Exam+Guide.pdf`

**Pages created**:
- `claude-certified-architect-foundations-exam-guide.md` — Exam overview with domain breakdown table
- `agentic-architecture.md` — Agentic loop, multi-agent patterns, Claude Messages API, parallelism
- `tool-design-mcp.md` — MCP protocol, tool design principles, server/client architecture, transport types
- `claude-code.md` — Configuration, hooks, git workflow, multi-agent worktrees, MCP integration
- `prompt-engineering.md` — Techniques: chain-of-thought, few-shot, role assignment, output formatting
- `context-reliability.md` — Token management, cache_control, truncation vs summarization

**Updated**: `wiki/index.md` with all new pages and one-line descriptions

**Emphasis**: Domains 1–3 (Agentic Architecture 40%, Tool Design & MCP 30%, Claude Code 20%) given highest depth per user request.

## 2026-04-16

**Source ingested**: `anthropic-agents-to-skills.md` (YouTube, dotta, summarized via summarize CLI)

**Pages created**:
- `skills-anthropic.md` — Skills as organized knowledge collections, progressive disclosure design, skills + MCP architecture, computing stack analogy, organizational compounding
- `agent-vs-expert-problem.md` — The gap between agent intelligence and domain expertise that skills aim to fill

**Updated**: `wiki/index.md` with new pages and one-line descriptions

**Source ingested**: `paperclip-agent-orchestrator.md` (YouTube, dotta, summarized via summarize CLI)

**Pages created**:
- `agent-orchestration-patterns.md` — Hierarchical delegation (org chart), human control plane, QA review gates, reusable routines, skills auto-discovery. Uses Paperclip as concrete case study.

**Updated**: `wiki/index.md` with new page and one-line description

## 2026-04-17

**Source ingested**: `mihail-eric-junior-engineers-crisis.md` (YouTube, Stanford talk by Mihail Eric, summarized via summarize CLI)

**Pages created**:
- `mihail-eric-junior-engineers-crisis.md` — Main summary: perfect storm facing junior devs, AI-native engineer profile, agent-friendly codebase principles
- `ai-native-engineer.md` — Context switching across agents, building one workflow at a time before scaling
- `agent-friendly-codebase.md` — Tests as contracts, README-code consistency, error compounding warnings
- `junior-engineer-advantage.md` — "Good naivety" and healthy arrogance as structural AI adoption advantages
- `software-taste.md` — "The last mile" where taste develops after functional correctness

**Updated**: `wiki/index.md` with all new pages and one-line descriptions

**Also**: Created `socratic-tutoring.md` — linked from `ai-tutor` and `index.md`

## 2026-04-23

**Source ingested**: `AI Engineer Chapter 1 (Chip Huyen, 2025).md` (GitHub chapter-summaries.md, Chip Huyen)

**Pages created**:
- `ai-engineering-ch1.md` — Main summary: evolution arc, AI engineering as discipline, pre-build question
- `ai-engineering-discipline.md` — Discipline framing vs toolbox, framework for overwhelm, should-you-build-it
- `ai-engineering-vs-ml-engineering.md` — Model as component, probabilistic evaluation, human-AI interaction as product
- `generative-ai-use-cases.md` — Table 1-3: 8 categories consumer vs enterprise
- `ai-tutor.md` — Product concept: UG mathematics tutor with NCDC curriculum moat
- `tax-preparer.md` — Product concept: UG tax assistant with URA regulations moat

**Updated**: `wiki/index.md` with all new pages and one-line descriptions

## 2026-04-23 (Evening)

**Source ingested**: `Matt Pocock Software Fundamentals AI Age (2025).md` (YouTube, Matt Pocock, summarized via summarize CLI)

**Pages created**:
- `pocock-software-fundamentals.md` — Core thesis: bad code is most expensive in AI workflows, 6 failure modes, deep modules, feedback loops
- `deep-modules.md` — Ousterhout's deep module architecture as ideal for AI: simple interfaces, tested boundaries

**Updated**: `wiki/index.md` with new pages and one-line descriptions

**Also**: Added workflow patterns section to `claude-code.md` — plan mode workflow, phased planning, context preservation via GitHub issues, memory rules

## 2026-04-24

**Source ingested**: `Khanmigo Scaling Case Study (Shawn Jansepar, 2024).md` (YouTube, Shawn Jansepar, summarized via summarize CLI)

**Pages created**:
- `khanmigo-scaling-case-study.md` — Scale proof (200K users), math agent (CoT + RAG), Writing Coach, AI-first org transformation, technical hurdles

**Updated**: `ai-tutor.md` and `socratic-tutoring.md` sources to include new Khanmigo case study

## 2026-04-24 (Evening)

**Source ingested**: `Superset Workflow Kiet (2024).md` (YouTube, summarized via summarize CLI)

**Pages created**:
- `superset-workflow.md` — 5-stage manufacturing pipeline (trigger/plan/coding/review/merge), throughput bottleneck, token allocation problem

**Updated**: `log.md`