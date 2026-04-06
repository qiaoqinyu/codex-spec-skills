# Codex Guidance Quality Criteria

Use this rubric when auditing `AGENTS.md` and adjacent `specs/*.md`.

## Scoring Rubric

Total score: 100

1. Entry-point quality (20)
- `AGENTS.md` is short, accurate, and routing-focused.
- if the repo uses a router stack, the role of each router is explicit.
- The file contains durable rules rather than large topic dumps.
- High-priority commands and boundaries are easy to find.
- If `specs/*.md` exists, `AGENTS.md` tells Codex where to start.

2. Routing clarity (20)
- It is obvious which markdown file to read for which task.
- Topic files have distinct ownership.
- secondary routers such as `WORKSPACE.md` or subtree `INDEX.md` have a clear,
  non-overlapping role when they exist.
- The current structure avoids unnecessary extra layers.
- `specs/index.md` is not added unless it solves a real routing problem.

3. Repository reality (15)
- Commands, paths, and tool names match the actual repo.
- Guidance does not depend on removed files or dead workflows.
- coherent alternative layouts are not misclassified as stale just because they
  differ from the default shape.
- Migration notes do not misstate Codex capabilities.
- Experiment logs point to real artifact locations when they claim to.

4. Conciseness and progressive disclosure (15)
- `AGENTS.md` stays dense and skimmable.
- Longer detail lives in topic docs rather than the entrypoint.
- The structure avoids forcing large amounts of context up front.

5. Actionability and boundaries (15)
- The docs tell the agent what to do, what to ask first, and what not to touch.
- Validation steps are concrete.
- Dangerous operations are gated clearly.
- Temporary state versus durable guidance is explicit.

6. Duplication and contradiction control (15)
- Each important fact has a clear canonical home.
- Topic docs do not fight each other.
- multiple routers can coexist only when their scopes are clearly separated.
- Background and rules are separated clearly enough to avoid drift.
- Stable conclusions are promoted out of experiment journals into topic docs.
- Promotion boundaries do not blur state, capture, and reconcile ownership.

## Grade Bands

- A: 90-100
- B: 75-89
- C: 60-74
- D: 40-59
- F: 0-39

## High-Signal Best Practices

- Keep `AGENTS.md` short and practical.
- Put topic detail in `specs/*.md`.
- allow coherent router stacks such as `AGENTS.md` plus `WORKSPACE.md` or
  subtree `INDEX.md` when they genuinely reduce search cost.
- Prefer one topic file per recurring domain.
- Introduce extra routing layers only when they solve a real problem.
- Add minimal `AGENTS.md` routing whenever deeper docs exist.
- Keep the route from mutable state to durable guidance explicit and small.
- When migrating from Claude, replace implicit loading claims with explicit
  routing language.

## Common Failure Modes

- `AGENTS.md` tries to be both router and encyclopedia
- `specs/*.md` has unclear topic ownership
- a coherent alternative router stack gets flattened just to match a preferred
  style
- the same rule appears in multiple files with different wording
- a fake `rules` subsystem is introduced without real benefit
- historical logs remain mixed into normative guidance
- a repo has many results folders but no readable experiment journal
- low-certainty state or one-off findings are promoted into durable docs
