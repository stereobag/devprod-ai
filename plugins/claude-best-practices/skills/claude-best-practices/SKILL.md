---
name: claude-best-practices
description: Use when working with Claude Code itself — designing skills/commands/subagents, editing settings.json, configuring hooks, debugging tool behavior, or evaluating an existing setup. Encodes patterns that consistently work and anti-patterns to avoid.
---

# Claude Code Best Practices

## Tool selection

- **Read** for known paths. Don't `cat`.
- **Edit** for modifying existing files. Don't `sed`. Don't `Write` unless creating new or fully rewriting.
- **Grep / Bash grep** for symbol search and codebase exploration.
- **Agent (subagent)** for parallel research, long-running searches, or anything that would pollute the main context. Not for tasks the parent could do faster inline.
- **WebFetch / WebSearch** for current info beyond training cutoff. Always cite.
- **TaskCreate** for multi-step work. Mark each task complete the moment it's done, not at the end.

## Parallel tool calls

If you have N independent tool calls (no data dependency between them), batch them in one message. Sequential calls only when later calls depend on earlier results.

Common parallelizable batches:
- `git status` + `git diff` + `git log`
- Reading multiple unrelated files
- Running unrelated bash queries

## Skill design

- **Description first.** The description field is the trigger. Be specific. "Use when X" beats "Useful for various X-related tasks."
- **One job per skill.** If a skill has three jobs, split it.
- **Show your reasoning model.** Skills are for *how* to do something, not just *what*. Include the rule and the *why* so the model can judge edge cases.
- **Length matters.** Skills are loaded into context every time they trigger. Keep them under ~400 lines unless the content genuinely earns it.

## Command design

- **Verb-object naming.** `/write-article`, `/critique-article`, `/devprod-daily` — not `/article-helper`.
- **Argument-hint frontmatter** for any command that takes input.
- **`allowed-tools`** restricts the blast radius. Always specify for actions that could write or push.
- Commands shell out the slash-command syntax; they're not skills. Don't duplicate.

## Subagent design

- **Single responsibility.** Subagents that "do everything" produce thin work.
- **Pass full context in the prompt.** Subagents don't see your conversation; brief them like they walked in cold.
- **Specify output format.** "Report in under 400 words" beats "Tell me what you find."
- **Use `model: sonnet`** unless you specifically need opus depth or haiku speed.

## Settings.json

- Permissions: scope as tightly as workflow allows. `Bash(npm:*)` beats `Bash(*)`.
- Hooks: SessionStart for context injection, PreToolUse for guardrails, PostToolUse for cleanup.
- Env vars: anything secret goes in a `.env`, never in settings.json.

## Hooks

- **PreToolUse hooks can block** by exiting non-zero with a message. Use sparingly — false positives kill flow.
- **PostToolUse hooks observe** without blocking. Logging, telemetry, auto-format.
- **SessionStart hooks** inject project context. Keep them under a few hundred lines.
- Hooks run in the user shell; treat them as code that can have bugs.

## Anti-patterns

- **Auto-committing without asking.** Always confirm "should I create a commit?" unless the user has durably authorized it.
- **Long preambles.** "I'm going to read the file then…" — just read the file.
- **Verifying success without evidence.** Run the command, read the output, then claim success.
- **Reading freshly-edited files.** Edit already told you it worked. Trust it.
- **Sequential when parallel works.** See "Parallel tool calls" above.

## When responding to the user

- One sentence of intent before the first tool call ("Reading the config now.").
- Short updates at key moments. Silent ≠ good.
- End-of-turn summary: 1–2 sentences. What changed, what's next.
- Default to no comments in code. Default to no documentation files unless asked.
