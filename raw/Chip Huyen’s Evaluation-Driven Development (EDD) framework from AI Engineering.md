---
title: "Chip Huyen’s Evaluation-Driven Development (EDD) framework from AI Engineering:"
source: "https://medium.com/@keerthanams1208/chip-huyens-evaluation-driven-development-edd-framework-from-ai-engineering-a2939cc9ecf8"
author:
  - "[[Keerthanams]]"
published: 2025-07-26
created: 2026-05-04
description: "In traditional software, developers define success upfront does the system return the correct value, does it meet the latency budget, is it"
tags:
  - "clippings"
---
## Evaluation-Driven Development (EDD): Designing with the End in Mind

## Why Evaluation Should Lead the Way

In traditional software, developers define success upfront does the system return the correct value, does it meet the latency budget, is it scalable? But when it comes to AI systems, especially those built on large foundation models like GPT or Claude, outputs are probabilistic, not deterministic. That’s where Evaluation-Driven Development comes in. Instead of building an AI system and figuring out later how to judge it, EDD starts by defining **what good looks like**, and uses those definitions to guide the entire lifecycle model selection, design, deployment, and iteration.

## The Four Evaluation Pillars

Chip Huyen describes four critical dimensions to evaluate any AI system meaningfully. These form the skeleton of the EDD framework.

## Domain-Specific Capability

This refers to how well the AI handles tasks within the specific domain it’s built for. A chatbot for mental health support needs very different capabilities than a legal document summarizer. Domain-specific evaluation ensures your model isn’t just smart in general it’s smart where it matters.

Example:  
If you’re building an AI to review medical scans, you evaluate it on metrics like sensitivity, false negatives, or ability to detect rare pathologiesmetrics that wouldn’t matter for a product recommendation engine.

## Generation Quality

This is about how well the model generates content text, answers, decisions. It’s often measured in terms of:

- **Coherence**: Is the output logically consistent?
- **Relevance**: Does it stay on topic?
- **Factuality**: Are the statements true and verifiable?
- **Fluency**: Is the language natural?

Example:  
For a travel assistant that generates itineraries, poor generation quality might mean hallucinating places that don’t exist or suggesting unrealistic plans (like visiting 5 cities in one day).

## Instruction-Following Capability

This pillar measures how precisely a model follows user instructions or developer prompts. It’s not enough for a model to generate fluent text — it must stick to the task.

Example:  
If you ask your AI to summarize a contract in bullet points but it replies with a full paragraph or ignores a clause, the instruction-following quality is low. This often happens with generic LLMs when prompts aren’t carefully designed or tested.

## Latency and Cost Trade-Offs

Performance matters. A model might be accurate but too slow or expensive to run in production. This pillar ensures we weigh computational costs, response times, and hardware constraints.

Example:  
If you’re building a customer support bot that answers 1,000 queries a minute, using GPT-4 Turbo might give better answers but be too costly or slow. You might prefer a smaller distilled model that’s 90% as good but runs 10x faster.

## Model Selection Workflow: Making Informed Trade-Offs

Evaluation criteria don’t live in theory they guide action. Here’s how Chip Huyen suggests we use them in the model selection process.

## Step 1: Initial Filtering

Narrow down the list of potential models by eliminating obvious mismatches. This includes:

- Language support (e.g., does it handle Tamil?)
- Licensing (e.g., can you use it commercially?
- Hardware compatibility (e.g., does it run on your infrastructure?)

This saves time and cost upfront.

## Step 2: Benchmarking

Compare the remaining candidates using existing benchmarks (like MMLU, TruthfulQA, or domain-specific datasets). This gives you a birds-eye view of their strengths and weaknesses.

Example:  
For a finance summarizer, you might test models on a FinBERT benchmark or use financial documents annotated with key insights.

## Step 3: Hands-On Prototyping

Now that you’ve got a shortlist, test the models with your **actual use case data**. This step is non-negotiable because no benchmark can simulate the quirks of your users or data.

## Get Keerthanams’s stories in your inbox

Join Medium for free to get updates from this writer.

Example:  
You feed sample customer complaints into the model and check if it correctly identifies tone, urgency, or key issues. This often reveals subtle issues like hallucinations, over-summarization, or misunderstanding tone.

## Step 4: Continuous Monitoring

Models can degrade over time or behave differently in production than in test environments. You need systems to track:

- Drift in performance
- Failure patterns
- Emerging edge cases

Example:  
A product description generator may start inserting false claims after fine-tuning on new data. Monitoring pipelines will help catch these anomalies early.

## Building Evaluation Pipelines That Scale

Evaluation should not be a one-time event. You need robust pipelines that are automated, interpretable, and easy to maintain.

## System-Level vs Component-Level Evaluation

- **System-Level** looks at the end-to-end performance: does the chatbot resolve the query? Does the summarizer reduce time spent by users?
- **Component-Level** breaks it down: is the named entity recognizer tagging entities properly? Is the summarization module preserving intent?

Both levels matter. You can’t fix what you don’t measure.

## Creating Clear Evaluation Guidelines

Different annotators or reviewers may interpret model outputs differently. To ensure consistent judgment, you need **guidelines**:

- What does it mean to “follow instructions”?
- What’s considered a “correct” summary?

Example:  
For a hiring recommendation engine, define what an “appropriate” suggestion looks like: Is it based on skill match? Prior experience? Availability?

## Choosing the Right Sampling Strategy

You can’t test every output, so sampling is key. Choose smartly:

- **Random Sampling**: Gives an unbiased picture.
- **Stratified Sampling**: Ensures coverage of edge cases or priority segments.
- **Error focused Sampling**: Reviews the worst-performing examples in detail.

Example:  
In an email response generator, you might sample high-risk messages (angry customers) more frequently to ensure tone sensitivity.

## Meta-Evaluation: Evaluating the Evaluation

Even your evaluation processes need tuning. Ask:

- Are your metrics actually measuring what matters?
- Are humans consistent in their annotations?
- Are your tests covering real-world complexity?

Example:  
If your summarizer scores high on ROUGE but users still complain, then ROUGE isn’t capturing what matters. You need better metrics like helpfulness or information preservation.

## Real-World Applications

Here’s how companies are applying Evaluation-Driven Development today:

## Airbnb

They test how AI-generated descriptions affect user conversion rates. Evaluation isn’t just about linguistic quality, it’s about business outcomes.

## Notion AI

Evaluation of their summarization and ideation features goes beyond language quality to measure task completion, tone matching, and utility for productivity.

## Hugging Face

In their model cards and leaderboard evaluations, they provide detailed metrics across domains and use EDD principles to help users choose the right models.

## Healthcare AI

EDD is essential to ensure models don’t just perform statistically well, but are **clinically valid**, interpretable, and aligned with medical guidelines.

## From Metrics to Mindset

Evaluation-Driven Development isn’t just about numbers. It’s a mindset: that **“better” is not generic it’s contextual.** In every AI product, you must define what “better” means for your users, your domain, and your values.

EDD brings structure, accountability, and focus to what can otherwise become a trial-and-error process. It makes your AI system not just technically competent, but **fit for purpose**.

If you internalize this framework, every AI product you build will be more robust, more ethical, and more useful by design.

## Reference

This post was inspired by Chapter 4 of *AI Engineering* by Chip Huyen - a practical and insightful framework for anyone building scalable, evaluation-first AI systems that work in the real world.

Huyen, Chip. *AI Engineering*. [https://huyenchip.com/ai-eng](https://huyenchip.com/ai-eng).