# Codex runtime contract

Read this before executing a bundled workflow. This contract replaces upstream harness-specific instructions throughout pstack, including playbooks, templates, and delegate prompts. System, developer, user, and repository instructions remain authoritative.

## Skills and settings

Invoke skills with `$skill-name` or the installed namespaced name Codex shows. A workflow's `/skill-name` notation means read that bundled skill's `SKILL.md` and follow it; it does not assert a Codex slash command exists. Resolve sibling skills relative to the installed skill file, never a hard-coded plugin cache version.

Read `~/.config/pstack/codex-models.md` if present before selecting agents. It is ordinary Markdown read on demand, not an automatically loaded Cursor rule. Project skills belong in `.agents/skills/`; personal skills belong in `~/.agents/skills/`. Do not modify Codex's plugin cache to persist user configuration.

## Delegation and models

Use only the agent tools exposed in the current session. Upstream `Task` means the available spawn tool, not a literal tool name. Inspect its schema before calling it. `run_in_background`, `readonly`, `environment`, `cloud_base_branch`, and `subagent_type` are not portable arguments; omit them unless the actual tool supports them. Put read-only scope and prohibitions in the prompt. This is an instruction, not a sandbox guarantee.

The named agents are prompt files at `agents/poteto-agent.md` and `agents/comment-sicko.md`, not registered Codex agent types. Read the selected file and include its instructions and the absolute poteto-mode skill path in the delegate prompt. A general-purpose delegate needs no agent file.

Default every role to `inherit-parent`: omit model and reasoning overrides. An explicit role choice from `$setup-pstack` may select only models and efforts supported by the current spawn schema. Follow the tool's rules about context inheritance when supplying overrides. Never construct model IDs by appending effort or speed suffixes. If a configured model is unavailable, report it and inherit the parent. Never silently substitute a different vendor. A panel still gets independent reviewers when it inherits one model; call it independent review, not multi-model evidence. Different models may be requested only when the environment supports them.

Respect the session's agent count, nesting limit, write permissions, and delegation policy. Queue excess work. Each writer gets an exclusive scope or explicitly created worktree; spawning an agent does not create one. If delegation is absent or prohibited, do the work sequentially, disclose reduced independence, and never label self-review as independent verification. If a gate requires an independent verdict, that gate remains blocked.

Cloud placement is optional and capability-gated. Only use a remote agent API when it is exposed, documented, and authorized. Local agents do not imply isolated VMs, cloud persistence, or survival after session shutdown. Where a playbook needs a separate VM or persistent remote owner, stop that lane as blocked unless that environment exists; do useful local preparation without claiming completion. Store durable state in a project path allowed by the session; use a gitignored `.pstack/` directory when no store is supplied.

## Tools and external integrations

Map upstream Read, Grep, Shell, AskQuestion, and todo operations to the available read/search/exec, user-input, and plan tools. When no structured question tool exists, ask in chat. When no plan tool exists, keep a concise checklist. Upstream readonly mode does not determine MCP access in Codex: inspect actual connector availability.

`create-skill` means an available skill-authoring skill, or direct authoring with valid YAML `name` and `description`, existing relative links, and behavioral checks when needed. `deslop` means review the diff for unnecessary abstractions, duplication, dead code, and unrelated changes. `control-ui` and `control-cli` mean an available browser/native/terminal driver suited to the surface. These are capability descriptions, not dependencies on cursor-team-kit. Report missing runtime proof as unverified.

`/loop` and the loop skill mean a bounded task loop inside this session using available wait tools. There is no promise of an unattended wake, persistent scheduler, or overnight execution. Never invent a schedule or cloud agent. Grok Bot routines, webhook secret cards, and Benny Cursor automations are not implemented by this plugin. Do not use Cursor-only APIs or request credentials in chat.

Read only the active conversation or explicitly supplied, in-scope history via tools available in this session. There is no assumed transcript directory or JSONL format. If history is not exposed, use the visible conversation plus a user-supplied handoff and label the gap. Never scan global Codex or Cursor session directories to discover private chats. Transcript timestamps do not prove agent liveness. Query the available agent-status tool or ask the user before deleting a possibly active worktree.

## Authorization

A workflow is not authorization to publish, merge, deploy, delete data, send messages, file tracker issues, or alter account settings. Follow the user's actual grant and the session's approval requirements. Preserve unrelated edits. Never reset a dirty tree, force-remove a worktree, or overwrite a skill to avoid a conflict. Reflect may propose tracker items; file them only when authorized. Explicit approval already granted need not be requested again.
