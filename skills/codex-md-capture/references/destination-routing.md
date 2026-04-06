# Destination Routing

Route each learning to the narrowest stable home.

## Decision Table

### handoff to `$codex-harness-state`

Use when:

- the request is mainly about progress tracking, session continuity, or resume
  instructions
- the key artifact is a mutable track, experiment board row, or handoff note
- the learning cannot stand on its own without current run context
- the immediate need is to strengthen the state layer before any durable
  write-back

Do not force mutable run state into `AGENTS.md` or `specs/*.md`.

### `AGENTS.md`

Use for:

- durable repo-wide instructions
- approval boundaries
- exact validation commands that matter on many tasks
- routing guidance to deeper docs

Avoid putting topic detail or long background here.

### `specs/<topic>.md`

Use for:

- topic-specific workflows
- recurring gotchas for one domain
- architecture, data, environment, review, or deployment details
- examples that only matter for that topic

Prefer updating an existing topic file before creating a new one.

### skill `references/`

Use only when:

- the learning is about a reusable skill workflow rather than repository truth
- the rule belongs to the skill itself, not the active project

### handoff to `$codex-md-reconcile`

Use when:

- the learning mainly exposes stale routing or duplicated ownership
- the canonical home is unclear without restructuring
- a missing navigation layer or ambiguous layout is the real problem
- the repository needs a guidance repair, not a factual write-back

### `~/.codex/AGENTS.md`

Use only for:

- user-personal defaults
- local preferences that should not be committed to the repository

## Why-Not-Elsewhere Rule

For every accepted learning, state:

- why this destination is the canonical home
- why the learning does not belong in the next-most-plausible home

If the answer is unclear, do not guess. Escalate to `$codex-md-reconcile`.
