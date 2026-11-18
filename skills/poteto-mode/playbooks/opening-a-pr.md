### Opening a PR

Run this only when the user's task authorizes publishing. A read-only investigation or a plan does not authorize a PR. Otherwise report the local result and stop.

Work from an explicitly created git worktree off trunk, and keep unrelated work out of it. Rebase into small, landable commits only within the user's grant. Review the diff for unnecessary code before commit per the Codex runtime contract. Apply **technical-writing** and **unslop** to the title and body.

Title: `type(scope): subject`, naming a real symbol when one carries the change. Body: a one-minute briefing under 40 lines with these `##` headings in order, dropping empty ones: `## Why`, `## What changed`, `## Scope`, `## Tradeoffs` (only rejected alternatives a reviewer would otherwise ask about), `## Blast Radius`, `## Verification`.

Stack follow-ups by base branch. Prefer the run's PR tool when available, using its actual schema. Otherwise use `gh pr create`, or `origin pr create --status open` when Origin's CLI resolves the repository. Open ready unless the user requested a draft; set a supported `draft` field accordingly or use `--draft` with `gh`. Opening a PR does not start a babysit. An Autopilot owner whose brief explicitly assigns babysitting starts it after the code-ready report.
