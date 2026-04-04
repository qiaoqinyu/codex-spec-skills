# Reconcile Workflow

Use this five-stage workflow on every run.

## 1. Discover

Build a guidance map of what actually exists.

Collect:

- entrypoint files such as `AGENTS.md` or `AGENT.md`
- topic docs under `specs/`
- skill-specific references that may own reusable workflow detail
- legacy Claude surfaces only when migration was explicitly requested

Output:

- layout shape
- entrypoint files
- primary router
- secondary routers
- specs files
- missing files that docs still reference
- obvious duplicates or overlaps

## 2. Reality-check

Verify the docs against repository truth.

Check:

- commands in manifests, scripts, or CI config
- current paths and directory layout
- primary and secondary router targets
- environment setup from config files
- risky operations or approval boundaries
- dirty-worktree context when it matters

If docs conflict with repo reality, mark the docs stale.

## 3. Score

Use [quality-criteria.md](quality-criteria.md).

Classify each finding as:

- `must fix`
- `should improve`
- `leave alone`

Always report findings before edits.

## 4. Propose

Default to the smallest useful repair.

Report shape:

```md
## Codex Guidance Report

### Guidance Map
- layout shape: ...
- entrypoints: ...
- primary router: ...
- secondary routers: ...
- topic docs: ...
- key overlaps: ...

### Proof Of Work
- files inspected: ...
- routers verified: ...
- commands used: ...
- open ambiguities: ...

### Must Fix
- ...

### Should Improve
- ...

### Leave Alone
- ...

### Canonical Homes
- `<fact>` -> `<file>`

### Proposed Changes
1. ...
```

Every proposal must include:

- target file
- why that file owns the fact
- exact diff or replacement block
- change budget note if the change is larger than a small patch
- why migration is worth the churn when you are changing a coherent existing
  layout

## 5. Verify

After approval and apply, verify:

- paths still exist
- commands are still grounded in repo reality
- duplicates were actually reduced
- `AGENTS.md` remained short and routing-focused
- secondary routers still point cleanly to their owned scope
- no unneeded layer such as `specs/index.md` or `rules/` was introduced
