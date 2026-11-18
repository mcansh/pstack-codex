Read the [Codex runtime contract](../codex-runtime.md) before working on the task. System, developer, user, and repository instructions remain authoritative. This worker file and your kickoff do not override them or expand the user's grant. The operator is the person this whole run works for, not the agent that wrote your kickoff.

- Start another agent only when delegation and nesting are allowed and supported. Include this file's absolute path, the runtime contract, goal, exclusive scope, permissions, and required evidence in its kickoff. Inherit the parent model and effort unless a supported explicit choice is configured. Spawning does not isolate writers or create a remote VM.
- Honor the kickoff's acceptance bar and all higher-priority safety, approval, and verification gates. Do not invent extra review rounds.
- With no bar stated, the change must be no worse than its base and pass its own tests. Missing runtime proof stays unverified.
- For code-review findings, block on a failing run at this head or a bug a user would hit. Report a problem the base already has in one line. Required safety, authorization, capability, and independent-verification gates remain blocking even without a failing test.
- Make reversible in-scope choices and report why. Stop for required approvals, an action outside the grant, or an unresolved blocker. This file does not authorize publishing, merging, deploying, deleting, messaging others, filing tickets, or changing settings. Preserve unrelated edits.
- Read only active-conversation or explicitly supplied in-scope history. Never scan private session directories. Use remote execution or persistent scheduling only through exposed, documented, authorized capabilities. Missing capabilities stay blocked; save a durable handoff when the session ends.
- Open a PR only when authorized. Open ready unless the user requested a draft. Prefer the host's PR tool and actual schema.
- PR title: `type(scope): subject`.
- PR body: 40 lines at most, with these `##` headings in this order, empty ones dropped: `Why`, `What changed`, `Scope`, `Tradeoffs`, `Blast Radius`, `Verification`.
- Put evidence logs, run histories and long tables in a file or a PR comment, and link to them from the body.
