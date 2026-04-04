# Capture Examples

## Good captures

- `pytest tests/test_cli.py -q` now required after CLI edits
  - verified command
  - likely to recur
  - repo-specific
  - belongs in `AGENTS.md` or `specs/review.md`

- `specs/environment.md` is the canonical home for Conda activation and CUDA
  checks
  - durable routing fact
  - avoids repeating environment detail in `AGENTS.md`

- `scripts/bootstrap.sh` is the real setup entrypoint, not the old README
  command
  - verified against repo reality
  - worth writing back as a corrected command

- the same validation command surfaced in multiple sessions and is still absent
  from repo guidance
  - stability is now closer to `recurring pattern`
  - worth proposing as durable guidance rather than leaving it as session-only
    trivia

## Reject and return no-op

- a single failed attempt with no confirmed fix
- raw stack traces copied from one run
- a maybe-correct explanation that was never validated
- generic advice like "write clear code"
- temporary branch notes that will age out immediately
- the target file already contains an equivalent rule with different wording
  - cite the existing rule
  - return `no-op` instead of duplicating it

## Borderline cases

- medium-confidence learning with strong evidence but no final end-to-end run
  - only keep if future agents would still clearly benefit
  - include explicit validation notes

- session revealed missing routing between `AGENTS.md` and `specs/*.md`
  - do not patch structure here
  - hand off to `$codex-md-reconcile`

- session revealed that the real problem is split ownership between two files
  - do not guess a winner inside `codex-md-capture`
  - classify this as a structure signal and hand off to
    `$codex-md-reconcile`
