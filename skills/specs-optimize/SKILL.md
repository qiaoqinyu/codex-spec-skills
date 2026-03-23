---
name: specs-optimize
description: >-
  Audit and improve an existing specs-first repository setup. Use when the repo
  already has `specs/` and the user wants to tighten routing, deduplicate
  content, repair stale or contradictory guidance, shrink adapters, separate
  archive material from normative specs, or otherwise improve the current
  setup. This is the default day-to-day skill for maintaining `specs/`.
---

# Specs Optimize

Audit and improve an existing specs-first repository setup with findings first
and edits second.

This is the default maintenance skill for repositories that already have
`specs/`.

## Goals

- tighten `specs/index.md` routing
- remove duplication
- repair stale or contradictory guidance
- keep adapters thin
- preserve implementation-critical detail
- reduce context bloat without deleting reusable contracts

## Use This Skill When

- the repo already has `specs/`
- the user wants to optimize, clean up, or tighten an existing setup
- adapters are too long or duplicate spec content
- routing is vague or stale
- archive material is mixed into normative specs

## Do Not Use This Skill When

- the repository does not have `specs/` yet
- the task is mainly a migration from legacy Claude-specific surfaces
- the task is only to write back conclusions from the current session

Use `spec-initialize` for bootstrap or migration.
Use `specs-capture` for session delta write-back.

## Workflow

### 1. Audit the Current State

Check:

- whether `specs/index.md` routes clearly
- whether important facts have one canonical home
- whether adapters point to `specs/index.md`
- whether archive material is mixed into normative specs
- whether commands, paths, and architecture notes still match the repo
- whether any files are bloated, vague, stale, or redundant

### 2. Report Findings Before Editing

Always separate:

- `Must Fix`: correctness, freshness, contradiction, broken routing
- `Should Improve`: signal-to-noise, compression, structure, readability

Always output findings before proposing changes. Do not jump straight into
rewrites.

Use this shape:

```md
## Specs Optimization Report

### Summary
- specs files: X
- adapters checked: X
- key risks: ...

### Must Fix
- [specific correctness or freshness issue]

### Should Improve
- [specific structural or signal-to-noise issue]

### Proposed Changes
1. [targeted change with rationale]
```

If there are no `Must Fix` items, say so explicitly.

### 3. Propose Targeted Improvements

Prefer:

- tightening sections
- merging duplicate guidance
- moving raw history to archive files
- shrinking adapters
- clarifying `specs/index.md` task routing

Avoid:

- full rewrites without need
- aggressive file splitting
- replacing exact contracts with generic prose

### 4. Apply Minimal Changes

Make the smallest set of edits that resolves the real findings.

### 5. Validate

Verify:

- routes are clearer than before
- no canonical facts were lost
- commands and paths still resolve
- archive and normative material are separated
- adapter text remains thin and accurate

## Output Shape

1. Audit summary
2. `Must Fix`
3. `Should Improve`
4. Proposed or applied edits
5. Validation summary

Findings must come before edits.
