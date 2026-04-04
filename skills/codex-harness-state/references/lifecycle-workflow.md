# Lifecycle Workflow

Use a small, explicit lifecycle vocabulary so the state layer stays comparable
across sessions.

## Allowed Status Values

- `proposed`
- `ready`
- `running`
- `blocked`
- `review`
- `done`
- `archived`

## Meaning

- `proposed`: idea exists, but the track is not ready to run
- `ready`: inputs and commands are known; safe to start
- `running`: work or execution is in progress
- `blocked`: a concrete blocker prevents progress
- `review`: outputs exist and need interpretation or validation
- `done`: the goal of this track is complete
- `archived`: the track is intentionally closed but kept for reference

## Transition Rules

- move to `ready` only after the required command, config, or entrypoint is
  known
- move to `running` only after a real launch or implementation start
- move to `review` only when outputs or code changes exist to inspect
- move to `done` only when the intended question is answered or the task is
  complete
- use `blocked` instead of pretending progress is still active
- use `archived` for abandoned or superseded tracks rather than deleting them

## Required Fields Per Active Track

Every active board row should capture:

- `id`
- `goal`
- `status`
- `baseline`
- `changed_variables`
- `invariants`
- `artifact_paths`
- `next_action`
- `updated_at`

If any field is unknown, say so explicitly.
