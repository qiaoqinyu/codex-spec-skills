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

## Automatic Rejections

Reject the candidate and return `no-op` or `rejected learning` when it is:

- raw debugging chatter
- a low-confidence hypothesis
- an unverified workaround
- a one-off command output with no future value
- temporary branch state or dirty-worktree trivia
- a long narrative summary with no stable rule or command inside it

## Confidence Bands

- high: verified directly against repo reality or successful execution
- medium: supported by strong evidence, but not fully exercised end-to-end
- low: incomplete evidence; do not write back

Only `high` and selective `medium` items should survive to a proposal.
