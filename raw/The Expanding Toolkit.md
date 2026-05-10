---
title: "The Expanding Toolkit"
source: "https://www.youtube.com/live/GMIWm5y90xA"
author:
  - "Lucas (Research PM, Anthropic)"
published: 2026-05-06
created: 2026-05-10
description: "Code with Claude 2026 — Session 4: How scaffolding that used to be built manually now ships with the model. Covers tool use, context management, code execution, and computer use. Key theme: compensating for model unreliability has a half-life of months — leave that to Anthropic."
tags:
  - "clippings"
  - "anthropic-event"
---

# The Expanding Toolkit

**Speaker**: Lucas (Research PM, Anthropic)
**Event**: Code with Claude 2026
**Date**: May 6, 2026
**Watch**: https://www.youtube.com/live/GMIWm5y90xA

---

## Core Theme

> "Think of the model no longer as just an input-output LLM box, but as a series of tools around that model that expands its capabilities and leads to better performance."

**The key rule**:
- **Compensating for model unreliability** (retry logic, routers, planners, verification loops) → will have a half-life of months. Leave that work to Anthropic — it gets absorbed into the model.
- **Connecting your model to your world** (custom tools, your data, your specific context) → code that compounds. The model can't absorb what it can't see.

---

## 1. Tool Use: Routers Are Dead

### Before (Brittle)
- Build routers via string matching and heuristics ("if model mentions SQL → give database tool")
- Retry decorators on top because tools failed often
- Routers = "guesses about user intent in conditional if statements" — brittle, first thing to break when adding new tools

### After (Built-in)
- Model can **search through tools and pick the right one** itself
- Tool selection accuracy is now high enough that pre-filtering **makes things worse**, not better
- When a tool errors, Claude **sees the error, recovers on its own, and calls the tool again** — no more retry routers

### Quick Tip: Output Schema in Tool Description

When giving a tool to Claude, describe the **output schema** as well — not just the input parameters.

```txt
Tool: search_docs
Input: query string
Output schema: {id, title, snippet, score}
```

By describing the output, Claude knows what to expect — e.g., it knows a `score` will be returned, so it can rank outputs without an extra round trip.

### Claude Code Quick Tip: Pre/Post Tool Hooks

In Claude settings, define hooks that trigger **before** or **after** a specific tool is called:
- Block certain tool calls in specific situations
- Analyze and log outputs programmatically after tool calls

---

## 2. Context Management: Near-Infinite Context

### Before (Scaffolding Overload)
- Build your own memory system, chunking, RAG
- Call another model to summarize after every N turns
- Cash breakpoints to move by hand to save cost
- Manual context compaction to extend the window

### After (Built-in)
- **1 million context length at flat pricing** — reduces most window pressure
- **Server-side compaction** — automatic context compression
- **Context editing** — few lines of config
- Result: "much closer to the feeling of an infinite context window"

### Quick Tip: Clear Stale Tool Results Every Turn

> "By pruning stale tool outputs — screenshots, search results, file reads — you can save tremendously on context while keeping the decisions they informed."

The pattern:
1. Model reads a huge file → gets screenshot → makes a decision
2. Model runs a search that dumps a ton of text
3. **Clear those results** — keep only: the core task, the decision made, the results the agent analyzed itself
4. Tokens saved in real time

### Claude Code Quick Tip: `{slash} context`

Type `{slash} context` to get a **live colored grid breakdown** of what's filling your context window — viscerally see how much space messages, tool results, systems, and MCP definitions take. Also shows optimization suggestions.

---

## 3. Code Execution: Built-In Sandbox

### Before (Write-Run-Fix Loop)
1. Find a VM provider
2. Spin up sandbox on their VM
3. Model outputs code → put code on VM → run it
4. Parse traceback → feed back into model → repeat

Every round trip was a manual harness responsibility.

### After (Single API Turn)
Claude gets a **hosted sandbox on the server side**:
- That entire loop happens inside a single API turn
- No more harness round trips between Claude and a VM
- Claude has its own computer for stateless compute, data analysis, custom library installation
- All without disrupting or cluttering your local file system

### Mental Model: Two Computers

| Computer | Use For |
|----------|---------|
| **Claude's sandbox** | Stateless compute, data analysis, installing libraries |
| **Your local bash** | Access to your repo, local Python env, local context |

Claude intelligently knows which to use. It uses the sandbox for scratch pad work; it uses local bash when it needs repo access.

### Claude Code Quick Tip: `/schedule`

Use `/schedule` to set **cron-triggered autonomous runs** — the self-iteration loop on a timer, happening when you need it, completely autonomously.

---

## 4. Computer Use: No More Scaling Math

### Before (Image Glue)
For reliable clicks on a 1080p screen:
1. Take 1080p screenshot → downscale to Claude's pixel limits
2. Track the scaling factor
3. When Claude samples a click → scale coordinates back up to original resolution
4. Wrap in retries and verify statements

This was a **big pain point**.

### After (Native Resolution)
Opus 4.7 can take **native resolution screenshots and return 1:1 pixel coordinates up to 1440p** — covers the vast majority of display resolutions.

- The scaling math is completely gone
- Send the image → trust Claude will click exactly where it needs to

### OS World Eval (Computer Use Progress)

| Timeline | Score | What It Means |
|----------|-------|--------------|
| <12 months ago | <50% | Couldn't complete half the tasks |
| Now (Opus 4.7) | **78%** | Near the cusp of broad usability |

### Recommendations for Computer Use

- **Up to 1440p**: Try Claude native resolution
- **4K and above**: Downscale on your side still recommended
- **Format comparison**: JPEG, PNG, WebP compress differently — test what works best for your UI

### Claude Code Quick Tip: Claude in Chrome

Claude Code can leverage your **Chrome browser session** via the Claude in Chrome extension (`claude.ai/chrome`):
- Claude code session can start navigating the web
- Works for local development too

### Demo Highlight: Agentic Coding Loop with Chrome

In the demo, Claude Code:
1. Opens the dashboard in Chrome
2. **Reproduces the bug** — types in the live board, sees it fail
3. **Debugs in real time** — diagnoses the issue while testing
4. **Fixes the code** — wires up card creation correctly
5. **Retests the full flow** — creates item → verifies → tests drag-and-drop
6. **Recaps all changes** automatically

> "Giving Claude the capability to do browser use allows it to close the loop where it can create human-focused software and actually solve bugs itself directly without the developer needing to come in and handhold Claude to the bug and the solution."

---

## Key Takeaways

1. **Tool use**: Don't build routers — model picks tools intelligently now. Describe output schema in tool definitions.
2. **Context**: Prune stale tool results every turn. Use 1M context + server-side compaction.
3. **Code execution**: Use Claude's hosted sandbox for stateless compute — keeps local dev clean.
4. **Computer use**: Opus 4.7 handles up to 1440p native — no more scaling math. 78% on OS World eval.
5. **The rule**: Leave compensating code (retries, routers, verification loops) to Anthropic. Invest in connecting code (custom tools, your data, your context).
6. **The ecosystem is moving**: Every agent will get a front door for agents. The interesting work is what's on the other side of that door.

---

## Existing Wiki Connections

- [[context-reliability.md]] — context window, compaction strategies
- [[tool-design-mcp.md]] — tool design principles
- [[agentic-architecture.md]] — agentic loops, tool use
- [[claude-code.md]] — Claude Code features (hooks, /schedule, slash context)