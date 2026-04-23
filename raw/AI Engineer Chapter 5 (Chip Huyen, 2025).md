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
## Chapter 5. Prompt Engineering

[![](https://github.com/chiphuyen/aie-book/raw/main/assets/prompt-anatomy.png)](https://github.com/chiphuyen/aie-book/blob/main/assets/prompt-anatomy.png)

  
*Figure 5-1. A simple example to show to anatomy of a prompt.*  

Foundation models can do many things, but you must tell them exactly what you want. The process of crafting an instruction to get a model to do what you want is called prompt engineering. How much crafting is needed depends on how sensitive the model is to prompts. If a small change can cause a big change in the model's response, more crafting will be necessary.

You can think of prompt engineering as human–AI communication. Anyone can communicate, but not everyone can communicate well. Prompt engineering is easy to get started, which misleads many into thinking that it's easy to do it well.

The first part of this chapter discusses the anatomy of a prompt, why in-context learning works, and best prompt engineering practices. Whether you're communicating with AI or other humans, clear instructions with examples and relevant information are essential. Simple tricks like asking the model to slow down and think step by step can yield surprising improvements. Just like humans, AI models have their quirks and biases, which need to be considered for a productive relationship with them.

Foundation models are useful because they can follow instructions. However, this ability also opens them up to prompt attacks in which bad actors get models to follow malicious instructions. This chapter discusses different attack approaches and potential defenses against them. As security is an ever-evolving cat-and-mouse game, no security measurements will be foolproof. Security risks will remain a significant roadblock for AI adoption in high-stakes environments.

This chapter also discusses techniques to write better instructions to get models to do what you want. However, to accomplish a task, a model needs not just instructions but also relevant context. How to provide a model with relevant information will be discussed in the next chapter.