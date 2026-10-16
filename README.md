# pstack for Codex

[Lauren Tan's pstack](https://github.com/cursor/plugins/tree/main/pstack), adapted for Codex. Deliberate design, small changes, independent review, and proof against the real app.

## Install

Requires a Codex version with `codex plugin` support.

```sh
codex plugin marketplace add mcansh/pstack-codex
codex plugin add pstack@mcansh-pstack
```

Restart the Codex session so its skill catalog refreshes. In Codex, invoke the installed skill name shown by autocomplete:

```text
$pstack:poteto-mode reproduce this bug, fix its root cause, and verify the user flow.
```

If Codex shows a namespaced skill name, use that exact name. `$poteto-help` explains the workflows. `$setup-pstack` optionally configures supported models per role in `~/.config/pstack/codex-models.md`. Setup is not required: every role inherits the current model.

## What is included

All 54 upstream top-level skills, the 23 poteto-mode playbooks, principle references, two delegate prompt files, and the plan checker, PR watcher, orchestration store, and worktree audit tools. Run tools only when a workflow needs them. The TypeScript tools require Bun; PR operations also require authenticated `gh` or the upstream optional `origin` CLI. The worktree audit additionally needs Bash, Git, jq, and standard Unix tools.

The [Codex runtime contract](skills/codex-runtime.md) is read by every skill. It maps workflow concepts to the actual tools exposed in the session, respects agent limits, gives writers separate scopes, and keeps independent verification gates blocked when no independent agent exists. Same-model panels are independent attempts, not evidence of model diversity.

This port does not supply Cursor Custom Modes, Grok Bot routines, Benny automations, a cloud-agent service, or a persistent overnight scheduler. Cloud and unattended workflows require capabilities provided by the host; installing skills cannot create them. `make-bot-ui` requires an existing documented webhook integration. See [compatibility](docs/COMPATIBILITY.md).

## Check the package

```sh
python3 scripts/check-plugin.py
cd skills/poteto-mode/scripts
bun install --frozen-lockfile
bun run test
bun run typecheck
```

The package check validates portable and Codex metadata, skill names and runtime pointers, local Markdown links, absence of Cursor settings paths, and the worktree audit's behavior on a disposable Git repository. It does not exercise model behavior, remote agents, live PR operations, or every playbook.

## Upstream

MIT licensed. Copyright remains with Lauren Tan. [docs/UPSTREAM.json](docs/UPSTREAM.json) records the source revision and version. This port has its own version sequence beginning at `0.1.0`; it is not an official Cursor or OpenAI plugin.

The original README and guide are preserved under [docs/upstream](docs/upstream/README.md) as historical Cursor documentation. Follow this README and the runtime contract for Codex installation and capabilities.
