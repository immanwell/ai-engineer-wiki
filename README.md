# AI Engineer Wiki

A personal knowledge base for building foundational AI engineering knowledge, maintained by Claude Code.

## Purpose

This wiki follows the [LLM Wiki](https://karpathy.github.io/2019/04/19/llm_wiki/) pattern pioneered by Andrej Karpathy. It serves as both:

- A structured study companion for the **Claude Certified Architect – Foundations** exam
- A growing reference for AI engineering best practices

The exam covers five domains: `agentic-architecture`, `tool-design-mcp`, `claude-code`, `prompt-engineering`, and `context-reliability`.

## Folder Structure

```
raw/          -- immutable source documents (PDFs, papers)
wiki/         -- markdown pages maintained by Claude
  index.md    -- table of contents for the entire wiki
  log.md      -- append-only record of all wiki operations
templates/    -- page templates
CLAUDE.md     -- instructions for Claude
```

## Build Process

This wiki is maintained through a structured workflow:

1. **Ingest** — Source documents go in `raw/`, then Claude extracts and synthesizes key ideas
2. **Connect** — New pages are cross-linked via `[[wiki-links]]` to build a web of knowledge
3. **Maintain** — `wiki/log.md` tracks every addition and change with timestamps

## Wiki Pages

| Page | Description |
|------|-------------|
| `agentic-architecture` | Designing autonomous AI systems that plan, use tools, and adapt |
| `tool-design-mcp` | Building reliable tools and MCP servers for AI agents |
| `claude-code` | Using Claude Code CLI effectively |
| `prompt-engineering` | Crafting prompts that get reliable, high-quality outputs |
| `context-reliability` | Managing context window, retrieval, and long-horizon coherence |
| `context-reliability` | Exam study guide with domain breakdown |

## License

MIT — See [LICENSE](LICENSE) for details.
