---
title: "chiphuyen/aie-book: [WIP] Resources for AI engineers. Also contains supporting materials for the book AI Engineering (Chip Huyen, 2025)"
source: "https://github.com/chiphuyen/aie-book/blob/main/chapter-summaries.md#chapter-1-introduction-to-building-ai-applications-with-foundation-models"
author:
published:
created: 2026-04-23
description: "[WIP] Resources for AI engineers. Also contains supporting materials for the book AI Engineering (Chip Huyen, 2025) - chiphuyen/aie-book"
tags:
  - "clippings"
---

## Chapter 1. Introduction to Building AI Applications with Foundation Models

Table 1-3. Common generative AI use cases across consumer and enterprise applications.

| Category | Examples of Consumer Use Cases | Examples of Enterprise Use Cases |
| --- | --- | --- |
| Coding | Coding | Coding |
| Image and Video Production | Photo and video editing   Design | Presentation   Ad generation |
| Writing | Email   Social media and blog posts | Copywriting   SEO   Reports, memos, design docs |
| Education | Tutoring   Essay grading | Employee onboarding   Employee upskill training |
| Conversational Bots | General chatbot   AI companion | Customer support   Product copilots |
| Information Aggregation | Summarization   Talk-to-your-docs | Summarization   Market research |
| Data Organization | Image search   Memex | Knowledge management   Document processing |
| Workflow Automation | Travel planning   Event planning | Data extraction, entry, and annotation   Lead generation |

I meant this chapter to serve two purposes. One is to explain the emergence of AI engineering as a discipline, thanks to the availability of foundation models. Two is to give an overview of the process needed to build applications on top of these models. I hope that this chapter achieved this goal. As an overview chapter, it only lightly touched on many concepts. These concepts will be explored further in the rest of the book.

The chapter discussed the rapid evolution of AI in recent years. It walked through some of the most notable transformations, starting with the transition from language models to large language models, thanks to a training approach called self-supervision. It then traced how language models incorporated other data modalities to become foundation models, and how foundation models gave rise to AI engineering.

The rapid growth of AI engineering is motivated by the many applications that the emerging capabilities of foundation models enable. This chapter discussed some of the most successful application patterns, both for consumers and enterprises. Despite the incredible number of AI applications already in production, we're still in the early stages of AI engineering, with countless more innovations yet to be built.

Before building an application, an important yet often overlooked question is whether you should build it. This chapter discussed this question together with major considerations for building AI applications.

While AI engineering is a new term, it evolved out of ML engineering, which is the overarching discipline involved with building applications with all ML models. Many principles from ML engineering are still applicable to AI engineering. However, AI engineering also brings with it new challenges and solutions. The last section of the chapter discusses the AI engineering stack, including how it has changed from ML engineering.

One aspect of AI engineering that is especially challenging to capture in writing is the incredible amount of collective energy, creativity, and engineering talent that the community brings. This collective enthusiasm can often be overwhelming, as it's impossible to keep up-to-date with new techniques, discoveries, and engineering feats that seem to happen constantly.

One consolidation is that since AI is great at information aggregation, it can help us aggregate and summarize all these new updates. But tools can only help to a certain extent. The more overwhelming a space is, the more important it is to have a framework to help us navigate it. This book aims to provide such a framework.

The rest of the book will explore this framework step-by-step, starting with the fundamental building block of AI engineering: the foundation models that make so many amazing applications possible.