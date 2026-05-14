---
description: Start a structured article draft from a topic. Use the 300-word pitch format by default; specify "long" or "longform" to switch to long-form.
argument-hint: <topic> [length: pitch|long]
allowed-tools: [Read, Write, Edit, WebFetch, WebSearch]
---

# Write Article

Topic: $ARGUMENTS

Apply the `article-writing` skill voice and structure rules.

**Default behavior (pitch format):** Produce a 250–300 word pitch with:
- Title (provocative but accurate)
- 1–2 sentence hook
- 3 topic bullets
- 1 "why now" line

**If user passed "long" or "longform":** Produce a structured outline first (title, hook, 3–5 sections with one-line summaries, conclusion direction), then ask before drafting full sections.

**Always:**
- Surface 2–3 alternative title options at the end.
- Cite any external claims with URLs.
- Don't start drafting until you've named the specific reader you're writing for (one sentence).
