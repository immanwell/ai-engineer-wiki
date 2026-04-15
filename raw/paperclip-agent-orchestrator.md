---
source: https://youtu.be/h403btjldDQ
title: "What is Paperclip?"
author: @steipete
date: 2026-04-16
tool: summarize
---

### What is Paperclip?

Paperclip is an open-source agent orchestrator designed as a "human control plane for AI labor." It allows users to set up an org chart of AI agents, manage them, invoke their own preferences into how agents work, and have them complete real business tasks. The core philosophy is that you remain involved from higher-level design all the way through execution, ensuring your taste and accountability are built into every workflow. To get started, users run `npx paperclip AI onboard` in their terminal, optionally passing `-SCS` for default options.

### Core Architecture: Agents, Org Charts, and Skills

Paperclip organizes work around companies containing agents structured like a corporate hierarchy — a CEO at the top who delegates to executives (CTO, CMO, etc.), who in turn manage individual contributor agents like coders, content strategists, and video writers. A key differentiator is that users bring their own agents — Gemini, OpenClaw, Claude, Hermes, Pi, and others can all be hired as employees within the system. Each agent has an "agentic surface" meaning the CEO knows how to hire new agents and install new skills. Paperclip integrates with skills.sh, and the skills manager can automatically locate and install capabilities like Remotion best practices for video creation. The system also tracks monthly spend budgets per agent and per project, supporting both subscription-based usage and pay-per-inference models.

### How Work Gets Done: Projects, QA, and Routines

Work in Paperclip flows through projects (familiar task-management interfaces) where agents are assigned specific tasks and work through them. To ensure quality and reliability, Paperclip provides built-in workflows including QA review and approval gates — for example, a QA agent with the agent browser skill can open websites, fill forms, and click buttons to verify work before it returns to the human manager. Unlike brittle hooks that work differently across Claude Code, Cursor, or other IDEs, these workflows are vendor-neutral. Routines enable reusable task templates — users can set up scheduled or manual workflows like "create a Discord message for all merges to master" or "run a Gretile code review on submitted PRs." These routines support template variables, allowing things like branch names to be passed in at execution time.

### The 40,000 Stars Demo: Speed and Context in Action

The creator demonstrates Paperclip's power by showing how he created a Remotion video celebrating 40,000 GitHub stars in roughly five minutes. He created an issue, assigned it to the CEO agent, and instructed the CEO to hire a video writer and install the Remotion best practices skill. The video writer then looked at the existing dashboard, branding guide, and stats — context that was already stored in Paperclip — and produced an on-brand animation with real charts. The creator notes this task would normally take a week, but with Paperclip it became an afterthought because the agents already had access to brand identity, existing projects, and institutional memory. Over time, feedback given to agents is collected and used to create organization-specific skills — for instance, a Paperclip-specific Remotion skill that encodes preferences like "cuts should be two seconds, not six."

### Creating Your Own Company and Scaling Wisely

During the demo, the creator shows how to bootstrap a new company called "Agent Tools Directory" — a hypothetical MCP directory proxy service. The CEO agent was hired first, then asked permission to hire a CTO, which the user approved. The CEO then built a hiring plan covering phases for core engineering and go-to-market. The creator advises starting small — just the agents you need — rather than importing huge templates with 130 pre-configured agents, because if you don't take time to craft how you expect agents to behave, you won't get good results. He also notes that not every agent needs frontier model pricing; Open Router support means agents can use cheaper models like Qwen 3.6 Plus for tasks that don't require peak intelligence, reserving Claude or GPT for higher-stakes work.

### Roadmap and Current Limitations

Paperclip launched March 4th and crossed 40,000 GitHub stars within about 34 days (likely 50,000 by video release). The creator acknowledges significant gaps in the current version: multi-user support is missing (a priority this week for cloud deployment), workspaces for isolated environments are experimental, and features like CEO chat, "maximizer mode" for token-burned sprint work, E2B/dev.exe/cloud sandboxing integration, and a free open-source desktop app are all on the roadmap. Memory, knowledge base improvements, and general stability work are also planned over the next 30 days. The creator emphasizes that Paperclip is not a coding tool or code review tool — it's a tool for creating and running businesses, usable by non-technical people for marketing, sales, finance operations, and beyond. *"You do not have to be a coder to use Paperclip."*
