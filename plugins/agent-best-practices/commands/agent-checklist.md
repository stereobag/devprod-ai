---
description: Pre-build checklist for a new agent. Walks through scoping, tools, prompt, evals, guardrails, and cost. Use before writing the first line of code.
argument-hint: <agent-name-or-purpose>
allowed-tools: [Read]
---

# Agent Pre-Build Checklist

Proposed agent: $ARGUMENTS

Apply the `agent-best-practices` skill. Walk the user through the checklist below by asking targeted questions one section at a time. Don't accept vague answers — push back until each item is concrete.

## 1. Scope
- [ ] What is the one decision or output this agent owns?
- [ ] What is explicitly out of scope?
- [ ] Where does it hand off (other agents, humans, fallback)?

## 2. Failure modes
- [ ] What does it do on out-of-scope input?
- [ ] What does it do on insufficient data?
- [ ] What does it do on downstream tool failure?

## 3. Tools
- [ ] Minimum sufficient toolset listed?
- [ ] Each tool's description is precise enough that the model can pick correctly?
- [ ] Idempotent where retry matters?
- [ ] Structured outputs via tool use, not "respond in JSON"?

## 4. Prompt
- [ ] System prompt = role + scope + tone + output format?
- [ ] Few-shot examples for shape?
- [ ] Negative examples for known failure modes?
- [ ] Prompt caching planned for repeated invocations?

## 5. Evals
- [ ] Golden set drafted (30–100 cases)?
- [ ] Coverage: happy / edge / refusal / out-of-scope / adversarial?
- [ ] Metrics: task completion, accuracy, hallucination, guardrail compliance?
- [ ] Run plan: eval on every prompt change / model upgrade / tool addition?

## 6. Guardrails
- [ ] Out-of-scope refusal logic?
- [ ] Tool output sanitization?
- [ ] No secrets in agent context / memory / logs?
- [ ] Destructive actions gated by confirmation?

## 7. Human-in-the-loop
- [ ] Plan-then-execute pattern designed?
- [ ] Mid-execution control (stop/skip/handoff) supported?
- [ ] Recovery from user interrupt?

## 8. Cost
- [ ] Loop iteration cap set?
- [ ] Cheap classifier before expensive agent considered?
- [ ] Smallest model that passes evals chosen?

## 9. Multi-agent (if applicable)
- [ ] Orchestrator owns coherence?
- [ ] Sub-agents return structured results?
- [ ] Conflict surfacing rather than silent picks?

After the user has answered, summarize the spec back in one paragraph and call out any item that's still vague.
