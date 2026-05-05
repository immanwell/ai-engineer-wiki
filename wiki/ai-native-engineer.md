---
title: "AI-Native Engineer"
aliases:
  - "AI-native development"
tags:
  - wiki
  - "agentic-architecture"
domain: "agentic-architecture"
sources:
  - "mihail-eric-junior-engineers-crisis.md"
status: stub
confidence: medium
---

Created: Friday, 17 April 2026, 02:51
Modified: `=dateformat(this.file.mtime, "DDDD, HH:mm")`

---

# AI-Native Engineer

**Summary**: An AI-native engineer combines traditional programming fundamentals with strong competency in agentic workflows, centering on the ability to manage multiple AI agents simultaneously through effective context switching.

**Sources**: [[raw/mihail-eric-junior-engineers-crisis.md|Mihail Eric Stanford talk]]

---

## Definition

Mihail Eric defines an AI-native engineer as someone who combines traditional programming foundations with strong competency in agentic workflows. The core skill is **context switching** — watching multiple "eager, savvy intern" agents work simultaneously, remembering where each left off, and meaningfully pushing each task forward.

## Key Principles

### Start Simple
Eric cautions against mimicking the "Boris from Claude" pattern of running 10 agents simultaneously — starting that way is the wrong approach entirely.

Instead:
1. Build one agent workflow reliably first
2. Add a second agent only when the first is well-understood
3. Add a third only when the first two work together smoothly

### The Context Switching Skill
Managing multiple agents requires:
- Tracking where each agent left off
- Understanding what each agent is working on
- Meaningfully pushing each task forward
- Knowing when to intervene vs. let agents run

Eric notes this mirrors what makes a good human manager — and the best multi-agent practitioners often have prior experience managing human developers.

## Practical Implementation: Claude Code Workflow Example

Using the same 3-step principle for building software with Claude Code:

### Step 1: Build one workflow reliably

**Example: URL shortener in Node.js/Express**

Start a fresh Claude Code session. Build one task at a time:

```bash
/plan build a URL shortener in Node.js with Express
→ review plan → approve → it creates files

Add POST /shorten endpoint
Add GET /:shortcode endpoint
Add GET /health endpoint
```

After each task, you run and check the output. Note what Claude gets wrong (hallucinates require statements, misses edge cases).

**By end of this stage:** You can predict what Claude will do before it does it. You know its failure modes.

### Step 2: Second workflow — parallel worktrees

Now add two features simultaneously using two Claude Code sessions:

**Terminal 1** (`feature/analytics`):
```bash
cd ~/url-shortener
claude-code --worktree feature/analytics
→ "Add click tracking — increment counter in SQLite on each visit"
```

**Terminal 2** (`feature/custom-slugs`):
```bash
cd ~/url-shortener
claude-code --worktree feature/custom-slugs
→ "Add custom slugs — let users choose their own short code"
```

Both run in parallel. You review both, then merge sequentially.

**By end of this stage:** You can track two Claude Code sessions without forgetting what either is doing.

### Step 3: Full pipeline — plan mode + worktree + merge

New issue: "Add rate limiting — 100 req/min per IP"

```bash
Trigger → Plan → Code → Review → Merge

/plan add rate limiting with sliding window algorithm, 100 req/min per IP
→ review plan, suggest adding burst traffic tests → approve

Claude Code writes rate limiting middleware + unit tests
You review: does it actually block at 100? Do tests pass?

git checkout -b feature/rate-limiting
git add . && git commit && git push
gh pr create && gh pr merge
```

### The Signal Before Moving to Next Step

| Transition | Signal |
|-------------|--------|
| Step 1 → 2 | You can explain what Claude will do before it does it |
| Step 2 → 3 | You can track two worktrees without forgetting what either is doing |

If you're still surprised by Claude's output in step 1, you're not ready for step 2. If you can't track two worktrees in step 2, you're not ready for step 3.

## Exam Relevance

- [[agentic-architecture]] — multi-agent orchestration, when to add agents
- [[context-reliability]] — managing agent state across context switches

## Related Pages

- [[mihail-eric-junior-engineers-crisis]]
- [[agent-friendly-codebase]]
- [[junior-engineer-advantage]]
