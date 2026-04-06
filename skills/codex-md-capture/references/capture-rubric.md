# Capture Write-Back Gate

Use this gate before proposing any persistent write-back.

Every candidate learning must pass all four checks:

1. Verified
- grounded in repository reality, a successful command, a confirmed path, or an
  explicit user-approved rule
- not a guess, vibe, or half-tested theory

2. Repeated or likely to recur
- already mattered more than once in the session, or
- would predictably matter again for future agents in the same repository

3. Durable
- still useful after this session ends
- not tied to one temporary log, one failing run, or one transient branch state

4. Repo-relevant
- specific to the repository, workflow, environment, or reusable skill
- not generic engineering advice

## Promotion Prerequisites

If the candidate comes from `.agents/state/*`, an experiment board, or a
track note, it should also preserve the source contract:

- baseline
- changed variables
- invariants
- artifact paths
- evidence
- current outcome

If those fields are missing, do not silently upgrade the candidate into durable
guidance. Return `discard`, `no-op`, or `handoff`.

## Stability Horizon

Classify every candidate that passes the gate:

- `session fact`: useful to record now, but not yet strong enough to imply a
  repo-wide or long-lived rule on its own
- `recurring pattern`: repeated enough that future agents would likely benefit
  from seeing it in guidance
- `policy-level signal`: stable enough to justify a durable rule, boundary, or
  canonical routing fact

Bias toward `session fact` unless the stronger label is supported by evidence.

## Automatic Rejections

Reject the candidate and return `no-op` or `rejected learning` when it is:

- raw debugging chatter
- a low-confidence hypothesis
- an unverified workaround
- a one-off command output with no future value
- temporary branch state or dirty-worktree trivia
- a long narrative summary with no stable rule or command inside it

## Blocking Conditions

Do not write back the candidate when:

0. Source contract is too weak
- the candidate points at a run, track, or experiment, but no baseline,
  artifact path, or direct evidence survives
- do not paraphrase this into a durable rule
- hand off to `$codex-harness-state` if the state layer itself is too weak

1. Duplicate or equivalent rule already exists
- check the likely destination first
- if the same rule already exists with equivalent meaning, return `no-op`
- prefer pointing to the existing rule over restating it

2. Structural signal, not a write-back
- the candidate mainly reveals missing routing, ambiguous canonical ownership,
  or a stale guidance layout
- do not force this into a factual write-back
- hand off to `$codex-md-reconcile`

## Decision Outcomes

- `keep`: propose the minimal durable write-back
- `discard`: reject the candidate because the gate failed
- `no-op`: nothing new is needed because the rule already exists or nothing
  survived
- `handoff`: the real problem belongs to `codex-harness-state` or
  `codex-md-reconcile`

## Confidence Bands

- high: verified directly against repo reality or successful execution
- medium: supported by strong evidence, but not fully exercised end-to-end
- low: incomplete evidence; do not write back

Only `high` and selective `medium` items should survive to a proposal.
