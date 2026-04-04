# codex-md-reconcile

Harness-aware guidance-layer skill for reconciling `AGENTS.md`, `specs/*.md`,
and related Codex guidance surfaces.

## What It Does

- audits the real guidance surface before proposing repairs
- verifies docs against repository reality
- classifies findings into `must fix`, `should improve`, or `leave alone`
- proposes the smallest repair that improves routing, ownership, and structure

## What It Does Not Do

- write back one session's learnings when a narrow factual update is enough
- build session-state or lifecycle scaffolding such as `progress.md`,
  `session-handoff.md`, `init.sh`, or feature trackers
- act as a full harness builder or runtime-state owner

## Typical Outputs

- a guidance map with primary and secondary routers
- proof of work with files inspected and commands used
- minimal repair proposals with canonical ownership rationale
- explicit `leave alone` or out-of-scope decisions when appropriate

## When To Trigger

- `AGENTS.md` and `specs/*.md` are stale, duplicated, or poorly routed
- a repository has Codex guidance but key navigation is missing
- Claude-oriented guidance needs explicit Codex migration
- the user asks for a guidance audit, cleanup, or bootstrap

## Example Prompts

- "Reconcile AGENTS.md with the existing specs files."
- "Audit the Codex guidance surface and tell me what is stale."
- "Bootstrap the minimum missing routing into specs without a big rewrite."

## Bundled References

- `references/reconcile-workflow.md`
- `references/quality-criteria.md`
- `references/canonical-home-rules.md`
- `references/verification-checklist.md`
- `references/examples.md`
- `references/templates.md`

## Evaluation Focus

The bundled evals focus on:

- stale router repair
- coherent alternative router leave-alone decisions
- minimal bootstrap into existing docs
- explicit boundary handling when the real problem is lifecycle or state

## See Also

- `../codex-md-capture/README.md`
