---
title: "Code with Claude 2026 Opening Keynote"
source: "https://www.youtube.com/live/GMIWm5y90xA"
author:
  - "Anthropic"
published: 2026-05-06
created: 2026-05-06
description: "Code with Claude 2026 Opening Keynote Summary & Narrative Transcript — Anthropic"
tags:
  - "clippings"
  - "anthropic-event"
---

Code with Claude 2026: Opening Keynote Summary & Narrative Transcript

Event Date: May 6, 2026
Host: Anthropic

1. Introduction: The Exponential Curve of AI (Ami Vora)

Speaker: Ami Vora (Chief Product Officer, Anthropic)

Ami Vora opens the keynote by reflecting on her early days in computer science—waiting in long lines to log into basement servers to compile code. She contrasts that slow, manual era with the current state of software development powered by Claude.

She notes that while the "ground is shifting" and models are improving on an exponential curve—from Opus 4.1, 4.5, 4.6, to the brand new Opus 4.7 and the highly anticipated Mythos Preview—most engineering organizations are still adopting AI on a linear path. To close this gap, Anthropic is launching massive updates across the Claude Platform and Claude Code, including a 17X increase in API volume and doubling rate limits for developers.

2. Advancements at the Model Layer (Dianne Penn)

Speaker: Dianne Penn (Head of Product, Research)

Dianne recaps the rapid release cycle of the Claude model family. She highlights that the jump from the 3-series to the new 4-series (specifically Opus 4.7 and Sonnet 4.6) is designed to give developers the raw intelligence needed for long-context, agentic loops, adaptive thinking, and visual design.

3. The Claude Platform: Speed, Scale, and the "Advisory Strategy" (Angela Jiang & Katelyn Lesse)

Speakers: Angela Jiang (Head of Product, Claude Program) & Katelyn Lesse (Head of Engineering, Claude Platform)

Angela and Katelyn introduce the new capabilities of Claude Managed Agents, which abstract away the complex infrastructure required to run multi-agent systems at scale. They introduce a concept called "Dreaming," where agents can asynchronously review their past sessions, surface patterns, and automatically update their memories to improve future performance.

EMPHASIS: The Advisory Strategy

One of the most critical breakthroughs discussed by Angela and Katelyn is the "Advisor Strategy." Historically, developers face a dilemma: routing all tasks through a massive, highly intelligent model (like Opus) is too slow and expensive, but using a smaller, faster model (like Sonnet) can lead to edge-case failures on complex tasks.

How the Advisory Strategy works:

The Executor (Claude Sonnet): A smaller, faster model acts as the "Executor." It handles the main loop, running every single turn rapidly and reading/writing to the shared context.

The Advisor (Claude Opus): A larger, highly capable model sits in the background as the "Advisor."

The Loop: When the Executor gets stuck, encounters an ambiguous instruction, or needs higher-level reasoning, it makes an on-demand Tool Call to the Advisor. The Advisor reviews the shared context (conversation, tools, history) and sends strategic advice back down to the Executor to proceed.

The Results: This strategy is a game-changer. They shared internal performance metrics showing that pairing Sonnet 4.6 (Executor) with an Opus 4.7 (Advisor) actually increased agentic terminal coding accuracy from 59.6% to 63.4%, while simultaneously dropping the cost from $0.94 to $0.88 per run compared to using a massive model alone. It gives developers "Frontier model quality at 5X lower cost."

4. Redefining Engineering with Claude Code (Cat Wu)

Speaker: Cat Wu (Head of Product, Claude Code)

Cat Wu details how Claude Code is evolving from an individual developer tool into a system for entire engineering organizations. She highlights new features like:

Claude Code Desktop App: A visual, desktop-native interface to watch agents work.

Remote Agents: The ability to execute Claude Code entirely in the cloud or via mobile devices.

CI Auto-fix: Claude now monitors Continuous Integration pipelines and automatically generates PRs to fix broken builds.

Claude Security: Automated, overnight scanning of codebases for vulnerabilities.

5. EMPHASIS: The "Boris Part" - Live Autonomous Demo (Boris Cherny)

Speaker: Boris Cherny (Head of Claude Code)

Boris Cherny takes the stage (pausing to take a quick selfie with the crowd) and delivers the emotional core of the keynote. He admits that even working at Anthropic, the capabilities they are shipping still feel "magical." He notes that asynchronous, autonomous coding is no longer a future concept—it is here.

The Live "Acme Pay" Demo:
Boris runs a live demonstration playing the role of an engineer at a fictional payments company called Acme Pay.

The Task: He gives Claude Code a high-level task: "Add a refund flow to the merchant dashboard."

The Execution: Claude Code opens up the terminal and begins coding the entire frontend and backend implementation.

The Edge Case (The Magic Moment): Claude attempts to test the UI. It clicks the "Refund" button in the simulated browser, but realizes something is wrong: "There is no success toast [notification]." 4.  Autonomous Debugging: Without any human intervention, Claude Code digs into the React tree, discovers a race condition where an AnimatePresence component is unmounting the toast before it can render, rewrites the code to fix the bug, and successfully verifies the fix.

Routines & CI Auto-fix: Claude then automatically opens a Pull Request on GitHub. But wait—the GitHub CI pipeline fails due to a flaky network timeout on a staging API gateway! A background "Routine" agent immediately notices the failure, diagnoses it as a known infrastructure flake, retries the job, and gets a green build.

The Conclusion: Boris shows that all he has to do as a human developer is wake up, review the cleanly formatted PR, see that all CI checks are green, and hit "Merge."

Boris concludes the keynote by stating that the default is no longer humans prompting AI—it is AI running continuous routines, and humans stepping in only for higher-order review and creative direction.