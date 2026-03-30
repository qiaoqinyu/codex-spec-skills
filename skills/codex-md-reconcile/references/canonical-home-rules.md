# Canonical Home Rules

Use these rules before moving or creating guidance.

## Ownership Order

### `AGENTS.md`

Owns:

- repo-wide instructions
- approval boundaries
- exact validation commands that matter broadly
- routing to deeper topic docs

Should not own:

- large topic background
- long examples
- repeated detail already maintained in `specs/*.md`

### `specs/<topic>.md`

Owns:

- topic-specific workflows
- recurring gotchas for one domain
- architecture, environment, data, review, or deployment detail
- stable examples that help on that topic

### skill references

Own only:

- reusable workflow guidance for the skill itself
- templates or checklists that are not repository truth

### personal global docs

Own only:

- user-local defaults that should not be committed

## Tie-Break Rules

- if a fact matters on nearly every task, keep the short form in `AGENTS.md`
- if a fact only matters inside one recurring domain, move it to
  `specs/<topic>.md`
- if a fact is about how a skill operates rather than how the repo works, move
  it to skill references
- if two files both contain the same rule, choose one canonical home and trim
  the other to a pointer

## Stop Conditions

Stop and escalate before editing when:

- canonical ownership is genuinely ambiguous
- the repository already uses a non-standard but coherent doc layout
- migration would require changing multiple layers at once
- fixing the issue would introduce a new navigation layer with unclear payoff
