# Reconcile Examples

## Good reconcile cases

- `AGENTS.md` never mentions `specs/architecture.md`, `specs/commands.md`, and
  `specs/environment.md` even though they exist
  - add a minimal routing block

- `AGENTS.md` repeats long environment setup that already lives in
  `specs/environment.md`
  - trim the entrypoint and leave a pointer

- docs still mention `scripts/bootstrap.sh` but the repo now uses
  `scripts/setup.sh`
  - mark stale guidance and repair the command

## Leave-alone cases

- the structure is slightly opinionated but coherent and easy to follow
- `AGENTS.md` is already short and routes cleanly into topic docs
- a second navigation layer already exists and works well

## Over-repair to avoid

- adding `specs/index.md` when three direct routes in `AGENTS.md` are enough
- inventing a `rules/` subsystem without a user request
- turning a small stale-command fix into a full doc rewrite
- merging unrelated topic docs just to reduce file count

## Escalate instead of guessing

- two plausible canonical homes both make sense
- the repo mixes `AGENT.md`, `AGENTS.md`, and spec-driven tooling in a custom,
  coherent way
- migration from Claude surfaces would touch multiple layers with unclear
  ownership
