---
title: "LLM Wiki Index"
tags:
  - wiki
  - index
domain: certification
status: stable
confidence: high
---
Created: Friday, 15 April 2026, 12:13
Modified: `=dateformat(this.file.mtime, "DDDD, HH:mm")`

---
# LLM Wiki — Index

A curated knowledge base for the Claude Certified Architect – Foundations exam.

## Exam Guide

- [[claude-certified-architect-foundations-exam-guide]] — Exam overview, domains, format

## Core Domains

- [[agentic-architecture]] — 40% of exam — Multi-agent systems, tool use, context management
- [[agent-orchestration-patterns]] — Case studies in hierarchical delegation, human control plane, QA gates, routines
- [[skills-anthropic]] — Skills as organized knowledge collections, progressive disclosure, MCP integration
- [[tool-design-mcp]] — 30% of exam — MCP protocol, tool design patterns
- [[claude-code]] — 20% of exam — CLI tool, hooks, git workflow, MCP integration

## Supporting Domains

- [[prompt-engineering]] — 5% of exam — Crafting inputs to reliably produce desired outputs (Ch5 expanded)
- [[prompt-attacks]] — Prompt injection, jailbreaking, and defenses — security risks from following instructions
- [[context-reliability]] — 5% of exam — Token management, cache optimization

## Core Concepts

- [[agent-vs-expert-problem]] — Why agents need domain expertise beyond raw intelligence
- [[mihail-eric-junior-engineers-crisis]] — Stanford talk: AI-native engineer skills, agentic codebase design, junior dev advantage
- [[ai-native-engineer]] — Context switching across agents, building workflows incrementally
- [[the-expanding-toolkit]] — Session 4: tool routing, 1M context, hosted sandbox, computer use 1440p native (Code with Claude 2026)
- [[the-capability-curve]] — Session 5: capability curve, planning/error recovery/attention gains, 3 tips (evals, simplify scaffolding, give model room)
- [[advisory-strategy]] — Executor (Sonnet) + Advisor (Opus) pattern: frontier quality at 5x lower cost (Claude 2026 keynote)
- [[claude-managed-agents]] — Managed infrastructure for agents: sandboxing, state store, retries, Event Topology, Outcomes (Public Beta)
- [[agent-friendly-codebase]] — Tests as contracts, documentation consistency, error compounding
- [[junior-engineer-advantage]] — "Good naivety" and healthy arrogance as AI adoption strengths
- [[software-taste]] — "The last mile" differentiator in software quality
- [[ai-engineering-ch1]] — Chip Huyen Ch1: intro to AI engineering as a discipline
- [[ai-engineering-discipline]] — Discipline framing vs toolbox — judgment calls, not just tools
- [[ai-engineering-vs-ml-engineering]] — Model as component, probabilistic evaluation, human-AI interaction
- [[generative-ai-use-cases]] — Table 1-3: 8 categories consumer vs enterprise
- [[ai-tutor]] — Product concept: UG mathematics tutor with NCDC curriculum moat
- [[socratic-tutoring]] — Teaching method: guide students to answers, never give them away
- [[pocock-software-fundamentals]] — Software fundamentals beat AI hype: feedback loops, deep modules, ubiquitous language
- [[deep-modules]] — Ousterhout's architecture ideal for AI: simple interfaces, tested boundaries, gray-box internals
- [[rlhf]] — Reinforcement Learning from Human Feedback: post-training alignment, SFT + preference finetuning
- [[scaling-laws]] — Parameters, training tokens, FLOPs: the 3 numbers that define model scale
- [[transformer-limitations]] — Context limits, hallucinations, symbolic reasoning gaps, and agentic implications
- [[rag-retrieval]] — RAG: 2-step retrieve-then-generate pattern, retriever types (term vs embedding-based), vector search foundations
- [[agent-memory]] — Agent memory systems: working, episodic, semantic memory; reflection and progress tracking
- [[foundation-model-evaluation]] — Evaluation as the first step in systematic AI engineering (Ch3 + Ch4 complete)
- [[functional-correctness]] — Exact evaluation: binary pass/fail on whether AI produces correct output
- [[ai-as-a-judge]] — Subjective evaluation: AI judges score other AI outputs, judge-dependent and context-specific
- [[preference-models]] — Specialized AI judges trained to predict which response users prefer
- [[private-model-selection]] — Public benchmarks contaminated; model selection = creating a private leaderboard
- [[build-vs-buy-ai]] — 7 axes decision framework: data privacy, performance, control, cost for API vs self-host
- [[tax-preparer]] — Product concept: UG tax assistant with URA regulations moat
- [[khanmigo-scaling-case-study]] — Khan Academy scaling Khanmigo to 200K: math agent architecture, AI-first org, technical hurdles
- [[finetuning]] — When to finetune vs RAG, full vs PEFT, LoRA, quantized training, model merging (Ch7)
- [[dataset-engineering]] — Three criteria (quality/coverage/quantity), data phases, synthetic data, annotation challenges (Ch8)
- [[inference-optimization]] — TTFT/TPOT metrics, latency/throughput tradeoff, model-level and service-level techniques, top-4 most impactful (Ch9)
- [[ai-application-architecture]] — Common generative AI architecture: model gateway, guardrails, context construction, observability, data flywheel (Ch10)