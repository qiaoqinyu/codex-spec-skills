# Codex Guidance Templates

Use these as starting points. Fill them only with verified facts from the
current repository.

## Core Templates

- [templates/agents-minimal.md](templates/agents-minimal.md)
- [templates/specs-architecture.md](templates/specs-architecture.md)
- [templates/specs-commands.md](templates/specs-commands.md)
- [templates/specs-environment.md](templates/specs-environment.md)
- [templates/specs-review.md](templates/specs-review.md)

Use these for almost any code repository that wants `AGENTS.md + specs/*.md`.

## Deep Learning Research Templates

- [templates/dl-training.md](templates/dl-training.md)
- [templates/dl-data-handling.md](templates/dl-data-handling.md)

Use these when the repository is experiment-heavy and has training, evaluation,
sampling, or preprocessing semantics that deserve stable docs.

## AI for Science / Materials Templates

- [templates/science-split-policy.md](templates/science-split-policy.md)
- [templates/science-provenance-and-workflow.md](templates/science-provenance-and-workflow.md)
- [templates/science-artifact-manifest.md](templates/science-artifact-manifest.md)
- [templates/science-representation-and-conventions.md](templates/science-representation-and-conventions.md)
- [templates/science-experiment-journal.md](templates/science-experiment-journal.md)

Use these when experiment validity depends heavily on split semantics, data
lineage, artifact completeness, or scientific representation choices.

## Selection Rules

- Start with the core templates.
- Add the deep-learning templates only if the repo trains or evaluates models.
- Add the science templates only if the project has meaningful protocol,
  provenance, or representation risk beyond ordinary ML repos.
- Do not create `specs/index.md` by default.
- If `specs/*.md` exists, make sure `AGENTS.md` routes into it.
- Keep stable conclusions in topic docs; keep per-run history in
  `experiment-journal.md`.

## Compression Checklist

When condensing a bloated setup, keep only:

- the true entrypoint
- exact commands
- concrete boundaries
- routing to topic docs
- durable recurring constraints
