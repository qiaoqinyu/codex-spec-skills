# `specs/` Taxonomy

Use `specs/` as the repository-local knowledge base shared across agents.

Do not treat this taxonomy as a mandatory checklist. Pick the smallest shape
that matches the repo.

## Core Principles

- `specs/` is the shared system of record for stable repository knowledge.
- Agent entrypoints are adapters into `specs/`, not parallel knowledge bases.
- `specs/index.md` is the single navigation hub across agents.
- `specs/index.md` should behave like a context router, not a narrative manual.
- Prefer dense, durable documents over large numbers of tiny files.
- Default to a single `specs/` folder with files split by subject.
- Write spec files in English by default to maximize compatibility with coding
  agents' reasoning and retrieval behavior.
- Do not create subdirectories unless the flat layout has already become hard
  to navigate.

## Default Layout

Use this as a common starting shape, not a required target:

```text
specs/
├── index.md
├── commands.md
├── environment.md
├── architecture.md
├── project.md
└── ...
```

Many repos can start with only one or two of these. A slightly fuller setup is:

- `index.md`
- `commands.md`
- `environment.md`
- `architecture.md`

Add more topic files only when they are justified by the actual project.

## What Each File Usually Holds

### `specs/index.md`

Use this as the top-level table of contents.

Include:

- What each spec file is for
- Which tasks should read which file first
- Which files are normative versus archival
- Relative paths to each spec file

Prefer a routing structure such as:

```md
# Specs Index

## Read First

- For running, testing, and verification: `./commands.md`
- For environment, paths, and toolchain: `./environment.md`
- For code structure and boundaries: `./architecture.md`

## Project-Specific Topics

- For model training and experiments: `./training.md`
- For dataset and preprocessing rules: `./data-handling.md`
- For frontend work: `./frontend.md`
- For LLM or agent workflows: `./llm-agents.md`

## Archive

- Historical experiment logs: `./experiment-archive.md`
```

Prefer entries like:

- `./commands.md`
- `./environment.md`
- `./training.md`

This makes the index easier to reuse across different coding CLIs and keeps
path interpretation unambiguous for LLMs.

Write the index itself in concise English as well.

### `specs/project.md`

Put stable high-level context here:

- Goals
- Domain vocabulary
- Project scope
- Important business or research framing

### `specs/architecture.md`

Put codebase structure and dependency rules here:

- Major modules
- Dependency boundaries
- Key abstractions
- Important invariants

### `specs/environment.md`

Put environment setup here:

- Toolchain
- Runtime versions
- Env activation
- External system locations

### `specs/commands.md`

Put operational commands here:

- Build
- Test
- Lint
- Run
- Release

Keep commands copy-pasteable and current.

Write commands and surrounding notes in concise English.

### `specs/workflows.md`

Put recurring execution flows here:

- Common implementation flow
- Release flow
- Data processing flow
- Review or validation flow

### `specs/conventions.md`

Put repo-specific conventions here:

- Naming rules
- File placement rules
- Style guidance that is not already enforced elsewhere

### Domain-Specific Files

Create flat, topic-named files for domain knowledge:

- `specs/data-handling.md`
- `specs/frontend.md`
- `specs/training.md`
- `specs/integrations.md`
- `specs/llm-agents.md`

Prefer topic files over category subdirectories.

For your common project types, the usual optional additions are:

- Deep learning:
  `training.md`, `data-handling.md`, `experiment-archive.md`
- LLM / agents:
  `llm-agents.md`, `evals.md`, `integrations.md`
- Frontend:
  `frontend.md`

### Archive Files

If historical material is still worth keeping near the harness, use flat file
names such as:

- `specs/experiment-archive.md`
- `specs/migration-history.md`
- `specs/decision-log.md`

Keep stable conclusions in normal specs and raw history in clearly archival
files.

As a rule:

- experiment results
- debugging outcomes
- metric snapshots
- run summaries

belong in archival spec files, not in normative specs such as `training.md` or
`architecture.md`.

Even archival spec files should default to English so future agents can reason
over them consistently.

## Naming Rules

- Prefer lowercase kebab-case file names.
- Prefer meaningful subject names over agent-specific names.
- Avoid `claude-*.md`, `codex-*.md`, or `agent-*.md` inside `specs/` unless the
  content is genuinely agent-specific.
- Name files by subject, not by the tool that first created them.

## When Not To Create a New Spec

Do not create a new file when:

- The content can fit cleanly into an existing spec.
- The material is one-off debugging chatter.
- The rule should instead live in code, tests, or CI.
- The information is temporary and not useful enough to keep as a lasting spec.
- The content is really a recipe and belongs in a skill instead.

## When To Add Subdirectories

Only add subdirectories if all of these are true:

- The flat `specs/` folder has become crowded.
- Related files are clearly forming a stable cluster.
- The split will reduce navigation cost instead of increasing it.

If in doubt, keep the flat layout.

## Recommended Reading Order

When building or refactoring a harness:

1. Root adapter file
2. `specs/index.md`
3. `specs/commands.md` or equivalent
4. Relevant topic spec
5. Relevant archival spec if needed
