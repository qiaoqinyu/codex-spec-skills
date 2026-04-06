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
- move to `done` only when the intended question is answered and the final
  `outcome` is recorded
- use `blocked` instead of pretending progress is still active
- use `archived` for abandoned or superseded tracks rather than deleting them

## Decision Outcomes

Track status and run outcome are separate.

- `keep`: current evidence supports keeping the track or its latest result
- `discard`: the latest hypothesis or result should not be carried forward
- `no-op`: nothing new is worth carrying forward, but the state was checked
- `handoff`: the next step belongs in durable guidance capture or doc
  reconciliation rather than more state-only updates

## Required Fields Per Active Track

Every active board row should capture:

- `id`
- `goal`
- `status`
- `baseline`
- `changed_variables`
- `invariants`
- `artifact_paths`
- `evidence`
- `certainty`
- `outcome`
- `untouched_scope`
- `next_action`
- `updated_at`

If any field is unknown, say so explicitly.
