# Organization Patterns

Use these patterns to decide where guidance belongs in a Codex-oriented repo.

## Routing Decision Tree

```text
This guidance...
|
+-- Needed on nearly every task?
|   |
|   +-- YES --> Put the short version in AGENTS.md
|   |            Keep it concise and executable
|   |
|   +-- NO
|       |
|       +-- Is it tied to one recurring topic?
|       |   |
|       |   +-- YES --> Put it in specs/<topic>.md
|       |   |
|       |   +-- NO
|       |       |
|       |       +-- Is it a reusable workflow?
|       |       |   |
|       |       |   +-- YES --> Put it in a skill
|       |       |   |
|       |       |   +-- NO --> Keep it in normal docs or archive material
```

## Default Codex Shape

Prefer the smallest useful shape:

```text
AGENTS.md
specs/
  architecture.md
  commands.md
  environment.md
```

Add more files only when the topic is genuinely recurring.

## When To Add `specs/index.md`

Do not add `specs/index.md` by default.

Add it only when:

- `AGENTS.md` is getting too route-heavy
- `specs/` contains enough topic files that a second navigation layer helps
- the repository has multiple parallel domains and direct routing in
  `AGENTS.md` has become noisy

If a repository already has a good `specs/index.md`, keep it and route through
it. Treat that as compatibility with an existing shape, not the default target.

## When To Avoid `rules/`

Avoid a standalone `rules/` layer when:

- the repository can express the guidance cleanly inside topic docs
- the distinction between rules and background would create duplication
- the user wants less interpretation burden on the agent

If the user explicitly wants `rules/`, make it a documented project convention,
not a claimed Codex builtin.

## When To Add `experiment-journal.md`

Add `specs/experiment-journal.md` when:

- the project runs many experiments with changing configs or protocols
- raw outputs live in `results/` or external result directories
- conclusions need a readable bridge between artifacts and durable specs

Do not use the journal as the canonical home for stable project truth. Promote
reusable conclusions into topic docs such as `training.md` or
`data-handling.md`.

## Missing `AGENTS.md` Routing Is A Must-Fix

If `specs/*.md` exists but `AGENTS.md` does not mention it, add a minimal
navigation block.

Default pattern:

```text
Read specs/architecture.md for structure.
Read specs/commands.md for runnable commands.
Read the relevant topic file under specs/ before substantive work.
```

## Migration Patterns

### Pattern 1: `CLAUDE.md` -> `AGENTS.md`

- keep durable guidance
- remove Claude-specific wording
- keep the entrypoint short

### Pattern 2: `@import` -> explicit routing

Before:

```text
CLAUDE.md -> @docs/claude/data.md
```

After:

```text
AGENTS.md
  - Read specs/data.md when working on data or evaluation
```

### Pattern 3: `.claude/rules/*.md` -> `specs/<topic>.md`

Before:

```text
.claude/rules/data.md
```

After:

```text
specs/data.md
```

Keep background and rules in separate sections inside the same file if needed.
