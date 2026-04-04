# Capture Output Template

Use this structure for every run.

## Session learnings worth keeping

- `<learning>` — `<short reason it passed the gate>`

## Rejected learnings

- `<candidate>` — `<why rejected or why this is a no-op>`

## Destination map

### Learning: `<short label>`
- evidence: `<command, path, file, or observed repo fact>`
- stability: `<session fact | recurring pattern | policy-level signal>`
- destination: `<AGENTS.md | specs/<topic>.md | skill reference | ~/.codex/AGENTS.md | handoff to $codex-md-reconcile>`
- why-not-elsewhere: `<why the next-most-likely home is wrong>`
- dedup-check: `<not found | equivalent rule already exists | unclear>`
- existing-rule-checked-at: `<path + line, command, or search result>`
- promotion-decision: `<write-back now | no-op | handoff to $codex-md-reconcile>`
- validation: `<how this was or will be checked>`
- confidence: `<high | medium>`

## Proposed changes

### Update: `<file path>`
**Why:** `<one-line reason>`
**Layer:** `<AGENTS.md | specs | skill reference | personal global>`

Diff:

    + <minimal addition>

## Validation notes

- `<path exists / command verified / duplicate avoided / no-op>`

## No-op result

If nothing passes the gate, return:

- `No durable learning passed the write-back gate.`
- `No files should change.`

If a duplicate or equivalent rule already exists, return:

- `An equivalent rule already exists in the canonical destination.`
- `No files should change.`
