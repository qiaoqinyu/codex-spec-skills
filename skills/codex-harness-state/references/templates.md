# State Templates

Use these templates as the smallest viable scaffold.

## Core Templates

- [templates/progress.md](templates/progress.md)
- [templates/session-handoff.md](templates/session-handoff.md)
- [templates/experiment-board.json](templates/experiment-board.json)

Use these for almost every repo that needs session continuity.

## Optional Deep-Track Template

- [templates/experiment-note.md](templates/experiment-note.md)

Use this only when a board row is too small to hold the important detail for a
track.

## Selection Rules

- one active track: `progress.md` plus `session-handoff.md`
- two or more active tracks: add `experiment-board.json`
- repeated restarts, comparisons, or long review cycles: add per-track notes
- if the real need is stable repo documentation, stop and use
  `$codex-md-capture` or `$codex-md-reconcile` instead
