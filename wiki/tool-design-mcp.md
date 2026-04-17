---
title: "Tool Design & MCP"
aliases:
  - mcp
  - model-context-protocol
  - tool-design
  - mcp-server
  - mcp-client
tags:
  - wiki
  - tool-design-mcp
domain: certification
sources:
  - "instructor-8lsy243ftffjjy1cx9lm3o2bw-public-1773274827-Claude+Certified+Architect+–+Foundations+Certification+Exam+Guide.pdf"
status: stable
confidence: high
---
Created: Friday, 15 April 2026, 10:24
Modified: `=dateformat(this.file.mtime, "DDDD, HH:mm")`

---
# Tool Design & MCP

**Summary**: The Model Context Protocol (MCP) is Anthropic's standard for connecting AI models to external tools, data sources, and services. Tool design covers how to build effective tools that agents can invoke reliably.

**Sources**: [[raw/instructor-8lsy243ftffjjy1cx9lm3o2bw-public-1773274827-Claude+Certified+Architect+–+Foundations+Certification+Exam+Guide.pdf|architect exam guide]]

---

## What is MCP?

The **Model Context Protocol** is a standardized way to connect AI models to external resources — tools, data stores, APIs, and services. Rather than hardcoding integrations, MCP provides a consistent interface both for:

- **MCP Servers**: External services that expose tools via MCP
- **MCP Clients**: Applications (like Claude Code) that consume those tools

MCP servers and clients communicate over JSON-RPC 2.0, typically via stdio or HTTP/SSE.

## MCP Architecture

```
┌─────────────┐     MCP Protocol      ┌──────────────┐
│   MCP Host  │◄─────────────────────►│  MCP Server  │
│ (Claude     │                       │ (your tool   │
│  Code, API) │                       │  server)     │
└─────────────┘                       └──────────────┘
```

- **MCP Host**: The application using Claude (Claude Code, API client, etc.)
- **MCP Server**: The service exposing tools — can be local (stdio) or remote (HTTP/SSE)
- **MCP Client**: The client-side component within the host that manages the session

## Tool design principles

### Input schema design

Tools receive structured JSON input. Design principles:

- **Flat parameters** preferred over deeply nested objects
- **Sensible defaults** for optional fields
- **Clear type annotations** — string, number, boolean, array, object
- **Avoid excessive optional fields** — makes tool harder to use correctly

### Tool naming

- Use `snake_case` for tool names (e.g., `read_file`, not `readFile`)
- Be explicit: `database_query` not `query`
- One verb per tool: each tool should do one thing well

### Response design

Tools return structured JSON. The `content` array typically contains:
- `type: "text"` for text results
- `type: "image"` for image data
- Error messages as text with clear descriptions

### Idempotency

Design tools to be safely retried. If a tool call fails mid-operation, a retry should not cause duplicate side effects.

## MCP Server patterns

### Transport types

- **stdio**: Local communication, JSON-RPC over stdin/stdout — common for local tool servers
- **HTTP + SSE**: Remote servers, using Server-Sent Events for responses
- **WebSocket**: Bidirectional streaming (less common)

### Server implementation

A minimal MCP server exposes:
1. **Server info** — name, version, capabilities
2. **Tool definitions** — name, description, input schema
3. **Tool handlers** — the actual logic when a tool is called
4. **Resource definitions** (optional) — static data the server can provide

### Handlers and responses

When a tool is called via MCP:
1. Parse the JSON-RPC request
2. Execute the tool logic
3. Return a JSON-RPC response with the result

Errors should follow JSON-RPC error codes and include a message.

## MCP in Claude Code

Claude Code ships with built-in MCP support:
- Configure MCP servers in `settings.json` or via CLI
- Tools from MCP servers appear alongside built-in tools
- Can combine MCP tools with custom scripts and user-defined tools

## Security considerations

- Tools have access to everything the host process has
- MCP servers run with the permissions of the calling process
- Validate and sanitize all tool inputs
- Use minimal permissions principle — servers should only expose what's needed

## Exam relevance

Expected to understand:
- MCP protocol basics and JSON-RPC communication
- Tool input/output schema design
- Server vs. client roles in MCP
- How tools integrate into the agentic loop
- Transport mechanisms (stdio vs. HTTP)

## Related pages

- [[agentic-architecture]] — how agents use tools
- [[claude-code]] — MCP configuration in Claude Code
- [[agent-orchestration-patterns]] — how orchestration uses tools in multi-agent workflows