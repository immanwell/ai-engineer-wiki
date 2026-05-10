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

## 2026-04-29

**Source ingested**: `AI Engineer Chapter 2 (Chip Huyen, 2025).md` (GitHub chapter-summaries.md)

**Pages created**:
- `rlhf.md` — RLHF: SFT + preference finetuning, post-training alignment
- `scaling-laws.md` — Parameters, training tokens, FLOPs, compute budget tradeoffs
- `transformer-limitations.md` — Context limits, hallucinations, symbolic reasoning gaps
- `foundation-model-evaluation.md` — Evaluation as first step in systematic AI engineering (Ch3+4 to expand)

**Updated**: `wiki/index.md` with new pages and one-line descriptions

## 2026-05-04

**Source ingested**: `AI Engineer Chapter 3 (Chip Huyen, 2025).md` + `AI Engineer Chapter 4 (Chip Huyen, 2025).md` (GitHub chapter-summaries.md)

**Pages created**:
- `functional-correctness.md` — Exact evaluation: binary pass/fail on whether AI produces correct output
- `ai-as-a-judge.md` — Subjective evaluation: AI judges score other AI outputs, judge-dependent and context-specific
- `build-vs-buy-ai.md` — 7 axes decision framework: data privacy, performance, control, cost for API vs self-host
- `private-model-selection.md` — Public benchmarks contaminated; model selection = creating a private leaderboard

**Updated**: `foundation-model-evaluation.md` — expanded stub with Ch3 + Ch4 content
**Updated**: `wiki/index.md` with 4 new pages and one-line descriptions

**Also**: Created `preference-models.md` — referenced in ai-as-a-judge but had no dedicated page

## 2026-05-05

**Source ingested**: `Chip Huyen's Evaluation-Driven Development (EDD) framework from AI Engineering.md` (Medium article by Keerthanams, summarizing Ch4)

**Pages created**:
- `evaluation-driven-development.md` — EDD framework: 4 evaluation pillars, model selection workflow, pipeline building, meta-evaluation

**Updated**: `wiki/index.md` with new page and one-line description

## 2026-05-05 (Evening)

**Updated**: `wiki/ai-native-engineer.md` — added practical Claude Code workflow example (3-step implementation with URL shortener)

## 2026-05-06

**Source ingested**: `AI Engineer Chapter 5 (Chip Huyen, 2025).md` (GitHub chapter-summaries.md)

**Updated**: `wiki/prompt-engineering.md` — added Ch5 content: Prompt Anatomy (4 components), In-Context Learning (ICL)

**Pages created**:
- `prompt-attacks.md` — Prompt injection, jailbreaking, indirect injection, defenses

**Updated**: `wiki/index.md` with new page and updated prompt-engineering description

## 2026-05-06 (Evening)

**Source ingested**: `Code with Claude 2026 Opening Keynote.md` (transcript shared by user)

**Pages created**:
- `advisory-strategy.md` — Executor (Sonnet) + Advisor (Opus) pattern: 5x lower cost, 63.4% accuracy (up from 59.6%)

**Updated**:
- `wiki/index.md` — added advisory-strategy entry
- `wiki/ai-tutor.md` — freemium tiers mapped to Advisory Strategy (Free=Sonnet only, Paid=Sonnet+Opus Advisor)

## 2026-05-10

**Source ingested**: `AI Engineer Chapter 6 (Chip Huyen, 2025).md` (GitHub chapter-summaries.md)

**Pages created**:
- `rag-retrieval.md` — RAG: 2-step retrieve-then-generate, retriever types (term vs embedding), vector search foundations
- `agent-memory.md` — Agent memory systems: working/episodic/semantic memory, reflection, progress tracking

## 2026-05-10 (Evening)

**Sources ingested**: Three Zilliz RAG/embedding documents from `raw/`

**Updated**:
- `wiki/rag-retrieval.md` — expanded with Vector Embedding Types (dense/sparse/binary), embedding models table (Word2Vec, GloVe, BERT, CLIP, ColBERT, SPLADE, BGE-M3, TF-IDF), embedding creation methods (neural networks, matrix factorization), best practices and pitfalls, chunking strategies (fixed-size vs content-aware vs recursive), chunk size guidance, LangChain code example
- Changed status from `stub` to `stable`

**Raw files reviewed** (kept in raw/ as reference):
- `Everything You Need to Know about Vector Index Basics.md` — FAISS-level detail, too deep for exam prep
- `An Introduction to Vector Embeddings_ What They Are and How to Use Them.md` — used for embedding types + models
- `A Beginner's Guide to Website Chunking and Embedding for Your RAG Applications.md` — used for chunking strategies

**Source ingested**: `The Capability Curve.md` (Code with Claude 2026, Session 5)

**Pages created**:
- `the-capability-curve.md` — Capability curve concept, SweeBench 62%→87%, demo (Sonnet 4 vs Opus 4.7), three model gains (planning, error recovery, attention), three tips (evals, shrink scaffolding, give model room), customer results (Vercel, WinServ, Shopify)

**Updated**:
- `wiki/index.md` — added the-capability-curve entry

**Raw saved**: `The Capability Curve.md` (transcript from user)

**Source ingested**: `The Expanding Toolkit.md` (Code with Claude 2026, Session 4)

**Pages created**:
- `the-expanding-toolkit.md` — Tool use (routers dead), context management (1M, prune stale), code execution (hosted sandbox, two computers), computer use (1440p native, 78% OS World), key rule on compensating vs connecting code

**Updated**:
- `wiki/context-reliability.md` — added prune stale tool results tip, 1M context at flat pricing
- `wiki/tool-design-mcp.md` — added output schema in tool description tip
- `wiki/claude-code.md` — added pre/post tool hooks, `/schedule`, slash context, Claude in Chrome extension
- `wiki/agentic-architecture.md` — added two computers mental model for sandbox vs local bash
- `wiki/index.md` — added the-expanding-toolkit entry

**Raw saved**: `The Expanding Toolkit.md` (Gemini-formatted digest)

**Source ingested**: `How to Get to Production Faster with Claude Managed Agents.md` (Code with Claude 2026, Gemini-formatted transcript)

**Pages created**:
- `claude-managed-agents.md` — Managed infrastructure for agents: 3 pillars, State Store, Event Topology, Outcomes, Multiagent Orchestration

## 2026-05-10 (Session 3)

**Source ingested**: `Designing Memory Systems for Self-Learning Agents.md` (Code with Claude 2026, Gemini transcript)

**Updated**:
- `agent-memory.md` — Expanded with Ch6 + Claude 2026 session 3: file system memory model, permission scopes, optimistic concurrency, Dreaming deep-dive (6x Harvey improvement, 90% Roktun mistake reduction), three-layer framework

**Raw saved**: `Designing Memory Systems for Self-Learning Agents.md` (Gemini-formatted digest)