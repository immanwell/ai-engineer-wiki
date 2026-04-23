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
## Chapter 4. Evaluate AI Systems

[![](https://github.com/chiphuyen/aie-book/raw/main/assets/evaluation-process.png)](https://github.com/chiphuyen/aie-book/blob/main/assets/evaluation-process.png)

  
*Figure 4-5. An overview of the evaluation workflow to evaluate models for your application.*  

This is one of the hardest, but I believe one of the most important, topics that I've written about with regard to AI. Not having a reliable evaluation pipeline is one of the biggest blockers to AI adoption. While evaluation takes time, a reliable evaluation pipeline will enable you to reduce risks, discover opportunities to improve performance, and benchmark progresses, which will all save you time and headaches down the line.

Given an increasing number of readily available foundation models, for most application developers, the challenge is no longer in developing models but in selecting the right models for your application. This chapter discussed a list of criteria that are often used to evaluate models for applications, and how they are evaluated. It discussed how to evaluate both domain-specific capabilities and generation capabilities, including factual consistency and safety. Many criteria to evaluate foundation models evolved from traditional NLP, including fluency, coherence, and faithfulness.

To help answer the question of whether to host a model or to use a model API, this chapter outlined the pros and cons of each approach along seven axes, including data privacy, data lineage, performance, functionality, control, and cost. This decision, like all the build versus buy decisions, is unique to every team, depending on not only what the team needs but also what the team wants.

This chapter also explored the thousands of available public benchmarks. Public benchmarks can help you weed out bad models, but won't help you find the best models for your applications. Public benchmarks are also likely contaminated, as their data is included in the training data of many models. There are public leaderboards that aggregate multiple benchmarks to rank models, but how benchmarks are selected and aggregated is not a clear process. The lessons learned from public leaderboards are helpful for model selection, as model selection is akin to creating a private leaderboard to rank models based on your needs.

This chapter ends with how to use all the evaluation techniques and criteria discussed in the last chapter and how to create an evaluation pipeline for your application. No perfect evaluation method exists. It's impossible to capture the ability of a high-dimensional system using one- or few-dimensional scores. There are many limitations and biases associated with evaluating modern AI systems. However, this doesn't mean we shouldn't do it. Combining different methods and approaches can help mitigate many of these challenges.

Even though dedicated discussions on evaluation end here, evaluation will come up again and again, not just throughout the book but also throughout your application development process. Chapter 6 explores on evaluating retrieval and agentic systems, while Chapters 7 and 9 focus on calculating a model's memory usage, latency, and costs. Data quality verification is addressed in Chapter 8, and using user feedback to evaluate production applications in Chapter 10.

With that, let's move onto the actual model adaptation process, starting with a topic that many people associate with AI engineering: prompt engineering.