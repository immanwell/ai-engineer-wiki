---
title: "Build vs Buy AI"
aliases:
  - "host model vs API"
  - "model deployment decision"
  - "self-host vs model API"
tags:
  - wiki
  - "context-reliability"
domain: "context-reliability"
sources:
  - "AI Engineer Chapter 4 (Chip Huyen, 2025).md"
status: stub
confidence: high
---

Created: Monday, 4 May 2026, 14:30
Modified: `=dateformat(this.file.mtime, "DDDD, HH:mm")`

---

# Build vs Buy AI

**Summary**: The key decision for application developers: use a model API (buy) or self-host a model (build). Chip Huyen outlines 7 axes for this decision — data privacy, data lineage, performance, functionality, control, and cost.

**Sources**: [[raw/AI Engineer Chapter 4 (Chip Huyen, 2025).md|AI Engineering Chapter 4]]

---

## The 7 Axes

| Axis | What It Means |
|---|---|
| **Data Privacy** | Can your data leave your infrastructure? |
| **Data Lineage** | Do you know where data flows? |
| **Performance** | Latency, throughput, reliability |
| **Functionality** | Does the model support what you need? |
| **Control** | Can you customize/improve the model? |
| **Cost** | API pricing vs. infrastructure cost |
| *(implied)* | Safety, compliance, customization |

## Model API (Buy)

**Pros:**
- Fast to deploy
- Managed infrastructure
- Access to frontier models
- Lower upfront cost

**Cons:**
- Data leaves your infrastructure
- Less control over model behavior
- Rate limits, API costs at scale

## Self-Host (Build)

**Pros:**
- Full data privacy
- Full control over model
- Customize for domain

**Cons:**
- Infrastructure complexity
- GPU costs
- Need ML expertise to run

## The Decision

Like all build vs buy decisions: unique to every team, depending on what the team needs and what the team wants.

## Related Pages

- [[foundation-model-evaluation]]
- [[ai-tutor]] — relevant for the tutor product (data privacy for student data)
