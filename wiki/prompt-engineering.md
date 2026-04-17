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

**Sources**: [[raw/instructor-8lsy243ftffjjy1cx9lm3o2bw-public-1773274827-Claude+Certified+Architect+–+Foundations+Certification+Exam+Guide.pdf|architect exam guide]]

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

```
You are a senior software architect reviewing pull requests.
Focus on: security, scalability, and maintainability.
```

### Chain-of-thought prompting

Encourage the model to show reasoning before answering:

```
First, explain your reasoning. Then provide the answer.
```

This improves accuracy on complex multi-step problems.

### Few-shot examples

Provide examples of desired input-output pairs:

```
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

## Output formatting

### Structured outputs

Use clear delimiters and formatting instructions:

```
Return your response as:
1. **Summary** — one paragraph
2. **Key Points** — numbered list
3. **Next Steps** — actionable items
```

### Constraining format

For machine-readable outputs, specify exact schema:

```
Respond with valid JSON: {"title": string, "priority": "high"|"medium"|"low"}
```

## Exam relevance

Expected to understand:
- Role and persona techniques
- Chain-of-thought for complex reasoning
- Few-shot example design
- System vs. user prompt boundaries
- Context window management

## Related pages

- [[agentic-architecture]] — prompt techniques in agentic loops
- [[claude-code]] — Claude Code's system prompt handling
- [[context-reliability]] — context window management