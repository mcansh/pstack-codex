---
name: poteto-help
description: Explain pstack for Codex setup, skill selection, playbooks, and runtime limits. Use when asked how to use this plugin.
disable-model-invocation: true
---

# Poteto help for Codex

Read [Codex runtime contract](../codex-runtime.md) first.

For a help request, read [README](../../README.md) and answer without starting the task. For a work request, read [poteto-mode](../poteto-mode/SKILL.md) and do the authorized work.

- Setup and role models: [setup-pstack](../setup-pstack/SKILL.md).
- Understand code or rationale: [how](../how/SKILL.md), [why](../why/SKILL.md).
- Design alternatives: [architect](../architect/SKILL.md), [arena](../arena/SKILL.md).
- Review and impact: [interrogate](../interrogate/SKILL.md), [blast-radius](../blast-radius/SKILL.md).
- Parallel work: [swarm](../swarm/SKILL.md). Requires available agent tools and respects their capacity.
- App proof: [create-verification-skill](../create-verification-skill/SKILL.md), [maintain-verification-skill](../maintain-verification-skill/SKILL.md).
- Formal proof: [create-formal-verification-skill](../create-formal-verification-skill/SKILL.md), [maintain-formal-verification-skill](../maintain-formal-verification-skill/SKILL.md). Use for races or invariants tests rarely reach; maintain checks when covered code changes.
- Chat updates and decisions: [ketchup](../ketchup/SKILL.md). Lists every pending user decision with evidence and risk.
- Prior work: [recall](../recall/SKILL.md). Uses only exposed in-scope history.
- Personal style and lessons: [automate-me](../automate-me/SKILL.md), [reflect](../reflect/SKILL.md).

Playbooks belong to poteto-mode, not separate slash commands. Read its index to select bug fix, feature, refactoring, performance, shipping, babysit, or orchestration. Use `$poteto-mode` plus a concrete goal and a pass/fail check. Use the exact namespaced name shown by Codex if another plugin supplies the same skill name.

Defaults inherit the current Codex model. Different-model panels require actual supported models. Cloud agents, persistent loops, Cursor Custom Modes, Grok Bot routines, and Benny automations are not supplied by this port. A session without delegates can work sequentially, but cannot claim independent verification. See [compatibility](../../docs/COMPATIBILITY.md).

Keep the answer short. Give one concrete prompt when helpful and link the installed file or its actual public copy in mcansh/pstack-codex.
