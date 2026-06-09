---
title: "Skills (Anthropic)"
aliases:
  - anthropic-skills
  - skill-design
tags:
  - wiki
  - agentic-architecture
domain: certification
sources:
  - "anthropic-agents-to-skills.md"
status: stable
confidence: medium
---
Created: Friday, 16 April 2026, 17:12
Last Modified: `=dateformat(this.file.mtime, "DDDD, HH:mm")`

---
# Skills (Anthropic)

**Summary**: Skills are organized collections of files that package composable procedural knowledge for agents, bridging the gap between agent intelligence and domain expertise.

**Sources**: [[raw/anthropic-agents-to-skills.md|anthropic agents to skills]]

---

## Overview

Anthropic has shifted focus from building agents to building skills. After launching Claude Code and observing how customers use agents, they identified a critical gap: **agents have intelligence and capabilities but lack the domain expertise needed for real work**. As Barry Zhang put it: "Who do you want doing your taxes? Is it going to be Mahesh, the 300 IQ mathematical genius, or is it Barry, an experienced tax professional?" The answer is always the expert — agents today are brilliant but miss important context upfront and don't learn over time.

**Key realization**: Code is not just one use case — it is the *universal interface to the digital world*. An agent with file system and bash access can generate financial reports, run Python analysis, and produce formatted output without specialized scaffolding. Claude Code, originally conceived as a coding agent, turned out to be a general-purpose agent. The gap was never capability — it was expertise.

See [[agentic-architecture]] for foundational concepts and [[tool-design-mcp]] for the MCP protocol that skills build upon.

## What Skills Are

Skills are organized collections of files that package composable procedural knowledge for agents. Key characteristics:

- **Deliberate simplicity** — "Something that anyone, human or agent, can create and use as long as they have a computer"
- **Folder-based** — Skills live in directories with a core `skill.md` file
- **Versionable** — Can be versioned in Git, shared via Google Drive, or zipped for team distribution
- **Include tools** — Can include scripts as reusable tools, solving the limitation of traditional tools that are poorly documented and stuck in the context window

**Example**: When Claude repeatedly wrote the same Python script to style slides, they saved it inside the skill as a reusable tool for future sessions.

## Progressive Disclosure Design

The design philosophy centers on **progressive disclosure**:

- At **runtime**, only metadata is shown to indicate a skill exists
- This keeps the **context window protected** so hundreds or thousands of skills can fit
- When an agent needs a skill, it reads the full `skill.md` containing core instructions and directory structure

This architecture has already scaled to **thousands of skills within five weeks of launch**, spanning three categories:

| Category | Examples |
|----------|---------|
| **Foundational** | Anthropic document skills (Office file creation/editing), Cadence scientific research skills (EHR analysis, bioinformatics) |
| **Third-party / product** | Browserbase (Stagehand browser automation), Notion (deep research across a full workspace) |
| **Enterprise / team-specific** | Fortune 100 internal best practices; developer teams serving tens of thousands of engineers deploying code style and workflow conventions |

Notably, **non-technical workers** in finance, recruiting, accounting, and legal are building skills — early validation that the format is accessible beyond software engineers.

## Architecture: Skills + MCP

The emerging agent architecture layers:

| Layer | Role | Example |
|-------|------|---------|
| **MCP servers** | External connectivity | Connecting to outside world (APIs, databases, tools) |
| **Skills** | Domain expertise | Procedural knowledge, best practices, reusable scripts |

As Barry noted: "MCP is providing the connection to the outside world while skills are providing the expertise."

This enabled rapid vertical launches in **financial services** and **life sciences**, each equipped with relevant MCP servers and skill libraries.

## Future Directions

Anthropic plans to treat skills like software:
- **Testing** — Validate skill behavior
- **Evaluation** — Measure skill effectiveness
- **Versioning** — Track changes and updates
- **Dependency tracking** — Make composable skills work together predictably across different runtime environments

## Computing Stack Analogy

Anthropic draws an analogy to the computing stack:

| Layer | Analogy | Reality |
|-------|---------|---------|
| **Processors** | CPU | Models (massive investment, limited alone) |
| **Operating system** | OS | Agent runtime (orchestrates resources) |
| **Applications** | Apps | Skills (millions of developers encode domain expertise) |

"We hope that skills can help us open up this layer for everyone," Mahesh said. "This is where we get creative and solve concrete problems for ourselves, for each other, and for the world just by putting stuff in the folder."

## Skills as Transferable Memory

Skills move continuous learning from an aspiration to a concrete mechanism. Because Claude can write skills in a standardized format, anything it records can be **efficiently read by a future version of itself** — knowledge is transferable rather than locked in a session.

This makes skills a more narrowly reliable form of memory than raw retrieval: they capture *procedural knowledge for specific tasks* rather than trying to retain everything. Compare to [[agent-memory]] where episodic/semantic memory is broader but harder to guarantee.

## Organizational Knowledge Compounding

As skills accumulate organizational knowledge, a new employee on day 30 finds Claude already knows the team's priorities, workflows, and effective practices — creating **compounding value** that extends beyond individual organizations into the broader community. Skills built by anyone in the external community can also raise the ceiling for your own agents, just as MCP servers built by strangers expand what your agent can connect to.

## Exam Relevance

Understanding skills is relevant to:
- Agentic architecture questions about knowledge management
- Tool design patterns (skills as organized tool collections)
- Context management (progressive disclosure protecting context window)

## Related Pages

- [[agentic-architecture]] — Foundational agentic loop and handoff patterns
- [[tool-design-mcp]] — MCP protocol that skills build upon
- [[claude-code]] — Where skills are used in practice
- [[agent-orchestration-patterns]] — How skills integrate with orchestration