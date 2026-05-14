---
name: agent-best-practices
description: Use when scoping, building, or reviewing an agent (Anthropic SDK agent, Claude Code subagent, or multi-agent system). Covers responsibility scoping, tool selection, prompt design, evals, guardrails, and cost management.
---

# Building Agents That Work

## Scoping

- **Single responsibility.** "Customer support agent" fails. "Refund-eligibility-classifier" succeeds. If you can't name the one decision the agent owns, the scope is too broad.
- **Boundary conditions in the spec.** "This agent does X. It does NOT do Y, Z, W. When asked about Y, hand off to <Y-agent>."
- **Failure modes upfront.** What does the agent do when (a) the user asks something out of scope, (b) it doesn't have enough data, (c) a downstream tool fails?

## Tool selection

- **Minimum sufficient toolset.** Every tool is a way to fail. Start with the fewest tools that complete the job.
- **Tool descriptions are prompts.** The model picks tools from descriptions. Write them like you'd write a function comment for a teammate.
- **Idempotent tools where possible.** Retries are part of agent life. A tool that double-charges on retry is a bug.
- **Structured outputs** — when you need a specific JSON shape back, use tool-use to force it, don't ask the model to "respond in JSON".

## Prompt design

- **System prompt = job description.** Role, scope, tone, output format.
- **Few-shot for shape, not for content.** Examples teach formatting. They don't teach reasoning.
- **Negative examples are powerful.** "DO NOT do X — here's an example of doing X wrong" calibrates faster than only positive examples.
- **Caching.** For long system prompts or tool catalogs, use prompt caching. Cuts cost and latency materially for repeat invocations.

## Evals

If you can't measure it, you can't ship it.

- **Golden set first.** 30–100 cases covering: happy paths, edge cases, refusal cases, out-of-scope cases, adversarial inputs. Ground truth labeled by a human.
- **Eval metrics that matter:**
  - **Task completion rate** — did the agent finish the user's actual goal?
  - **Accuracy** — was the answer/action correct?
  - **Hallucination rate** — did it invent facts/entities/numbers?
  - **Guardrail compliance** — refusals where required, no leaks of sensitive data?
- **Eval at every change.** Prompt change, model upgrade, tool addition — re-run the eval set.
- **Track regressions visibly.** Per-case results, not just aggregate scores.

## Guardrails

- **Refuse before reasoning.** If the input is out of scope, the cheapest answer is the right one.
- **Sanitize tool outputs.** A tool returning user-controlled text into the agent's context is a prompt injection vector. Quote it.
- **Never leak secrets.** Credentials, API keys, raw PII — never in agent context, memory, or logs.
- **Confirm before destructive actions.** Default to confirm. Promote to auto-execute only via graduated trust, not by default.

## Human-in-the-loop

- **Design for it, not around it.** The interrupt-resume pattern is core, not an exception.
- **Plan-then-execute.** Agent proposes a plan in plain language. User approves, edits, or aborts. Then execute.
- **Mid-execution control.** "Stop", "skip", "change parameter", "hand off" must all work without state corruption.

## Cost management

- **Bounded loops.** Every agent loop has a max-iteration cap. No "until done" without a circuit breaker.
- **Cheap before expensive.** Try a fast classifier before invoking the heavy agent.
- **Prompt caching.** For static long context (tool catalogs, system prompts), enable caching. Often 90%+ cost reduction on repeat calls.
- **Smaller model first.** Try Haiku before Sonnet, Sonnet before Opus. Promote only when evals require it.

## Multi-agent

- **Orchestrator owns coherence.** Sub-agents don't talk to each other; the orchestrator routes.
- **Sub-agents return structured results, not free text.** The orchestrator stitches.
- **Conflict surfacing > silent picks.** If two sub-agents disagree, the orchestrator shows the user, not the answer it preferred.
- **Audit per agent.** Every action logged with which agent, which sub-step, what affected.

## Anti-patterns

- "It works in the demo." Demo and prod are different distributions.
- "We'll add evals later." Evals after launch is debugging by user report.
- "Just give it all the tools." Tool sprawl is failure surface.
- "Agent A calls Agent B calls Agent C." Three-deep chains are debugging hell. Flatten.
