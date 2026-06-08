---
title: "Dataset Engineering"
aliases:
  - "training data"
  - "synthetic data"
  - "data annotation"
  - "instruction data"
tags:
  - wiki
  - "context-reliability"
domain: "context-reliability"
sources:
  - "AI Engineer Chapter 8 (Chip Huyen, 2025).md"
status: stable
confidence: high
---

Created: Monday, 8 June 2026, 21:52
Modified: `=dateformat(this.file.mtime, "DDDD, HH:mm")`

---

# Dataset Engineering

**Summary**: Dataset engineering is the discipline of designing, acquiring, and evaluating training data. The process begins by thinking through what behaviors you want the model to learn — the rest follows. Data quality, coverage, and diversity consistently matter more than raw size.

**Sources**: [[raw/AI Engineer Chapter 8 (Chip Huyen, 2025).md|AI Engineering Chapter 8]]

---

## The Three Core Criteria

Every training dataset — regardless of phase — is evaluated against the same three dimensions:

| Criterion | What It Means | Why It Matters |
|-----------|---------------|----------------|
| **Quality** | Data is accurate, clean, and representative of desired behavior | Noisy data teaches wrong behaviors |
| **Coverage** | Data spans the full range of inputs the model will encounter | Gaps in coverage = failure modes in production |
| **Quantity** | Enough examples for the model to generalize | More isn't always better — see below |

**Key principle**: A small amount of high-quality, diverse data consistently outperforms a large amount of noisy data. Teams that increase dataset diversity often see larger performance gains than teams that simply add more examples.

## Data by Training Phase

Different training phases require different data types:

| Phase | Data Type | Example |
|-------|-----------|---------|
| **Pre-training** | Massive raw text corpus | Web crawls, books, code |
| **SFT / Instruction finetuning** | (Prompt, ideal response) pairs | Curated demonstrations of helpful behavior |
| **Preference finetuning (RLHF)** | Ranked response pairs | Human A/B comparisons of two model outputs |

The same quality/coverage/quantity criteria apply across all three phases, but what constitutes "quality" differs per phase.

## Synthetic Data

Because high-quality annotated data is expensive and slow to acquire, teams increasingly use AI to generate training data — synthetic data.

### What It Is

Synthetic data is training data generated programmatically, often by another AI model. The most common use case is generating instruction data for finetuning:

```txt
Seed prompt → AI generates (instruction, response) pairs → Filter/evaluate → Train
```

### Why It Works Now

Generating realistic, complex training data wasn't practical before foundation models. LLMs can now produce diverse, plausible instruction data at scale — making synthetic data a mainstream solution rather than a niche experiment.

### The Evaluation Requirement

Synthetic data must be evaluated before use. Skipping this step introduces the same failure modes as using noisy real data — and the evaluation challenge is identical to evaluating any other AI output.

> Evaluating AI-generated data is just as tricky as evaluating other AI outputs. People are more likely to use generated data they can reliably evaluate.

See [[ai-as-a-judge]] for evaluation approaches — these apply directly to synthetic data validation.

## The Non-Automatable Parts

A recurring theme in dataset engineering: **the hardest parts resist automation**.

| Task | Automatable? | Why Not |
|------|-------------|---------|
| Generating more data | Yes (synthetic) | — |
| Annotating data | Partially | Human judgment required for edge cases |
| Writing annotation guidelines | No | Requires deep domain + task understanding |
| Deciding what behaviors to teach | No | Strategic product decision |
| Verifying generated data | Partially | Ground truth often doesn't exist |

The practical implication: dataset work scales with human attention, not just compute. Dedicated data roles (data engineers focused on AI training data) are becoming standard on AI teams.

## Dataset Design Thinking

The process starts before any data is collected:

1. **Define target behaviors** — What should the model do that it doesn't do now?
2. **Identify failure modes** — Where does the current model fall short?
3. **Design examples that demonstrate the desired behavior**
4. **Set annotation guidelines** — What makes a response good vs bad for this task?
5. **Collect, generate, or synthesize data**
6. **Evaluate data quality** before training

Skipping step 4 (annotation guidelines) is the most common source of noisy training data — annotators make inconsistent decisions without clear criteria.

## Connection to Finetuning

Dataset engineering is the upstream dependency for [[finetuning]]. The observation that "finetuning is easy, getting data is hard" is what Chapter 8 unpacks. The PEFT/LoRA techniques in Chapter 7 are constrained by data availability just as much as by compute.

## Related Pages

- [[finetuning]] — how the dataset is used in PEFT/LoRA training pipelines
- [[rlhf]] — preference finetuning data (ranked pairs) is a specific dataset engineering problem
- [[ai-as-a-judge]] — AI evaluation techniques apply directly to synthetic data validation
- [[foundation-model-evaluation]] — same evaluation rigor applies to training data as to model outputs
- [[rag-retrieval]] — RAG is often preferred when dataset engineering cost is too high
