# Navigation Templates

Use these as starting points for thin adapter files. Adapt them to the actual
agent semantics of the target tool.

## General Rules

- Keep root adapters short.
- Point to `specs/index.md` first.
- Put shared truth in `specs/`, not repeated across agent files.
- Use relative paths inside `specs/index.md` to point to sibling spec files.
- Make `specs/index.md` route by scenario and task type.
- Only auto-import content that is needed in most sessions.
- If an agent lacks import support, keep the adapter as a precise map.
- After generating or updating `specs/`, normally sync the root adapter so the
  repository entrypoint actually points at `specs/index.md`.

## Template: `AGENTS.md`

Use this for Codex-style or generic agent entrypoints:

```md
# Agent Guide

This file is a navigation layer. Shared project truth lives in `specs/`.

## Start Here

- Before doing substantive work, read `specs/index.md`.
- Treat `specs/index.md` as the navigation hub.
- Follow only the relative paths relevant to the current task.
- Treat `specs/*.md` as the canonical shared project truth.
- If this file and `specs/*.md` appear inconsistent, prefer `specs/*.md`.

## Safety

- Ask before destructive operations.
- Prefer repo-verified commands over assumptions.
- If a constraint is enforceable in code or CI, keep it there.
```

## Template: `CLAUDE.md`

Use this when Claude supports `@import`. Only import content that truly belongs
in always-loaded context.

```md
# Role
You are working in a spec-first repository.

# Read First
@specs/index.md
```

If `specs/index.md` already routes well, avoid importing additional spec files
by default.

## Adapter Sync Rule

When `specs/` is newly created or substantially reorganized:

- update `AGENTS.md` to point to `specs/index.md`
- make `AGENTS.md` explicitly tell Codex to read `specs/index.md` before
  substantive work
- update `CLAUDE.md` to point to `specs/index.md` when Claude is in use
- keep the adapter thin; do not paste spec content back into the adapter
- skip this step only when the user explicitly requests specs-only output

## Template: `GEMINI.md`

Use a concise map when the agent relies on plain markdown rather than special
import syntax:

```md
# Repository Navigation

This repo uses `specs/` as the source of truth.

- Start with `specs/index.md`
- Follow the relative paths listed in `specs/index.md`
```

## Template: `specs/index.md`

Use this as the single routing document across agents:

```md
# Specs Index

## Read First

- Running, testing, verification: `./commands.md`
- Environment and paths: `./environment.md`
- Code structure and boundaries: `./architecture.md`

## Optional Project Topics

- Model training and experiments: `./training.md`
- Data pipeline and preprocessing: `./data-handling.md`
- Frontend implementation: `./frontend.md`
- LLM or agent workflows: `./llm-agents.md`

## Archive

- Historical experiment notes: `./experiment-archive.md`
```

The point is not to list every file. The point is to help the agent decide what
to read next for the current scenario.

## Template: Claude Compatibility Shim

Use this only when migrating from an older Claude Code setup and a scoped file
is still temporarily useful:

```md
---
paths:
  - "src/data/**"
  - "scripts/data/**"
---
# Data Handling

This file is only a router. Shared truth lives in:

- `specs/index.md`
```

Keep compatibility shims extremely short. Do not duplicate the full domain
spec.

## Template: Nested Local Adapter

Use nested agent files only when a subtree really has distinct local rules:

```md
# Local Agent Guide

This subtree follows the shared repo specs plus these local additions:

- Parent knowledge base: `../../specs/index.md`
- Relevant local spec files should also be listed from `../../specs/index.md`
```

## Adapter Smells

Refactor the adapter if you see:

- Long prose that restates `specs/`
- Run-by-run history in the adapter
- Different agents carrying different versions of the same fact
- Agent-specific filenames inside `specs/`
- More than a handful of always-loaded imports without a strong reason
- `specs/index.md` that is just a dump of filenames with no routing logic
