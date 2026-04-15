---
title: "Claude Code"
aliases:
  - claude-code
  - claude-code-configuration
  - claude-code-hooks
  - claude-code-multi-agent
tags:
  - wiki
  - claude-code
domain: certification
sources:
  - "instructor-8lsy243ftffjjy1cx9lm3o2bw-public-1773274827-Claude+Certified+Architect+–+Foundations+Certification+Exam+Guide.pdf"
status: stable
confidence: high
date_created: 2026-04-15
date_modified: 2026-04-15
---

# Claude Code

**Summary**: Anthropic's CLI tool for AI-assisted software development. Covers configuration, git workflows, hooks, debugging, multi-agent patterns, and tool integration via MCP.

**Sources**: (source: instructor-8lsy243ftffjjy1cx9lm3o2bw-public-1773274827-Claude+Certified+Architect+–+Foundations+Certification+Exam+Guide.pdf)

---

## Overview

Claude Code is a command-line interface that brings Claude into your terminal. It handles:

- Code editing, refactoring, and creation
- Git operations (commit, push, PR creation)
- Multi-file project tasks
- Tool use and MCP server integration
- Hooks for automation and validation

**20% of the exam** covers Claude Code specifically — the largest domain after agentic architecture and tool design.

## Core commands

### Project initialization

- `claude-code --init` — start a new project
- `claude-code` — resume an existing project
- `.claude/` — project-level directory for settings, hooks, and context

### Interactive vs. non-interactive

- **Interactive mode**: Claude Code prompts you in the terminal, confirms actions
- **Non-interactive mode**: Pass `--dangerously-skip-permissions` to run autonomously (use carefully)

## Configuration

### settings.json

Project-level settings in `.claude/settings.json`:

```json
{
  "permissions": {
    "allow": ["Read", "Write", "Bash"],
    "deny": ["Network"]
  },
  "maxTokens": 4000,
  "model": "claude-opus-4-6"
}
```

### Environment variables

- `CLAUDE_API_KEY` — API key for authentication
- `CLAUDE_API_KEY_FILE` — path to a file containing the key

## Git workflow

Claude Code integrates with git:

1. **Stage changes**: `claude-code --add` or interactive selection
2. **Review diffs**: Claude reads staged/unstaged changes
3. **Commit**: `claude-code --commit "message"` or interactive
4. **Push**: `claude-code --push` after commit
5. **Create PR**: `claude-code --pr` — creates a PR with description

### Commit hooks

Pre-commit hooks can validate, lint, or test before each commit.

## Hooks system

Hooks allow automation at key points in Claude Code's execution.

### Hook file locations

- `.claude/hooks/` — directory for hook scripts
- Hooks are triggered by lifecycle events

### Hook types

- **Pre-execution hooks** — run before Claude acts (e.g., validate code style)
- **Post-execution hooks** — run after Claude completes an action
- **Pre-tool hooks** — run before specific tools are called

### Hook configuration

In `settings.json`:

```json
{
  "hooks": {
    "pre-commit": [".claude/hooks/pre-commit-lint.sh"],
    "pre-tool-use": {
      "Bash": [".claude/hooks/pre-bash-verify.sh"]
    }
  }
}
```

### Hook use cases

- Enforcing code quality standards
- Running tests before or after edits
- Validating git commit messages
- Blocking destructive operations
- Generating changelogs or documentation

## Multi-agent

Claude Code supports multi-agent patterns:

### Session coordination

- Multiple Claude Code sessions can run in parallel
- Share context through shared files or a git worktree
- Each session is independent but can coordinate via files

### Worktrees

- `git worktree add` creates isolated branches for parallel work
- Useful when multiple agents need to work on different features simultaneously
- Each worktree has its own working directory and git state

### Supervisor pattern

One Claude Code session acts as the supervisor, delegating sub-tasks to other sessions (potentially running in background terminals or worktrees).

## MCP integration

Claude Code works with MCP servers to extend its tool capabilities. MCP servers are configured via:

- `settings.json` under `"mcpServers"`
- The `mcp` CLI command for quick server management

Example MCP server configuration in `settings.json`:

```json
{
  "mcpServers": {
    "my-tool-server": {
      "command": "node",
      "args": ["./mcp-server/dist/index.js"],
      "env": {}
    }
  }
}
```

## Debugging with Claude Code

### Error handling

- Claude Code shows tool error output directly
- Can iterate and retry failed operations
- Use `Continue` to retry with the same context

### Session logs

- `.claude/logs/` contains session history
- Useful for reviewing what happened in a session

### Permissions model

Claude Code has a granular permissions system:
- `Read` — read files and directories
- `Write` — create and modify files
- `Bash` — execute shell commands
- `Network` — make network requests
- `Edit` — modify existing files (vs. Write for new files)

## Exam relevance

Expected to understand:
- Settings.json structure and permission configuration
- Hooks lifecycle and use cases
- Git workflow (commit, push, PR creation)
- Worktree-based multi-agent patterns
- MCP server configuration
- Debugging and error recovery

## Related pages

- [[agentic-architecture]] — underlying agentic principles
- [[tool-design-mcp]] — MCP server development
- [[claude-certified-architect-foundations-exam-guide]] — exam overview