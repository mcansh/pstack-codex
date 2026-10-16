# Codex compatibility

| Upstream behavior | Codex port |
| --- | --- |
| `.cursor-plugin/plugin.json` | `.codex-plugin/plugin.json` with skills and interface metadata |
| Cursor marketplace | `.agents/plugins/marketplace.json` for the Codex marketplace CLI |
| `/skill` notation | `$skill` or the installed namespaced skill name; internal routing reads the bundled file |
| Cursor model defaults and suffixes | Parent-model inheritance; supported explicit model and effort fields only |
| Always-applied `.mdc` model rule | `~/.config/pstack/codex-models.md`, read on each invocation |
| Registered custom subagent types | Plain delegate prompt files, explicitly included by the parent |
| Task arguments | Actual host spawn schema, bounded by its agent and nesting limits |
| Automatically isolated cloud workers | Explicit isolated worktrees or supported remote environments; never assumed |
| Cursor transcript discovery | Exposed current conversation or explicitly supplied in-scope history |
| Worktree last-chat inference | `unknown` liveness and `verify-liveness` bucket; deletion requires a separate usage check |
| cursor-team-kit helpers | Available skill authoring, diff review, and runtime drivers; missing proof is reported |
| `/loop`, cloud owners, overnight runs | Capability-gated; no bundled scheduler or remote agent service |
| Grok Bot webhook UI | Existing documented webhook only; no Cursor routine creation or secret cards |
| Benny automation templates | Not included; they depend on Cursor's automation service |

Every skill reads `skills/codex-runtime.md`. Its mappings apply to referenced playbooks and templates too. Read-only scope is prompt-level unless the host supplies enforced permissions. The port does not grant permission to publish, merge, delete, message others, or change settings.

Packaging follows [OpenAI's plugin packaging guide](https://developers.openai.com/plugins/build/plugins), with a portable root manifest and a Codex compatibility overlay.

The original Cursor tutorial is preserved under `docs/upstream/` for provenance, not as a Codex runbook. The runtime contract and active skill files govern this port. The bundled Bun tools retain upstream dependency versions and behavioral tests; the worktree audit alone changes runtime behavior to avoid relying on private Cursor history.

Validation checks package structure and local tools. An installed-session smoke test is still needed to assess routing and agent behavior in a particular Codex host. Remote PR operations, cloud execution, and long-running scheduling require separate end-to-end validation against actual host capabilities.
