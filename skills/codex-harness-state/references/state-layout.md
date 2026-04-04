# State Layout

Use this skill to create a small mutable layer inside the target repository.

Default layout:

```text
.agents/
  state/
    progress.md
    session-handoff.md
    experiment-board.json
    experiments/
      exp28a.md
      exp28b.md
```

## File Roles

- `progress.md`: current objective, active tracks, recent verified changes,
  blockers, and near-term checkpoints
- `session-handoff.md`: next-session resume note with exact starting point,
  commands, files, and unresolved questions
- `experiment-board.json`: machine-friendly summary of active tracks and their
  lifecycle status
- `experiments/*.md`: optional deep notes for individual tracks when one-line
  board entries stop being enough

## Placement Rules

- prefer `.agents/state/` at the repo root
- keep these files out of `specs/` because they are mutable state, not stable
  guidance truth
- do not store them under `~/.codex/skills/`; skills define workflows, they do
  not hold project runtime state
- if the repository already has a coherent alternative state path, adapt to it
  instead of forcing a move

## Compression Rules

- start with `progress.md` plus `session-handoff.md`
- add `experiment-board.json` when there are multiple active tracks or a high
  risk of confusion
- add per-track note files only when the board is no longer enough
