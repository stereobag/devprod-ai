---
description: Run a health check on the current Claude Code project setup — CLAUDE.md, settings.json, skills, commands, agents, hooks — flagging gaps and anti-patterns.
allowed-tools: [Read, Bash, Grep]
---

# Claude Code Setup Health Check

Apply the `claude-best-practices` skill and audit the current workspace. Report findings under these headings:

## CLAUDE.md
- Does it exist?
- Does it cover: project purpose, tech stack, conventions, what to avoid?
- Anti-patterns: vague instructions, instructions duplicated in settings.json, instructions that are obvious from the code.

## settings.json
- Permissions: tight or wildcard-heavy?
- Hooks: any present? Do they look correct?
- Env vars: anything that looks like a secret leaked into settings.json?

## Skills (.claude/skills/ if present)
- Each skill has a frontmatter `description` that says *when to use* it?
- Any skill that does more than one thing (candidate for splitting)?
- Any skill over 400 lines that doesn't earn it?

## Commands (.claude/commands/ if present)
- Each command has `argument-hint` if it takes input?
- Each command has `allowed-tools` if it can write or push?
- Naming: verb-object?

## Agents (.claude/agents/ if present)
- Each agent has a tight `description` (when to invoke)?
- Each agent's system prompt is self-contained (doesn't assume conversation context)?
- Each agent specifies output format / length?

## Hooks
- PreToolUse hooks: do any block too aggressively?
- Any hook that could fail silently?

## Top 3 fixes
Prioritized list — the changes that would most improve this setup.

Be concrete. Cite file paths and line numbers.
