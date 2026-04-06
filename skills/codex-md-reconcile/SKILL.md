---
name: codex-md-reconcile
description: Reconcile Codex guidance files such as `AGENTS.md`, `specs/*.md`, and related repo skills. This is a harness-aware guidance-layer skill for routing, ownership, and structure repair, not a full harness or lifecycle builder.
---

# Codex MD Reconcile

Reconcile Codex guidance with findings first, edits second, and verification
last.

This skill is for repository-level reconciliation, bootstrap, migration, and
organization work. It is not the default tool for writing back one session's
learnings.

This is a harness-aware guidance-layer skill. It owns `AGENTS.md` plus
`specs/*.md` routing, canonical ownership, and structure repair, not session
state, handoff logs, bootstrap scripts, feature trackers, or runtime
verification scaffolding. It may still route `AGENTS.md` into an existing
`.agents/state/*` layer so that mutable state is discoverable.

Human shortcut: use this for "organize the docs", "repair routing", or "clean
up guidance ownership".

## Use This Skill When

- the user asks to reconcile, repair, or improve the active Codex guidance
  surface
- `AGENTS.md` and `specs/*.md` exist but are incomplete, stale, duplicated, or
  poorly routed
- some Codex guidance exists, but key files or navigation are missing and need
  minimal bootstrap
- `AGENTS.md` does not clearly route to the canonical `specs/*.md` files
- the user explicitly asks for Claude-to-Codex migration or cross-surface
  reconciliation

## Do Not Use This Skill When

- the task is only to capture new learnings from the current session
- the repository structure is already good and only needs a small factual
  update
- the user mainly wants to write back one or two newly discovered commands or
  gotchas
- the repository still contains Claude-oriented files, but the user did not ask
  for Claude-to-Codex migration or cross-surface reconciliation
- the user mainly needs progress tracking, session handoff, `init.sh`,
  feature-tracking artifacts, or verification scaffolding for an agent
  workflow
- the underlying problem is missing lifecycle/state machinery rather than stale
  or poorly routed guidance

Use `$codex-md-capture` for session delta write-back.

## Operating Rules

- follow the five-stage workflow in
  [references/reconcile-workflow.md](references/reconcile-workflow.md)
- score the guidance surface with
  [references/quality-criteria.md](references/quality-criteria.md)
- make the route decision explicit: say why this is a `reconcile` run and why
  it is not a narrow write-back or mutable-state request
- classify the repository layout before proposing repairs:
  `default_codex_shape`, `coherent_alt_router`, `migration_mixed`, or
  `broken_or_stale`
- use [references/organization-patterns.md](references/organization-patterns.md)
  only when restructuring is justified
- decide canonical ownership with
  [references/canonical-home-rules.md](references/canonical-home-rules.md)
- verify every proposed repair with
  [references/verification-checklist.md](references/verification-checklist.md)
- use [references/examples.md](references/examples.md) to avoid over-repair
- if `.agents/state/*` exists and is part of the active workflow, treat a tiny
  `AGENTS.md` pointer into it as compatible guidance routing rather than as
  state ownership
- use the shared outcome vocabulary:
  - `keep`: propose the minimal repair
  - `discard`: reject a repair idea that is not supported by repo reality
  - `no-op`: the current structure is already coherent enough to leave alone
  - `handoff`: the real problem is state continuity or narrow durable write-back
- treat a coherent alternative router stack as compatible unless it is causing
  confusion, duplication, or stale guidance
- include proof of work in the report: files inspected, routers checked,
  commands used, and open ambiguities
- if the real gap is session continuity, state tracking, bootstrap, or
  verification scaffolding, call that out explicitly instead of over-repairing
  the guidance surface
- default to the smallest useful change set
- do not introduce a separate `rules/` subsystem unless the user explicitly
  wants one
- do not introduce `specs/index.md` by default; only keep or add it when
  routing has genuinely outgrown direct `AGENTS.md` navigation

## Workflow

### 1. Discover and classify the real guidance surface

Inspect what actually exists before making any recommendation.

At minimum, find:

- `AGENTS.md` or `AGENT.md` entrypoints
- `specs/*.md`
- active `.agents/state/*` files when the repository uses a state layer
- secondary routers such as `WORKSPACE.md`, `specs/index.md`, or subtree
  `INDEX.md` files
- relevant skill references
- legacy Claude surfaces only when the user explicitly asked for migration

Classify the shape before recommending change:

- `default_codex_shape`
- `coherent_alt_router`
- `migration_mixed`
- `broken_or_stale`

### 2. Reality-check against the repository

Trust executable repo reality over stale docs.

Check:

- commands from manifests or scripts
- real paths and directories
- environment setup from config files
- dangerous operations and approval boundaries
- dirty-worktree context when it affects the docs

### 3. Score and classify findings

Produce findings before proposing edits.

Every issue should land in one of:

- `must fix`
- `should improve`
- `leave alone`

If the best answer is "leave the structure alone", say `no-op` explicitly.

### 4. Propose the minimal repair

Use the template in
[references/reconcile-workflow.md](references/reconcile-workflow.md).

Default priorities:

1. fix stale or incorrect guidance
2. repair missing routing into existing topic docs
3. add a tiny runtime-state pointer when `.agents/state/*` exists but is
   invisible from `AGENTS.md`
4. clarify canonical ownership
5. shrink `AGENTS.md` when it carries topic detail
6. leave good-enough structure alone

If the repository uses a coherent alternative router stack, prefer clarifying
roles and reducing confusion over normalizing it to the default shape.

Every proposal should also make explicit:

- why this belongs to `codex-md-reconcile`
- why it is not a `codex-md-capture` or `codex-harness-state` task
- touched scope versus untouched scope
- expected outcome: `keep`, `no-op`, or `handoff`

### 5. Apply with approval and verify

Before editing, show:

- which file will change
- why the change helps future Codex sessions
- the exact diff or replacement block

After approval, re-check the repository using
[references/verification-checklist.md](references/verification-checklist.md).

## Migration Rules

When porting from Claude-oriented guidance:

- replace `CLAUDE.md` with `AGENTS.md`
- replace `@import` semantics with explicit markdown references and routing
- replace `.claude/rules/*.md` with topic files under `specs/*.md` unless the
  user explicitly wants to preserve a rules directory
- replace `.claude.local.md` usage with `~/.codex/AGENTS.md` only for personal
  defaults
- do not claim Codex auto-loads arbitrary markdown files outside its
  `AGENTS.md` discovery model
- if `specs/*.md` exists but `AGENTS.md` does not route into it, treat that as
  a must-fix and add a minimal navigation block
- if `.agents/state/*` exists and is actively used but `AGENTS.md` does not
  mention it at all, treat a tiny runtime-state pointer as `should improve`
  unless the repo already has another coherent state router

Outside explicit migration work:

- do not treat `CLAUDE.md`, `.claude/rules/*.md`, or `docs/claude/*` as part
  of the active Codex guidance surface
- do not flag Claude-only files as stale, duplicated, or contradictory unless
  the user asked for migration or cross-surface cleanup
- do not rewrite a coherent alternative router stack solely to match the
  default `AGENTS.md` plus `specs/*.md` pattern
