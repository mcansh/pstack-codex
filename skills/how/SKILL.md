---
name: how
description: "Use for \"how does X work\", code walkthroughs before changing something, and placement / ownership / layering questions (\"where should this live\", \"which package owns this\", \"is this the right layer\"). Explains subsystem architecture, runtime flow, onboarding mental models. Use why for motivation."
disable-model-invocation: true
---
Read [Codex runtime contract](../codex-runtime.md) before executing this skill. It governs tools, models, settings, history, delegation, and authorization in all referenced files.

# How

Explore the codebase to answer "how does X work?" questions.

If the scope is ambiguous, state your interpretation and explore. The user can redirect.

## 1. Explain

Spawn one general-purpose delegate through the available agent tool with read-only scope in its prompt. Select `how explainer` from `~/.config/pstack/codex-models.md` if present, defaulting to `inherit-parent`. Use only supported spawn arguments. If delegation is unavailable or prohibited, explain directly and disclose the lack of an independent pass. Give the delegate the user's question and this brief:

> You are writing an architectural explanation for a senior engineer. Explore the codebase and write an explanation that a senior engineer unfamiliar with this area could read and walk away with a solid mental model. They should understand the architecture well enough to start working in it confidently. Do not edit files or perform external writes.

## 2. Present

Present the delegate's output. Light edits for clarity or context from the conversation are fine. Do not substantially rewrite it.
