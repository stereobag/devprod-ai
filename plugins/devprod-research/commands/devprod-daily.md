---
description: Run a structured daily research pass on AI-augmented developer productivity and output a digest. Optional argument scopes the digest (e.g., "agents", "coding assistants", "metrics").
argument-hint: [scope]
allowed-tools: [WebFetch, WebSearch, Read, Bash]
---

# Daily DevProd Digest

Today's research scope: $ARGUMENTS (default: full landscape)

Run the research playbook defined in the `devprod-research` skill. Produce a digest with these sections, ordered by signal density:

## 🚀 What shipped (top 3)
Specific releases, features, or product launches in the last 24–48 hours. Cite version + date + URL.

## ⚠️ What broke (top 3)
Incidents, regressions, controversies, outages, security findings. Cite source + date.

## 📢 What was announced (top 3)
Roadmap, beta access, partnerships, vendor moves with no ship date yet.

## 🔭 What to watch
One item with a specific date or trigger to revisit. Why it matters.

## 📚 Sources
Bulleted URLs of everything cited above.

---

**Rules of engagement:**
- Don't editorialize. Report; don't predict.
- If a source is a vendor blog, flag it.
- If you can't find 3 items in a category, say "nothing notable" instead of padding.
- Date format: YYYY-MM-DD.
- Default to the last 48 hours unless the user specifies otherwise.
