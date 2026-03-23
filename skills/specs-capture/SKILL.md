---
name: specs-capture
description: >-
  Capture durable learnings from the current session into the canonical files
  under `specs/`. Use when the repository already has `specs/` and the user
  wants to write back conclusions, decisions, command corrections, architecture
  discoveries, reusable constraints, or other durable project truth that
  emerged in this conversation. This skill is incremental only and should not
  perform broad repository cleanup or structural redesign.
---

# Specs Capture

Write durable session outcomes back into the existing `specs/` knowledge base.

This skill is for incremental session delta capture, not repository-wide
cleanup or harness redesign.

## Use This Skill When

- the current session produced durable conclusions
- an existing spec should be updated with corrected or clarified truth
- a small new sibling spec is justified by this session
- `specs/index.md` needs a small routing update because of this session

## Do Not Use This Skill When

- the repository needs a broad specs audit
- the existing structure is stale or contradictory across many files
- the repository has no `specs/` yet
- the task is large-scale migration or adapter redesign

Use `specs-optimize` for repository-wide cleanup.
Use `spec-initialize` for bootstrap or migration.

## What To Capture

Capture only durable, high-signal outcomes from the current session:

- confirmed project decisions
- command or environment corrections
- architecture discoveries
- implementation constraints
- reusable contracts such as counts, shapes, schemas, and path rules
- recurring failure signatures and their fixes
- clarified routing in `specs/index.md`

If the session mainly produced experiment results, debugging outcomes, metric
snapshots, or run summaries, capture them in an archival spec instead of
mixing them into normative specs.

Do not capture:

- temporary debugging chatter
- uncertain hypotheses
- raw chain-of-thought
- one-off trial output unless it became a durable lesson

## Workflow

### 1. Identify Durable Session Outcomes

Capture only what would help a future agent.

### 2. Find the Canonical Home

Prefer updating an existing spec over creating a new one.

### 3. Write a Minimal Increment

Keep the change narrow, durable, and high-signal.

### 4. Update `specs/index.md` Only If Routing Changed

Do not churn the index without need.

### 5. Touch Adapters Only If Strictly Necessary

Only patch adapter routing if it is clearly broken or missing.

## Output Shape

1. What this session clarified
2. Which file was updated
3. Whether `specs/index.md` changed
4. Whether any minimal adapter sync was needed
