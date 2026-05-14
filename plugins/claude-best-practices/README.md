# claude-best-practices

Encodes best practices for working effectively inside Claude Code — tool selection, skill design, command patterns, settings, hooks, and parallelism.

## What you get

- **Skill: `claude-best-practices`** — auto-activates when you're working with Claude Code itself (editing settings, designing skills/commands, debugging hook behavior, evaluating your setup).
- **Command: `/claude-checklist`** — run a setup health check on the current project / CLAUDE.md / settings.
- **Subagent: `claude-reviewer`** — review a specific Claude Code artifact (skill, command, agent, hook) for adherence to best practices.

## Inspired by

- The system prompts and skill definitions Anthropic ships with Claude Code.
- Patterns that consistently work in real production usage (parallel tool calls, skill triggers, hook-based automation, subagent isolation).
- Anti-patterns we've burned hours on (vague skill descriptions, over-eager auto-commit, monolithic agents).
