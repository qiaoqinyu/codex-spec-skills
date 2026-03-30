# Capture Output Template

Use this structure for every run.

## Session learnings worth keeping

- `<learning>` — `<short reason it passed the gate>`

## Rejected learnings

- `<candidate>` — `<why rejected or why this is a no-op>`

## Destination map

### Learning: `<short label>`
- evidence: `<command, path, file, or observed repo fact>`
- destination: `<AGENTS.md | specs/<topic>.md | skill reference | ~/.codex/AGENTS.md>`
- why-not-elsewhere: `<why the next-most-likely home is wrong>`
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
