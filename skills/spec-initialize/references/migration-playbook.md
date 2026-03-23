# Migration Playbook

Use this guide when converting an existing instruction setup into a spec-first
agent harness.

This reference is primarily for migration from older Claude Code-style setups.
If you are starting fresh, you usually do not need this migration workflow:
just create thin agent adapters plus a minimal `specs/` layout.

In the terminology of this skill, this file is for migration work, not for
routine cleanup or session capture.

When creating or rewriting spec files during migration, rewrite them in English
unless there is a strong project-specific reason not to.

## Step 1: Inventory the Current Surfaces

Common sources to inspect:

- `AGENTS.md`
- `CLAUDE.md`
- `GEMINI.md`
- `.claude/rules/*.md`
- `.claude/skills/*`
- `docs/**/*.md`
- design notes, execution notes, and generated markdown

Create a simple inventory:

```text
source file -> purpose -> stability -> target location
```

## Step 2: Classify Each File

Use these buckets:

- Thin adapter:
  short, high-signal entrypoint guidance
- Shared spec:
  durable repo truth that multiple agents need
- Archive:
  volatile history, result logs, superseded decisions
- Mechanical enforcement:
  anything better expressed as code, tests, schemas, or CI

## Step 3: Draft the Target Tree

Start with the smallest useful tree. Example:

```text
AGENTS.md
CLAUDE.md
specs/
├── index.md
├── environment.md
├── commands.md
├── architecture.md
├── data-handling.md
└── experiment-archive.md
```

Do not move files before the target tree makes sense.

As you create the new target files, normalize them into concise English rather
than preserving mixed-language fragments from the old layout.

## Step 4: Migrate by Meaning, Not by Original Tool

Do not preserve the old tool taxonomy blindly.

Examples:

- `docs/**/*.md` may contain both nested topic docs and root-level archive
  files. Migrate by meaning, not by original folder depth.
- `docs/claude/environment.md` should become
  `specs/environment.md`, not `specs/claude-environment.md`.
- `.claude/rules/data-handling.md` should become
  `specs/data-handling.md` if it contains shared domain knowledge.
- A surviving path-scoped rule should remain only as a thin compatibility shim
  that points to the shared spec.
- Old Claude skills should be kept only if they still provide a real reusable
  recipe that is not just duplicated project knowledge.

## Step 5: Distill Stable Conclusions

Many old instruction sets mix stable guidance with volatile history.

Split them:

- Stable lessons and recurring gotchas:
  keep in normal specs
- Run-by-run metrics, timestamps, or temporary conclusions:
  move to clearly archival spec files such as `specs/experiment-archive.md`

Good pattern:

```text
specs/training.md
  - stable workflow
  - recurring gotchas
  - durable conclusions

specs/experiment-archive.md
  - raw results
  - one-off failures
  - obsolete variants
```

## Example Mapping from a Claude-Oriented Repo

Illustrative mapping based on a repo with:

- `CLAUDE.md`
- `docs/claude/*.md`
- `docs/*.md`
- `.claude/rules/*.md`
- `.claude/skills/*`
- `docs/experiment-results-archive.md`

Suggested migration:

```text
CLAUDE.md
  -> keep as thin Claude adapter pointing to specs/index.md

AGENTS.md
  -> add as thin generic adapter if Codex or other agents are used

docs/claude/environment.md
  -> specs/environment.md

docs/claude/commands.md
  -> specs/commands.md

docs/claude/experiment-notes.md
  -> specs/training.md

.claude/rules/development-guide.md
  -> specs/architecture.md
     plus a short scoped rule that links there if still useful

.claude/rules/data-handling.md
  -> specs/data-handling.md
     plus a short scoped rule that links there if still useful

.claude/skills/*
  -> keep only if they still encode a real reusable recipe rather than shared
     project truth

docs/experiment-results-archive.md
  -> specs/experiment-archive.md
```

The key move is not "rename docs to specs". The key move is to separate:

- shared truth
- agent-specific routing
- volatile history
- legacy Claude-specific shims that may or may not still be worth keeping

And to remember that `docs/` may already mix:

- nested operational docs such as `docs/claude/*.md`
- root-level archive or reference docs such as `docs/*.md`

And to ensure all agents can start from the same navigation file:

- `specs/index.md`

## Step 6: Leave Breadcrumbs

During migration:

- Update old root adapters to point to `specs/index.md`
- Remove or shrink obsolete files after the new structure is stable
- Avoid leaving two authoritative copies of the same guidance

If backward compatibility matters temporarily, make the old file a redirecting
stub rather than a second knowledge base.

## Step 7: Validate After Migration

Check:

- Every linked spec exists
- Commands still work
- Remaining Claude-specific shims are minimal and non-authoritative
- Agents can discover the right doc from the adapter without guessing
- The root adapter is materially shorter than the previous monolith
