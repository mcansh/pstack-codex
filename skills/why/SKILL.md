---
name: why
description: "Use for 'why does X work this way', 'why we picked Y', design rationale, regressions, postmortems, or data-backed thresholds. Returns a cited read on decisions and tradeoffs. Use how for runtime behavior."
disable-model-invocation: true
---
Read [Codex runtime contract](../codex-runtime.md) before executing this skill. It governs tools, models, settings, history, delegation, and authorization in all referenced files.

# Why

Answer from the record, not the code: read the commits and PR discussions that introduced the target and each later change, and other available, in-scope sources if the trail is thin. Cite what the authors wrote, mark your own inferences as inferences, and say what the record does not answer. Report unavailable history or connectors as gaps. This is a read-only investigation, not authorization for external writes.
