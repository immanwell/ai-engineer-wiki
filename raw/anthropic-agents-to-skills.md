---
source: https://youtu.be/CEvIs9y1uog?si=PlhS6D_fy_QUtxKA
title: "From Agents to Skills: Anthropic's New Paradigm"
author: dotta
date: 2026-04-16
tool: summarize
---

### From Agents to Skills: Anthropic's New Paradigm

At Anthropic, Barry Zhang and Mahesh Murag have shifted their focus from building agents to building skills. After launching Claude Code and observing how customers use agents, they identified a critical gap: agents have intelligence and capabilities but lack the domain expertise needed for real work. "Who do you want doing your taxes? Is it going to be Mahesh, the 300 IQ mathematical genius, or is it Barry, an experienced tax professional?" Barry asked. The answer is always the expert—agents today are brilliant but miss important context upfront and don't learn over time.

Skills are organized collections of files that package composable procedural knowledge for agents. "This simplicity is deliberate," Mahesh explained. "We want something that anyone human or agent can create and use as long as they have a computer." Skills live in folders, can be versioned in Git, shared via Google Drive, or zipped for team distribution. They can include scripts as tools—solving a key limitation of traditional tools that are poorly documented and stuck in the context window. When Claude repeatedly wrote the same Python script to style slides, they simply saved it inside the skill as a reusable tool for future sessions.

The design philosophy centers on progressive disclosure: at runtime only metadata is shown to indicate a skill exists, keeping the context window protected so hundreds or thousands of skills can fit. When an agent needs a skill, it reads the full skill.md containing core instructions and the directory structure. This architecture has already scaled to thousands of skills within five weeks of launch, spanning foundational skills, partner-built skills (Notion, Browserbase, Cadence), and enterprise skills for Fortune 100 companies teaching agents about organizational best practices and internal software.

The emerging agent architecture layers MCP servers for external connectivity with skills for domain expertise. "MCP is providing the connection to the outside world while skills are providing the expertise," Barry noted. This enabled rapid vertical launches in financial services and life sciences, each equipped with relevant MCP servers and skill libraries. Future directions include treating skills like software with testing, evaluation, versioning, and dependency tracking—making composable skills work together predictably across different runtime environments.

Anthropic draws an analogy to the computing stack: models are like processors requiring massive investment but limited alone; agent runtime acts as the operating system orchestrating resources; and skills represent the application layer where millions of developers encode domain expertise. "We hope that skills can help us open up this layer for everyone," Mahesh said. "This is where we get creative and solve concrete problems for ourselves, for each other, and for the world just by putting stuff in the folder." As skills accumulate organizational knowledge, a new employee on day 30 finds Claude already knows the team's priorities, workflows, and effective practices—creating compounding value that extends beyond individual organizations into the broader community.