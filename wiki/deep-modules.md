---
title: "Deep Modules"
aliases:
  - "deep module"
  - "deep module architecture"
tags:
  - wiki
  - "agentic-architecture"
domain: "agentic-architecture"
sources:
  - "Matt Pocock Software Fundamentals AI Age (2025).md"
status: stub
confidence: high
---

Created: Thursday, 23 April 2026, 19:08
Modified: `=dateformat(this.file.mtime, "DDDD, HH:mm")`

---

# Deep Modules

**Summary**: From John Ousterhout's Philosophy of Software Design — deep modules hide significant functionality behind simple interfaces. This architecture is ideal for AI-assisted development because AI can work within tested constraints while humans own the interface design.

**Sources**: [[raw/Matt Pocock Software Fundamentals AI Age (2025).md|Matt Pocock Software Fundamentals]]

---

## Definition

**Deep module**: Hides significant functionality behind a simple interface. You don't need to understand internals to use it.

**Shallow module**: Doesn't hide much functionality, but forces you to navigate complex interfaces — many tiny blobs with shallow connections.

## Why Deep Modules Work for AI

Shallow module codebases are devastating for AI because:
- The model can't efficiently explore dependencies
- It often misses the right module entirely
- Cognitive load is high for both human and AI

Deep module codebases let you:
- Treat implementation as a gray box
- Design the interface carefully
- Test at the boundary
- Let AI handle internals within tested constraints

## The Design Pattern

1. Design the interface from the outside — you own this
2. Test at the boundary
3. Delegate interior implementation to AI
4. AI works within tested constraints

## Contrast with "Specs to Code"

"Specs to code" divests from design entirely. Deep modules make design a first-class concern — invest in the design of the system every day (Kent Beck's principle).

## Related Pages

- [[pocock-software-fundamentals]]
- [[agent-friendly-codebase]]
