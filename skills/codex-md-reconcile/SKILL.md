---
name: codex-md-reconcile
description: Reconcile Codex guidance files such as `AGENTS.md`, `specs/*.md`, and related repo skills. Use when the user asks to check, reconcile, optimize, condense, reorganize, repair, or bootstrap project instructions for Codex, especially when some guidance already exists but routing is unclear or key files are missing.
---

# Codex MD Reconcile

Reconcile Codex guidance with findings first and edits second.

This skill is for repository-level reconciliation, bootstrap, migration, and
organization work. It is not the default tool for writing back one session's
learnings.

## Use This Skill When

- the user asks to reconcile, repair, or improve the active Codex guidance surface
- `AGENTS.md` and `specs/*.md` exist but are incomplete, stale, duplicated, or poorly routed
- some Codex guidance exists, but key files or navigation are missing and need minimal bootstrap
- `AGENTS.md` does not clearly route to the canonical `specs/*.md` files
- the user explicitly asks for Claude-to-Codex migration or cross-surface reconciliation

## Do Not Use This Skill When

- the task is only to capture new learnings from the current session
- the repository structure is already good and only needs a small factual
  update
- the user mainly wants to write back one or two newly discovered commands or
  gotchas
- the repository still contains Claude-oriented files, but the user did not
  ask for Claude-to-Codex migration or cross-surface reconciliation

Use `$codex-md-capture` for session delta write-back.

## Core Model

For Codex-oriented repositories, prefer this layered model:

- `AGENTS.md`
  - durable repo-wide instructions
  - boundaries and approvals
  - exact validation commands
  - routing to deeper docs
- `specs/*.md`
  - topic-specific background, workflows, constraints, and recurring gotchas
- repo or user skills
  - reusable workflows, not the main home for repository truth

Default bias:

- keep `AGENTS.md` short
- route topic detail into `specs/*.md`
- do not introduce a separate `rules` subsystem unless the user explicitly
  wants one
- do not introduce `specs/index.md` by default; only keep it when the
  repository already uses it well or routing has genuinely outgrown
  `AGENTS.md`

## Workflow

### 1. Discovery

Inspect the real guidance surface:

```bash
find . -name "AGENTS.md" 2>/dev/null | head -50
find specs -name "*.md" 2>/dev/null | sort
find .agents/skills -name "SKILL.md" 2>/dev/null | head -50
```

Only if the user explicitly asks for Claude-to-Codex migration or
cross-surface reconciliation, also inspect legacy Claude surfaces when
present:

```bash
find . -name "CLAUDE.md" -o -path "*/.claude/rules/*.md" 2>/dev/null | head -50
```

Check:

- which file is the real entrypoint
- whether `AGENTS.md` tells Codex that `specs/*.md` exists and where to start
- whether `AGENTS.md` is carrying too much topic detail
- whether `specs/*.md` has clear topic boundaries
- whether any guidance is duplicated or contradictory
- whether legacy Claude concepts are still being described as if Codex supported
  them natively

By default, ignore Claude-specific surfaces such as `CLAUDE.md`,
`.claude/rules/*.md`, and `docs/claude/*`. Do not audit, sync, or clean them
unless the user explicitly asks for migration or cross-surface alignment.

### 2. Reality Check

Verify guidance against the actual repository:

- commands from manifests or scripts
- current paths and directory layout
- environment setup from config files
- validation steps that actually run
- dangerous operations that need approval

If guidance conflicts with executable repo reality, trust the repo and mark the
docs stale.

### 3. Quality Assessment

Use [references/quality-criteria.md](references/quality-criteria.md).

Always produce findings before proposing edits.

Report shape:

```md
## Codex Guidance Report

### Summary
- entrypoint files: X
- specs files: X
- key risk: ...

### Must Fix
- ...

### Should Improve
- ...

### Proposed Changes
1. ...
```

### 4. Draft Targeted Changes

Apply the routing guidance in
[references/organization-patterns.md](references/organization-patterns.md)
only when restructuring is justified.

Priorities:

1. fix stale or incorrect guidance
2. add or repair `AGENTS.md` routing into `specs/*.md` when it is missing
3. clarify routing and canonical ownership
4. shrink `AGENTS.md` if it carries too much topic detail
5. leave good-enough structure alone

Show each proposed change as a diff or replacement block.

### 5. Apply With Approval

Before editing, show:

- which file will change
- why the change helps future Codex sessions
- the exact diff or replacement block

After approval, update files and re-check key paths, commands, and routing.

## Migration Rules

When porting from Claude-oriented guidance:

- replace `CLAUDE.md` with `AGENTS.md`
- replace `@import` semantics with explicit markdown references and routing
- replace `.claude/rules/*.md` with topic files under `specs/*.md` unless the
  user explicitly wants to preserve a rules directory
- replace `.claude.local.md` usage with `~/.codex/AGENTS.md` only for personal
  defaults
- do not claim Codex auto-loads arbitrary markdown files outside its `AGENTS.md`
  discovery model
- if `specs/*.md` exists but `AGENTS.md` does not route into it, treat that as
  a must-fix and add a minimal navigation block

Outside explicit migration work:

- do not treat `CLAUDE.md`, `.claude/rules/*.md`, or `docs/claude/*` as part of
  the active Codex guidance surface
- do not flag Claude-only files as stale, duplicated, or contradictory unless
  the user asked for migration or cross-surface cleanup

## Common Problems To Flag

- `AGENTS.md` does not mention `specs/*.md` even though the repo uses it
- `AGENTS.md` repeats large blocks from `specs/*.md`
- topic knowledge has no clear canonical home
- safety rules are buried inside architecture or history docs
- legacy Claude terms remain in a Codex repo without explanation
- a new abstraction such as `rules/` was introduced without a real need
- long historical logs crowd out durable guidance
- experimental findings live only in `results/` paths with no journal or
  promoted durable conclusion

## References

- Use [references/quality-criteria.md](references/quality-criteria.md) for
  scoring and issue patterns.
- Use [references/organization-patterns.md](references/organization-patterns.md)
  for routing and migration choices.
- Use [references/templates.md](references/templates.md) for starter layouts.
