---
name: codex-md-capture
description: Capture durable learnings from the current session and propose concise updates to Codex guidance files. Use when the user asks to summarize this session, update project memory, write back new commands or gotchas, or turn conversation learnings into persistent guidance in `AGENTS.md`, `specs/*.md`, or related skill references.
---

# Codex MD Capture

Capture durable session outcomes and route them into the right Codex guidance
layer.

This skill is incremental. It turns one session's learnings into proposed
updates. It does not perform a broad documentation audit or redesign.

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

## Routing Model

Route each learning to the narrowest stable home:

- `AGENTS.md`
  - durable repo-wide instructions
  - high-priority boundaries
  - exact validation commands
  - routing guidance to topic docs
- `specs/*.md`
  - topic-specific background, workflows, constraints, or repeated gotchas
  - examples: `specs/architecture.md`, `specs/data.md`, `specs/review.md`
- skill `references/`
  - only when the learning is specific to a reusable skill workflow rather than
    the repository itself
- `~/.codex/AGENTS.md`
  - only for user-personal defaults that should not be stored in repo docs

Do not invent a separate `rules` layer unless the repository already has one
and the user explicitly wants to keep it.

Ignore Claude-specific surfaces such as `CLAUDE.md`, `.claude/rules/*.md`, and
`docs/claude/*` unless the user explicitly asks for Claude-to-Codex migration
or cross-surface reconciliation.

## What To Capture

Capture only high-signal outcomes that will help a future agent:

- verified commands or environment setup corrections
- confirmed architecture or path discoveries
- durable safety constraints and approval boundaries
- recurring failure modes and their fixes
- reusable review or validation steps
- clarified routing about which document to read for which task

Do not capture:

- raw debugging chatter
- uncertain hypotheses
- one-off outputs with no future value
- generic advice that is not specific to the repository

## Workflow

### 1. Reflect on the Session

Identify what was missing at the start of the session that would have made the
work faster or safer.

Focus on:

- commands discovered or corrected
- repo-specific patterns
- non-obvious gotchas
- environment quirks
- testing or review steps that proved useful

### 2. Find the Canonical Home

Prefer updating an existing file over creating a new one.

- put repo-wide instructions in `AGENTS.md`
- put topic detail in an existing `specs/<topic>.md`
- create a new `specs/<topic>.md` only if no good home exists and the topic is
  likely to recur
- if the session reveals that the repo is missing basic `AGENTS.md` to
  `specs/*.md` routing, propose handing the structural fix to
  `$codex-md-reconcile` rather than inventing a full layout here

### 3. Draft Minimal Additions

Keep additions dense and durable.

Preferred format:

- `<command or rule>` - `<brief purpose or caution>`
- short bullets over paragraphs
- examples only when they remove ambiguity

### 4. Show Proposed Changes First

For each target file, show:

```md
### Update: <file path>
**Why:** <one-line reason>
**Layer:** <AGENTS.md | specs | skill reference | personal global>

Diff:

    + <addition>
```

If a new file is truly needed, show the full proposed contents.

### 5. Apply With Approval

Only edit the files the user approves.

After applying, verify:

- paths and filenames in the added guidance are real
- the target file still reads cleanly
- `AGENTS.md` stays short and routing-focused

## Distillation Rules

- prefer verified repository truth over intent or aspiration
- keep one concept per bullet when possible
- capture stable lessons, not session transcript noise
- if a detail only matters for one topic, move it into `specs/<topic>.md`
- if the same mistake happened twice, bias toward capturing it

## Output Shape

1. Session learnings worth keeping
2. Proposed destination for each learning
3. Diff or inserted block per file
4. Validation notes after approval and apply
