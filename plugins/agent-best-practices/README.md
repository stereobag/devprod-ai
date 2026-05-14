# agent-best-practices

Encodes patterns for building agents that actually work in production — Anthropic SDK agents, Claude Code subagents, multi-agent systems.

## What you get

- **Skill: `agent-best-practices`** — auto-activates when you're scoping, building, or reviewing an agent. Covers scoping, tool selection, prompt design, evals, guardrails, and cost.
- **Command: `/agent-checklist`** — pre-build checklist for a new agent.
- **Subagent: `agent-reviewer`** — review an existing agent definition / prompt / eval setup against best practices.

## Opinions, not platitudes

- Single-responsibility agents beat omnibus agents.
- Evals are non-negotiable. If you don't have a golden set, you don't have an agent — you have a vibe.
- Tool minimalism: every tool an agent has access to is a way it can fail.
- Human-in-the-loop is a feature, not a fallback. Design for it.
