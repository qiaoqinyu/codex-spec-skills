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

## Reject and return no-op

- a single failed attempt with no confirmed fix
- raw stack traces copied from one run
- a maybe-correct explanation that was never validated
- generic advice like "write clear code"
- temporary branch notes that will age out immediately

## Borderline cases

- medium-confidence learning with strong evidence but no final end-to-end run
  - only keep if future agents would still clearly benefit
  - include explicit validation notes

- session revealed missing routing between `AGENTS.md` and `specs/*.md`
  - do not patch structure here
  - hand off to `$codex-md-reconcile`
