# devprod-ai

The home of devprod.ai — research, evals, and tooling for AI-augmented developer productivity.

## Contents

- **DevProd AI knowledge base** — research notes, eval logs, daily reports, and the dashboard:
  - `index.html` — dashboard
  - `agent_types_and_architectures.md`, `ai_tool_analysis.md`, `company_case_studies.md`, `developer_type_best_practices.md`, `measuring_developer_productivity.md`, `research_sources.md`
  - `daily_update_log.md`, `eval_log.md`
  - `reports/` — daily report archive
- **Claude Code plugin marketplace** — a small marketplace of Claude Code plugins:
  - `.claude-plugin/marketplace.json` — marketplace manifest
  - `plugins/devprod-research` — daily research playbook + `/devprod-daily` + `devprod-researcher` subagent
  - `plugins/article-writing` — voice and structure guardrails + `/write-article` + `/critique-article` + `article-critique` subagent
  - `plugins/claude-best-practices` — Claude Code workflow guidance + `/claude-checklist` + `claude-reviewer` subagent
  - `plugins/agent-best-practices` — agent design / eval / guardrail guidance + `/agent-checklist` + `agent-reviewer` subagent

## Install the marketplace

```bash
/plugin marketplace add stereobag/devprod-ai
/plugin install devprod-research@devprod-ai
/plugin install article-writing@devprod-ai
/plugin install claude-best-practices@devprod-ai
/plugin install agent-best-practices@devprod-ai
```

Each plugin has its own README under `plugins/<name>/README.md`.

## License

MIT (see `LICENSE`).
