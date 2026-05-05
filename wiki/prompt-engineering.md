---
title: "Prompt Engineering"
aliases:
  - prompt-engineering
  - prompt-techniques
tags:
  - wiki
  - prompt-engineering
domain: certification
sources:
  - "instructor-8lsy243ftffjjy1cx9lm3o2bw-public-1773274827-Claude+Certified+Architect+–+Foundations+Certification+Exam+Guide.pdf"
status: stable
confidence: high
---
Created: Friday, 15 April 2026, 18:54
Modified: `=dateformat(this.file.mtime, "DDDD, HH:mm")`

---
# Prompt Engineering

**Summary**: The practice of crafting inputs to language models to reliably produce desired outputs. Covers techniques for instruction clarity, context management, output formatting, and controlling model behavior.

**Sources**: [[raw/instructor-8lsy243ftffjjy1cx9lm3o2bw-public-1773274827-Claude+Certified+Architect+–+Foundations+Certification+Exam+Guide.pdf|architect exam guide]] · [[raw/AI Engineer Chapter 5 (Chip Huyen, 2025).md|AI Engineering Chapter 5]]

---

## Overview

Prompt engineering is the smallest domain at **5% of the exam** (4 questions), but the techniques apply across all domains. Strong prompt design improves every agentic system.

## Core techniques

### Explicit instruction

- State what you want explicitly, not implicitly
- Use imperative verbs: "Analyze", "Summarize", "Generate"
- Specify format requirements: JSON, markdown, bullet points
- Include constraints: "limit to 100 words", "use simple language"

### Role assignment

Assigning a persona or role improves consistency:

```txt
You are a senior software architect reviewing pull requests.
Focus on: security, scalability, and maintainability.
```

### Chain-of-thought prompting

Encourage the model to show reasoning before answering:

```txt
First, explain your reasoning. Then provide the answer.
```

This improves accuracy on complex multi-step problems.

### Few-shot examples

Provide examples of desired input-output pairs:

```txt
Input: "The system crashed" → Output: {"severity": "high", ...}
Input: "Slow response time" → Output: {"severity": "medium", ...}
```

Examples should be representative and cover edge cases.

### System vs. user prompts

- **System prompt**: Persistent instructions across the entire conversation
- **User prompt**: Turn-by-turn input that can override or supplement system instructions

## Context optimization

### What to include

- Relevant background information
- Domain-specific terminology definitions
- Constraints and requirements
- Examples of desired output

### What to exclude

- Out-of-context information (adds noise)
- Contradictory instructions
- Ambiguous terms without definitions

## Prompt Anatomy (Ch5)

A well-structured prompt has four components:

| Component | What It Is | Example |
|-----------|-----------|---------|
| **Instruction** | The task you want performed | "Summarize this document" |
| **Context** | Background information the model needs | Relevant docs, prior conversation |
| **Examples** | Input-output pairs showing desired behavior | Few-shot demos |
| **Output format** | How you want the response structured | JSON, bullet points, markdown |

Clear instructions with relevant examples and context are essential — this applies whether communicating with AI or humans.

## In-Context Learning

In-context learning (ICL) is the model's ability to learn from examples *included in the prompt* — no fine-tuning required.

How it works:
1. **Pattern matching** — model recognizes the structure from examples
2. **Task recognition** — model identifies what task the examples demonstrate
3. **Prior knowledge** — model combines pattern matching with its pre-trained knowledge

ICL is why few-shot prompting works: the examples prime the model on format, tone, and reasoning patterns without changing the model's weights.

Key insight: if a small change in the prompt causes a big change in output, the model is sensitive to prompt structure — more crafting (examples, clearer instructions) will yield significant improvements.

## Output formatting

### Structured outputs

Use clear delimiters and formatting instructions:

```txt
Return your response as:
1. **Summary** — one paragraph
2. **Key Points** — numbered list
3. **Next Steps** — actionable items
```

### Constraining format

For machine-readable outputs, specify exact schema:

```json
{"title": string, "priority": "high"|"medium"|"low"}
```

## Exam relevance

Expected to understand:
- Role and persona techniques
- Chain-of-thought for complex reasoning
- Few-shot example design
- System vs. user prompt boundaries
- Context window management
- In-context learning (ICL) — how examples in prompts enable zero-shot task recognition

## Related pages

- [[agentic-architecture]] — prompt techniques in agentic loops
- [[claude-code]] — Claude Code's system prompt handling
- [[context-reliability]] — context window management
- [[prompt-attacks]] — prompt injection, jailbreaking, and defenses (Ch5 security)