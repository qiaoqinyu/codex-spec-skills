# codex-md-capture

Harness-aware guidance-layer skill for turning verified session learnings into
durable Codex docs.

## What It Does

- captures verified, durable, repo-relevant learnings from the current session
- routes each accepted learning to the narrowest stable home such as
  `AGENTS.md`, `specs/*.md`, or a skill reference
- rejects duplicate, low-confidence, or structurally ambiguous write-backs
- hands off guidance-structure problems to `codex-md-reconcile`

## What It Does Not Do

- broad doc audits or migrations
- session-state or lifecycle scaffolding such as `progress.md`,
  `session-handoff.md`, `init.sh`, or feature trackers
- full harness creation or runtime verification design

## Typical Outputs

- `no-op` with a concrete reason
- a destination map with evidence, stability, and dedup result
- a minimal patch proposal for an approved guidance update

## When To Trigger

- after a debugging or coding session revealed a durable new command or rule
- when a recurring gotcha should be promoted into `AGENTS.md` or `specs/*.md`
- when the user asks to summarize the session into stable Codex guidance

## Example Prompts

- "Turn this session into a minimal update for `specs/commands.md`."
- "Capture the durable learnings from this debugging run."
- "Write back the verified gotcha we just found, unless it already exists."

## Bundled References

- `references/capture-rubric.md`
- `references/destination-routing.md`
- `references/output-template.md`
- `references/examples.md`

## Evaluation Focus

The bundled evals focus on:

- verified write-back
- duplicate detection and `no-op`
- structural handoff to `codex-md-reconcile`
- rejection of low-confidence or non-durable learnings

## See Also

- `../codex-md-reconcile/README.md`
