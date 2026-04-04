# codex-harness-state

Harness state-layer skill for project-local progress, handoff, and experiment
tracking files.

## What It Does

- creates or refreshes a minimal `.agents/state/` layer inside a target repo
- separates mutable session state from stable Codex guidance docs
- keeps progress, next steps, blockers, and active experiment/workstream status
  visible across interruptions
- supports parallel experiment tracking without turning state files into a huge
  lab notebook

## What It Does Not Do

- write stable rules into `AGENTS.md` or `specs/*.md`
- reconcile Codex guidance routing or canonical ownership
- build a full automation platform, scheduler, or runtime harness
- replace proper experiment artifacts, logs, or results directories

## Default Outputs

- `.agents/state/progress.md`
- `.agents/state/session-handoff.md`
- `.agents/state/experiment-board.json`
- `.agents/state/experiments/*.md` only when needed

## When To Trigger

- multi-session coding or research work that keeps getting interrupted
- parallel experiments or workstreams that are easy to confuse
- long-running tasks where the next session needs a clean resume point
- repos that already have stable docs but still lack state continuity

## Example Prompts

- "Create a minimal state layer for this repo so future sessions can resume cleanly."
- "We have three active experiments. Set up progress, handoff, and an experiment board."
- "Refresh the existing handoff and experiment board from the current repo state."

## Bundled References

- `references/state-layout.md`
- `references/lifecycle-workflow.md`
- `references/templates.md`
- `references/examples.md`

## Evaluation Focus

The bundled evals focus on:

- choosing the smallest useful state scaffold
- separating mutable state from durable guidance
- handling parallel experiment tracking cleanly
- refusing to solve a docs problem with state files
