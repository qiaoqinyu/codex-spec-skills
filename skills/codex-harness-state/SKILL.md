---
name: codex-harness-state
description: Create and maintain project-local state, handoff, and experiment tracking files for Codex workflows. Use when a repository needs `.agents/state/*`, progress logs, session continuity, or experiment/workstream lifecycle scaffolding across interruptions or parallel tracks. This is a harness state-layer skill, not a durable-doc capture or guidance reconciliation tool.
---

# Codex Harness State

Build and maintain the mutable state layer that sits beside durable Codex
guidance.

This skill is for session continuity, progress tracking, handoff, and
experiment or workstream lifecycle management. It does not replace `AGENTS.md`
or `specs/*.md`, but it may add a tiny `AGENTS.md` pointer so the state layer
is discoverable.

Human shortcut: use this for "continue the task", "set up a handoff", or
"keep parallel tracks straight".

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

- the user wants to write or broadly rewrite stable facts in `AGENTS.md` or
  `specs/*.md`
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
- make the route decision explicit: say why this is a `state` run and why it is
  not a durable-doc capture or doc-structure repair run
- keep stable truth in `AGENTS.md`, `specs/*.md`, and skill references; keep
  mutable progress and handoff material in state files
- if this skill creates or materially refreshes `.agents/state/*`, check
  whether `AGENTS.md` has a minimal runtime-state pointer
- if the pointer is missing and `AGENTS.md` is otherwise coherent, add only a
  short routing note into `AGENTS.md` that points to
  `.agents/state/session-handoff.md` first and `.agents/state/progress.md`
  second
- keep that `AGENTS.md` note tiny and routing-only; do not copy mutable state
  content into durable docs
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
- every update should capture:
  - `baseline`
  - `changed_variables`
  - `invariants`
  - `artifact_paths`
  - `evidence`
  - `certainty`
  - `outcome`
  - `next_action`
  - `updated_at`
- use the shared outcome vocabulary:
  - `keep`: the track or state update is worth keeping as the current truth
  - `discard`: the track or hypothesis was invalidated
  - `no-op`: nothing new should be written, but the state may still be checked
  - `handoff`: the state reveals a durable-doc or structure problem that should
    move to another skill
- keep `session-handoff.md` action-oriented: where to resume, what to run, what
  changed, and what is unresolved
- state can nominate a verified candidate for later promotion, but it does not
  itself promote durable rules into `AGENTS.md` or `specs/*.md`
- if the real gap is stable repo guidance, say so and hand off to
  `$codex-md-capture` or `$codex-md-reconcile`
- if `AGENTS.md` is missing, badly stale, or needs more than a tiny routing
  note, stop and hand off the guidance repair portion to `$codex-md-reconcile`
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
  verified changes, blockers, next checkpoints, and what evidence currently
  supports the state
- `session-handoff.md` should state how to resume safely in the next session
- `experiment-board.json` should list each active track with its status,
  baseline, changed variables, invariant checks, artifact paths, evidence,
  certainty, outcome, untouched scope, and next action
- if `AGENTS.md` exists and lacks a runtime-state pointer, add the smallest
  routing note needed so future sessions can discover `.agents/state/*`

### 4. Reconcile the state files against reality

Before finalizing:

- confirm referenced paths exist
- confirm commands or scripts are real
- confirm status labels match observed evidence
- confirm `outcome` and `certainty` match the evidence you actually have
- mark missing artifacts or ambiguous results explicitly
- confirm any new `AGENTS.md` pointer matches the real state paths and does not
  over-describe them

### 5. Verify and keep the layer lean

After editing, verify:

- the scaffold is under `.agents/state/` unless intentionally adapted
- the files do not conflict with stable guidance docs
- any `AGENTS.md` change is limited to discoverability, not state duplication
- no secrets or bulky logs were copied in
- the board statuses use the allowed lifecycle states
- every active track has evidence, certainty, and an explicit outcome
- next-session resume steps are concrete enough to act on
