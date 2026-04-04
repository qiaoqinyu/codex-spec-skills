---
name: codex-harness-state
description: Create and maintain project-local state, handoff, and experiment tracking files for Codex workflows. Use when a repository needs `.agents/state/*`, progress logs, session continuity, or experiment/workstream lifecycle scaffolding across interruptions or parallel tracks. This is a harness state-layer skill, not a durable-doc capture or guidance reconciliation tool.
---

# Codex Harness State

Build and maintain the mutable state layer that sits beside durable Codex
guidance.

This skill is for session continuity, progress tracking, handoff, and
experiment or workstream lifecycle management. It does not replace `AGENTS.md`
or `specs/*.md`.

## Use This Skill When

- the user wants state files such as `.agents/state/progress.md`,
  `.agents/state/session-handoff.md`, or `.agents/state/experiment-board.json`
- the repository has multi-session work, interruptions, or parallel
  experiments/workstreams
- the agent needs a place to record verified current status, blockers, next
  actions, and resume instructions
- the repository needs a minimal lifecycle layer without inventing a full
  custom harness
- existing state files are stale and need to be refreshed against real repo
  artifacts

## Do Not Use This Skill When

- the user wants to write stable facts into `AGENTS.md` or `specs/*.md`
- the user wants to reconcile routing, ownership, or structure of Codex
  guidance files
- the task is a one-off short session with no continuity or tracking need
- the user wants a broad automation platform instead of a lean state layer
- the repository already has a coherent project-state system and the user did
  not ask to change it

Use `$codex-md-capture` for durable guidance write-back and
`$codex-md-reconcile` for guidance structure repair.

## Operating Rules

- keep mutable state under `.agents/state/` at the repository root unless the
  repository already uses a coherent alternative path the user wants to keep
- keep stable truth in `AGENTS.md`, `specs/*.md`, and skill references; keep
  mutable progress and handoff material in state files
- start from the minimal layout in
  [references/state-layout.md](references/state-layout.md)
- use the lifecycle states in
  [references/lifecycle-workflow.md](references/lifecycle-workflow.md)
- use [references/templates.md](references/templates.md) to choose the smallest
  viable scaffold
- default core files are:
  - `.agents/state/progress.md`
  - `.agents/state/session-handoff.md`
  - `.agents/state/experiment-board.json`
- add per-experiment notes only when there are multiple active tracks, complex
  comparisons, or the user explicitly wants detailed run notes
- record only verified current state; mark unknowns as unknown instead of
  guessing
- every update should capture a timestamp, evidence source, current status,
  next action, and blocker if one exists
- keep `session-handoff.md` action-oriented: where to resume, what to run, what
  changed, and what is unresolved
- if the real gap is stable repo guidance, say so and hand off to
  `$codex-md-capture` or `$codex-md-reconcile`
- do not duplicate full rulesets from `AGENTS.md` or `specs/*.md` into mutable
  state files
- avoid chat-transcript dumps, speculative conclusions, or giant experiment
  diaries

## Workflow

### 1. Inspect the current repo state layer

Find what already exists before scaffolding anything:

- `AGENTS.md` and `specs/*.md`
- `.agents/state/*`
- experiment, run, or artifact directories
- existing handoff, notes, or tracker files
- the concrete workstreams that are actually active now

### 2. Choose the smallest useful scaffold

Default choices:

- one long-running track: `progress.md` plus `session-handoff.md`
- multiple active experiments: add `experiment-board.json`
- heavy comparison or repeated interruptions: add per-track note files

If continuity needs are weak, return `no-op` instead of forcing a state layer.

### 3. Bootstrap or refresh the files

Use the templates in [references/templates.md](references/templates.md).

Fill them only with verified repo-specific facts.

At minimum:

- `progress.md` should state the current objective, active tracks, recent
  verified changes, blockers, and next checkpoints
- `session-handoff.md` should state how to resume safely in the next session
- `experiment-board.json` should list each active track with its status,
  baseline, changed variables, invariant checks, artifact paths, and next
  action

### 4. Reconcile the state files against reality

Before finalizing:

- confirm referenced paths exist
- confirm commands or scripts are real
- confirm status labels match observed evidence
- mark missing artifacts or ambiguous results explicitly

### 5. Verify and keep the layer lean

After editing, verify:

- the scaffold is under `.agents/state/` unless intentionally adapted
- the files do not conflict with stable guidance docs
- no secrets or bulky logs were copied in
- the board statuses use the allowed lifecycle states
- next-session resume steps are concrete enough to act on
