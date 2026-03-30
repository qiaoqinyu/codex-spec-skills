---
name: codex-md-reconcile
description: Reconcile Codex guidance files such as `AGENTS.md`, `specs/*.md`, and related repo skills. Use when the user asks to check, reconcile, optimize, condense, reorganize, repair, or bootstrap project instructions for Codex, especially when some guidance already exists but routing is unclear or key files are missing.
---

# Codex MD Reconcile

Reconcile Codex guidance with findings first, edits second, and verification
last.

This skill is for repository-level reconciliation, bootstrap, migration, and
organization work. It is not the default tool for writing back one session's
learnings.

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

Use `$codex-md-capture` for session delta write-back.

## Operating Rules

- follow the five-stage workflow in
  [references/reconcile-workflow.md](references/reconcile-workflow.md)
- score the guidance surface with
  [references/quality-criteria.md](references/quality-criteria.md)
- use [references/organization-patterns.md](references/organization-patterns.md)
  only when restructuring is justified
- decide canonical ownership with
  [references/canonical-home-rules.md](references/canonical-home-rules.md)
- verify every proposed repair with
  [references/verification-checklist.md](references/verification-checklist.md)
- use [references/examples.md](references/examples.md) to avoid over-repair
- default to the smallest useful change set
- do not introduce a separate `rules/` subsystem unless the user explicitly
  wants one
- do not introduce `specs/index.md` by default; only keep or add it when
  routing has genuinely outgrown direct `AGENTS.md` navigation

## Workflow

### 1. Discover the real guidance surface

Inspect what actually exists before making any recommendation.

At minimum, find:

- `AGENTS.md` or `AGENT.md` entrypoints
- `specs/*.md`
- relevant skill references
- legacy Claude surfaces only when the user explicitly asked for migration

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

### 4. Propose the minimal repair

Use the template in
[references/reconcile-workflow.md](references/reconcile-workflow.md).

Default priorities:

1. fix stale or incorrect guidance
2. repair missing routing into existing topic docs
3. clarify canonical ownership
4. shrink `AGENTS.md` when it carries topic detail
5. leave good-enough structure alone

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

Outside explicit migration work:

- do not treat `CLAUDE.md`, `.claude/rules/*.md`, or `docs/claude/*` as part
  of the active Codex guidance surface
- do not flag Claude-only files as stale, duplicated, or contradictory unless
  the user asked for migration or cross-surface cleanup
