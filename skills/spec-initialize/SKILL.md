---
name: spec-initialize
description: >-
  Initialize a new specs-first repository setup, migrate legacy instruction
  surfaces into `specs/`, or rebuild the repository navigation structure when
  the current harness is fundamentally wrong. Use when the repo has no
  `specs/` yet, when migrating from `CLAUDE.md`, `.claude/rules`, or similar
  legacy instruction systems, or when the adapter -> knowledge base ->
  enforcement topology needs to be redesigned. This is a low-frequency setup
  skill, not the default tool for routine specs cleanup or session capture.
---

# Spec Initialize

Create or re-found a repository-local specs setup when the repository does not
already have a clean, usable shared knowledge base.

This skill is for bootstrap, migration, or structural reset. It is not the
default choice for routine optimization or session delta capture.

## Core Model

Treat the harness as three layers:

```text
Agent adapters
  AGENTS.md / CLAUDE.md / GEMINI.md / local prompts
      ->
Shared knowledge base
  specs/index.md -> focused spec files
      ->
Mechanical enforcement
  code / tests / linters / CI / scripts
```

Rules:

- Keep agent entrypoints thin. They are maps, not encyclopedias.
- Keep shared project truth in one canonical home.
- Introduce `specs/` only when it clearly improves routing and reuse.
- Move mechanically enforceable constraints into code, tests, linters, or CI.
- Keep stable guidance separate from volatile logs and run history.
- Default to a small flat `specs/` layout rather than a large taxonomy.
- Sync root adapters after initialization unless the user explicitly asks for
  specs-only output.

## Use This Skill When

- the repository does not have `specs/`
- the current repo is migrating from `CLAUDE.md`, `.claude/rules`, or similar
  legacy instruction surfaces
- the existing adapter and documentation topology is fundamentally confusing
- the user wants to establish a new shared source of truth for multiple agents

## Do Not Use This Skill When

- the repo already has usable `specs/` and only needs cleanup
- the task is to write back learnings from the current session
- the task is routine deduplication, routing cleanup, or stale-doc repair

Use `specs-optimize` for improving an existing setup.
Use `specs-capture` for incremental session write-back.

## Workflow

### 1. Discover Current Knowledge Surfaces

Inventory the current repository guidance before proposing a new shape:

```bash
find . -name "AGENTS.md" -o -name "CLAUDE.md" -o -name "GEMINI.md" 2>/dev/null
find . -path "*/docs/*" -o -path "*/specs/*" 2>/dev/null
find . -path "*/.claude/rules/*.md" -o -path "*/.claude/skills/*" 2>/dev/null
```

Check:

- root and nested agent entrypoints
- durable docs that already act as shared knowledge
- commands, environment docs, architecture docs, and workflow docs
- whether current docs already route well enough without `specs/`
- which constraints are documentation-only versus mechanically enforced

### 2. Decide Whether `specs/` Is Actually Needed

Before introducing `specs/`, check whether the repository can stay clean with
existing docs plus thin adapters.

Prefer introducing `specs/` only when it clearly improves:

- discoverability
- single source of truth
- progressive disclosure
- multi-agent compatibility
- separation of stable guidance from volatile history

Do not introduce `specs/` just because it is a familiar pattern.

### 3. Design the Minimal Target Shape

Default to the smallest useful setup.

Typical target:

```text
AGENTS.md / CLAUDE.md
  -> specs/index.md
      -> a few sibling specs
```

Design rules:

- start with `specs/index.md`
- add only the minimum useful sibling specs
- prefer flat files over subdirectories
- preserve exact contracts, counts, paths, and failure signatures when needed
- keep archives clearly separate from normative specs

Read these references as needed:

- [references/specs-taxonomy.md](references/specs-taxonomy.md)
- [references/navigation-templates.md](references/navigation-templates.md)
- [references/migration-playbook.md](references/migration-playbook.md)

### 4. Migrate or Generate

- create `specs/index.md`
- create only the minimum useful sibling specs
- move stable shared truth into `specs/`
- keep volatile history in clearly archival files
- reduce legacy shims to minimal compatibility routers when still needed

### 5. Sync Adapters

If `AGENTS.md` or `CLAUDE.md` exists, make it a thin router into `specs/`.

For Codex-oriented repos, `AGENTS.md` should explicitly tell the agent to read
`specs/index.md` before substantive work.

### 6. Validate

Use [references/harness-quality.md](references/harness-quality.md).

At minimum verify:

- a new agent can find the right file quickly
- shared truth has one canonical home
- adapters are thin
- commands and paths still match reality
- volatile history is separated from normative guidance
- remaining legacy shims do not duplicate the new canonical specs

## Output Shape

1. Current-state summary
2. Why `specs/` is needed or justified
3. Proposed target tree
4. New or migrated canonical files
5. Adapter sync proposal or applied diff
6. Validation summary

## Non-Goals

- Do not treat `specs/` as mandatory for every repository.
- Do not use this skill for routine dedupe or stale-doc cleanup.
- Do not preserve legacy structure just because it already exists.
- Do not create a large taxonomy when one small setup is enough.
- Do not mix normative specs with raw experiment history.
