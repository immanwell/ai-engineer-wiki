---
title: "Context Reliability"
aliases:
  - context-reliability
  - context-management
  - token-optimization
  - cache-management
tags:
  - wiki
  - context-reliability
domain: certification
sources:
  - "instructor-8lsy243ftffjjy1cx9lm3o2bw-public-1773274827-Claude+Certified+Architect+–+Foundations+Certification+Exam+Guide.pdf"
status: stable
confidence: high
date_created: 2026-04-15
date_modified: 2026-04-15
---

# Context Reliability

**Summary**: Ensuring AI systems remain accurate and efficient as conversations grow long and context windows fill up. Covers token budget management, cache optimization, and context truncation strategies.

**Sources**: (source: instructor-8lsy243ftffjjy1cx9lm3o2bw-public-1773274827-Claude+Certified+Architect+–+Foundations+Certification+Exam+Guide.pdf)

---

## Overview

Context reliability is the smallest exam domain at **5%** (4 questions), but managing context is critical in production agentic systems. Token limits and cache behavior directly affect system cost and performance.

## Token management

### Token budgets

Claude models have maximum context windows (e.g., 200K tokens for Claude Sonnet 4). Beyond the limit, you must:

- **Truncate** — remove older messages
- **Summarize** — compress context with an LLM call
- **Segment** — split long conversations into chapters

### Rolling context pattern

For long conversations:
1. Keep the most recent turns (last N messages)
2. Discard older turns but preserve key facts
3. Maintain a persistent system prompt with essential context

### Token counting

- ~4 characters per token (English average)
- API responses include `usage` with token counts
- Plan for both input and output tokens in your budget

## Cache management

### Prompt caching

Anthropic's `cache_control` attribute marks content as cacheable:

```json
{
  "content": "Large system prompt text...",
  "cache_control": {"type": "ephemeral"}
}
```

Caching reduces costs on repeated context.

### Cache invalidation

- Ephemeral caches last for the session
- Longer-term caching requires explicit configuration
- Changes to cached content require cache refresh

## Context overflow strategies

### Hybrid approach

Combine recent conversation with retrieved context:

```
[system prompt] + [retrieved docs] + [recent messages]
```

Use semantic search to pull relevant docs, discard irrelevant ones.

### Truncation strategies

- **Naive**: Drop oldest messages first
- **Smart**: Retain milestone messages (decisions, key facts)
- **Semantic**: Use embeddings to decide what to keep

### Summarization

For very long contexts:
1. Identify key facts and decisions in the conversation
2. Use an LLM to generate a summary
3. Replace the full history with the summary + recent turns

## Exam relevance

Expected to understand:
- Token budget implications of long conversations
- Cache control and ephemeral caching
- Truncation vs. summarization trade-offs
- Hybrid context approaches (recent + retrieved)

## Related pages

- [[agentic-architecture]] — context in agentic loops
- [[prompt-engineering]] — context optimization techniques
- [[claude-certified-architect-foundations-exam-guide]] — exam overview