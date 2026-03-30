---
name: codex-md-capture
description: Capture durable learnings from the current session and propose concise updates to Codex guidance files. Use when the user asks to summarize this session, update project memory, write back new commands or gotchas, or turn conversation learnings into persistent guidance in `AGENTS.md`, `specs/*.md`, or related skill references.
---

# Codex MD Capture

Capture session learnings as a narrow, verified write-back.

This skill is for incremental memory capture. It is not a doc audit, migration,
or broad rewrite tool.

## Use This Skill When

- the current session revealed commands, workflows, gotchas, or constraints
  worth preserving
- the user wants to update project memory after a debugging or coding session
- the user wants to convert conversation learnings into `AGENTS.md` or
  `specs/*.md`
- the repository already has a working Codex guidance surface and needs a
  narrow write-back

## Do Not Use This Skill When

- the repository guidance needs a broad audit or migration
- the current structure is stale, duplicated, or contradictory across many
  files
- the user wants a large rewrite of `AGENTS.md` or `specs/*.md`
- the repository has Claude-oriented legacy files, but the user did not ask to
  migrate or reconcile them

Use `$codex-md-reconcile` for structure cleanup, migration, or broader
organization work.

## Operating Rules

- only capture learnings that satisfy the write-back gate in
  [references/capture-rubric.md](references/capture-rubric.md)
- use the routing table in
  [references/destination-routing.md](references/destination-routing.md)
  before drafting edits
- use the output contract in
  [references/output-template.md](references/output-template.md)
- use [references/examples.md](references/examples.md) to distinguish
  write-back from `no-op`
- if no learning passes the gate, return a clear `no-op` result and stop
- prefer append-only, minimal additions over rewriting large sections
- do not invent a new rules layer unless the repository already uses one and
  the user explicitly wants to keep it
- ignore Claude-specific surfaces such as `CLAUDE.md`, `.claude/rules/*.md`,
  and `docs/claude/*` unless the user explicitly asks for Claude-to-Codex
  migration or cross-surface reconciliation

## Workflow

### 1. Collect candidate learnings

Extract the smallest set of session outcomes that might be worth preserving.

### 2. Apply the write-back gate

Keep only learnings that are:

- verified
- repeated or likely to recur
- durable beyond the current session
- relevant to the repository rather than generic advice

Return `no-op` if nothing survives this filter.

### 3. Find the canonical home

For each surviving learning:

- choose the narrowest stable destination
- state why that destination wins
- state why the learning does not belong in the other likely destinations

If the session reveals missing routing or stale structure rather than a simple
write-back, hand off to `$codex-md-reconcile`.

### 4. Draft a minimal proposal

Use the template in [references/output-template.md](references/output-template.md).

Always include:

- learning
- evidence
- destination
- why-not-elsewhere
- validation
- confidence

### 5. Apply with approval and verify

Only edit approved files.

After applying, verify:

- the target path is real
- the added guidance is not duplicate or contradictory
- `AGENTS.md` stays short and routing-focused
- no temporary or low-confidence material leaked into long-term docs
