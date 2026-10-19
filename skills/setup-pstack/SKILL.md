---
name: setup-pstack
description: Configure pstack role models using only model and reasoning choices exposed by this Codex session. Use when asked to set up pstack, change its model choices, or reduce its reasoning budget.
---

# Setup pstack for Codex

Read [Codex runtime contract](../codex-runtime.md) first.

1. Inspect the available agent tool schema. Record its supported models and efforts and any restrictions on overriding them. If the tool exposes no choices, use `inherit-parent`; do not guess model IDs or ask the user for IDs the tool cannot accept.
2. Read `~/.config/pstack/codex-models.md` if it exists. Preserve supported user choices. Report unavailable choices and propose `inherit-parent` for them.
3. Ask which roles, if any, should override the parent. Offer only supported choices. A reasoning budget is a separate supported effort, never part of a generated model ID. For panels, a comma-separated list sets the number of seats. Default panels have two `inherit-parent` seats. Explain that same-model panels give independent attempts, not model diversity.
4. Show the concrete configuration. Write it once the user's requested choices are clear. Create the directory if needed and preserve unrelated settings. `auto` means `inherit-parent`. Omit unsupported effort fields. Example defaults:

```markdown
# pstack Codex models
# Read on demand by pstack; this is not an automatically loaded Codex rule.
feature, refactoring: inherit-parent
bug-fix: inherit-parent
perf-issue: inherit-parent
hillclimb: inherit-parent
judgment and prose: inherit-parent
hardest tasks: inherit-parent
how explorer: inherit-parent
how explainer: inherit-parent
why investigators: inherit-parent
why synthesizer: inherit-parent
reflect tooling: inherit-parent
reflect judgment, divergent, synthesizer: inherit-parent
arena runners: inherit-parent, inherit-parent
arena cross-judge pool: inherit-parent, inherit-parent
swarm workers: inherit-parent
architect runners: inherit-parent, inherit-parent
interrogate reviewers: inherit-parent, inherit-parent
```

For an explicit override, use `model=<supported-id>; reasoning_effort=<supported-effort>` as one role value (or one comma-separated panel seat). Read these as separate fields when spawning; omit unsupported fields. An unqualified value `inherit-parent` omits both fields.

5. Report the path written. Every pstack invocation reads it afresh. If the session cannot spawn agents, explain that role settings cannot enable delegation.
6. Check for a runtime verification skill or existing app harness and a formal verification skill. For each missing kind, offer once to generate it with [$create-verification-skill](../create-verification-skill/SKILL.md) or [$create-formal-verification-skill](../create-formal-verification-skill/SKILL.md). Explain that the first drives app behavior and the second checks a code property within stated bounds and assumptions. Generate only the kind the user accepts; otherwise continue without pushing.
