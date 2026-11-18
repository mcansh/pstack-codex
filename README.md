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

All 58 upstream top-level skills, the 22 poteto-mode playbooks, principle references, two delegate prompt files, a shared worker brief, and the PR watcher and worktree audit tools. Run tools only when a workflow needs them. The PR watcher requires Bun. Statechart runs TypeScript on Node.js, Bun, or Deno. PR operations also require an available host integration, authenticated `gh`, or the upstream optional `origin` CLI. The worktree audit additionally needs Bash, Git, jq, and standard Unix tools.

Large or cross-cutting programs route to `figure-it-out`. Upstream removed the orchestration playbook and the Node plan checker; multi-phase planning now produces an evidence-backed checklist without that checker. The worker brief carries the Codex runtime, scope, authorization, and verification rules into delegates.

The [statechart skill](skills/statechart/SKILL.md) checks a TLA+ model and draws it as a Mermaid user flow, with the shortest path to each state that breaks a rule. Its scripts run on Node 22.18 to 22.x, Node 23.6 or later, Bun 1.1.5 or later, or Deno 2.0 or later. The first run can install TLC and Java with mise; or set `TLA2TOOLS` to `tla2tools.jar` and `JAVA` to a Java 11+ binary. Optional SVG rendering uses Pele as described in the skill.

The [Codex runtime contract](skills/codex-runtime.md) is read by every skill. It maps workflow concepts to the actual tools exposed in the session, respects agent limits, gives writers separate scopes, and keeps independent verification gates blocked when no independent agent exists. Same-model panels are independent attempts, not evidence of model diversity.

This port does not supply Cursor Custom Modes, Grok Bot routines, Benny automations, the upstream Claude Code harness adapter, a cloud-agent service, or a persistent overnight scheduler. The Codex runtime contract is this fork's harness adapter. Cloud and unattended workflows require capabilities provided by the host; installing skills cannot create them. `make-bot-ui` requires an existing documented webhook integration. See [compatibility](docs/COMPATIBILITY.md).

## Check the package

```sh
python3 scripts/check-plugin.py
node --disable-warning=ExperimentalWarning --test skills/statechart/scripts/test/*.test.ts
cd skills/poteto-mode/scripts
bun install --frozen-lockfile
bun run test
bun run typecheck
```

The package check validates portable and Codex metadata, skill names and runtime pointers, local Markdown links, and the absence of Cursor settings paths.
It also checks the documented README skill and playbook counts, the documented `node --test` globs and other check commands, and the worktree audit's behavior on a disposable Git repository.
It does not exercise model behavior, remote agents, live PR operations, or every playbook.
The Node suite skips TLC cases unless `TLA2TOOLS` is set. Its render tests install Pele and mermaid with npm on every run.

## Upstream

### Sync upstream changes

In this source checkout, ask Codex to use `$sync-upstream`, or say "sync pstack with upstream and adapt the changes for Codex."
The [repository skill](.agents/skills/sync-upstream/SKILL.md) fetches upstream changes, resolves conflicts, and reviews Codex compatibility before applying them.

To prepare the update manually, run:

```sh
python3 scripts/sync-upstream.py prepare
```

Requires Python 3, Git, and authenticated `gh` with access to GitHub. Use `--ref <commit-or-branch>` to select a revision.
The command merges against the revision in `docs/UPSTREAM.json` and preserves this fork's Codex edits.
Review the candidate in `.pstack/upstream-sync/tree` and its `plan.json`, then adapt any new Cursor instructions and resolve conflicts.
New skills receive the Codex runtime pointer automatically. Their instructions still need a compatibility review.
When the adapted candidate changes anything this README documents, update `README.md` in the candidate before apply.

After review, run:

```sh
python3 scripts/check-plugin.py --root .pstack/upstream-sync/tree
python3 scripts/sync-upstream.py apply --reviewed
python3 scripts/check-plugin.py
```

Apply validates the candidate and refuses local file changes made since preparation. Upstream provenance advances when the update is applied.
When upstream pstack content is unchanged, the candidate preserves all files, including upstream provenance; applying it makes no edits.
Use a fresh `--stage <directory>` for subsequent updates. Neither command commits or publishes changes.
For offline verification, `--source <local-git-repository>` reads revisions from a repository containing `pstack/`.

Run the sync regression suite with `python3 scripts/test-sync-upstream.py`.

### Schedule upstream updates

The [sync workflow](.github/workflows/sync-upstream.yml) checks upstream every four hours at midnight, 4 a.m., 8 a.m., noon, 4 p.m., and 8 p.m. America/Detroit (Eastern time, adjusted for daylight saving time). You can also run **Sync upstream pstack** manually from the Actions tab. It is `schedule` and `workflow_dispatch` only, and the adaptation job runs only on the default branch. Those triggers are what keep a fork pull request from starting it. The adaptation job and the publish job both run on GitHub-hosted `ubuntu-latest`. Adaptation needs `ubuntu-latest` because the pinned Pullfrog action's restricted shell needs Linux `unshare` PID namespaces. The publish job downloads the validated patch artifact and opens the draft PR. Checksums use `shasum`.
When upstream changes exist, [Pullfrog](https://docs.pullfrog.com/headless-action) runs the adaptation using your connected ChatGPT Codex subscription.
The adaptation must keep this README current when the candidate changes documented facts.
The workflow validates the result and opens a draft PR on `automation/sync-upstream`. Review and merge that PR to update the plugin.
Checks skip Codex when no mapped upstream files changed or an update PR is already open.

To enable the workflow after merging it into the default branch:

1. Install the [Pullfrog GitHub App](https://pullfrog.com) for this repository. The sync workflow invokes Pullfrog directly; `pullfrog.yml` handles general tasks.
2. From this checkout, run `npx pullfrog auth codex` and complete the ChatGPT sign-in. Pullfrog stores and refreshes a separate credential; do not upload your local `auth.json` or add an `OPENAI_API_KEY` secret for this workflow. Subscription usage limits still apply.
3. In **Settings > Actions > General > Workflow permissions**, enable **Allow GitHub Actions to create and approve pull requests**.
4. In Pullfrog's repository console, choose **Custom (set in workflow)** for the model. The workflow defaults to `openai/gpt-sol`; optionally set the repository variable `UPSTREAM_SYNC_MODEL` to another [Pullfrog OpenAI model specifier](https://docs.pullfrog.com/models).

Change the workflow's cron expression to adjust the cadence. Failed runs retain the staged candidate and Codex summary as artifacts for diagnosis.
The adaptation job has a read-only GitHub workflow token and OIDC permission for Pullfrog's credential exchange. Pullfrog runs with pushes disabled and shell isolation enabled. A separate job opens the PR after validation; the workflow does not merge it.

Run the workflow helper tests with `python3 scripts/test-sync-action.py`.

### General Pullfrog tasks

The [Pullfrog workflow](.github/workflows/pullfrog.yml) accepts tasks from the Pullfrog console and its configured GitHub event automations. After installing the app, click **Verify manual installation** in the repository's Pullfrog console. Select your connected ChatGPT Codex subscription and model there.

You can also run **Pullfrog** from the Actions tab with a prompt and optional run name. Agent pushes are limited to feature branches, and shell isolation stays enabled. That workflow stays on GitHub-hosted `ubuntu-latest`.

MIT licensed. Copyright remains with Lauren Tan. [docs/UPSTREAM.json](docs/UPSTREAM.json) records the source revision and version. This port has its own version sequence beginning at `0.1.0`; it is not an official Cursor or OpenAI plugin.

The original README and guide are preserved under [docs/upstream](docs/upstream/README.md) as historical Cursor documentation. Follow this README and the runtime contract for Codex installation and capabilities.
