---
name: devprod-research
description: Use when researching AI-augmented developer productivity — new tools, vendor moves, IDE integrations, agent platforms, devprod metrics, or incidents. Provides a structured research playbook to keep findings sourced, recent, and signal-dense rather than vendor-marketing-flavored.
---

# Researching AI-Augmented Developer Productivity

When the conversation is about developer productivity tools (Cursor, Copilot, Cline, Claude Code, Cody, Continue, Aider, etc.), AI coding assistant behavior, IDE integrations, agent frameworks for software engineering, or productivity metrics for AI-augmented dev work — follow this playbook.

## Sources, ranked

1. **Primary** — official changelogs, release notes, engineering blog posts, GitHub repos, vendor docs. Always preferred for "what is X capable of."
2. **Practitioner reports** — Hacker News threads, /r/cursor /r/ClaudeAI subreddits, Twitter/X engineering accounts (with caveats — opinions, not specs).
3. **Industry analysis** — Stack Overflow Developer Survey, GitHub Octoverse, Anthropic Economic Index, Latent Space, every-third newsletter writeups.
4. **Avoid** — vendor-funded "studies" without methodology, AI-generated SEO listicles, Medium thinkpieces with no shipped artifacts.

## Research signal rules

- **Show your work.** Cite specific URLs, dates, and version numbers. "Cursor 0.50 added X on 2026-04-12" beats "Cursor recently added X."
- **Distinguish announced vs. shipped vs. measured.** A blog post claiming a feature is not the same as users reporting it works.
- **Prefer measured productivity claims.** Treat "10x productivity" claims as marketing until you see a methodology.
- **Flag controversies, not just wins.** Devprod-AI's most interesting content is friction: layoff anxieties, fake-PR scandals, hallucinated code in production, copyright suits, model regressions.
- **Date everything.** "Recent" is not a date. Cite the actual release / publication date.

## Output structure

When asked to summarize findings, default to this shape:

```
Topic: <one-line>
Date: <YYYY-MM-DD>

What shipped     — bullet of confirmed releases
What was claimed — bullet of announcements without ship dates
What broke       — bullet of incidents, regressions, controversies
What to watch    — one item with a date or trigger
Sources          — list of cited URLs
```

## When to use a subagent

If the research will take more than 3 web fetches or you need an isolated read of a long doc, dispatch the `devprod-researcher` subagent instead of doing it inline. Keep the user's main context clean.
