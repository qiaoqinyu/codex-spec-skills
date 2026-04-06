# codex-spec-skills

OpenAI Codex skills for Codex guidance-layer maintenance and project-local
harness state.

This repository now contains three reusable skills:

- `codex-harness-state`: create or refresh a minimal `.agents/state/` layer for
  progress tracking, session handoff, and experiment/workstream continuity.
- `codex-md-reconcile`: reconcile, bootstrap, or migrate Codex guidance such as
  `AGENTS.md`, `specs/*.md`, and related skill docs.
- `codex-md-capture`: capture durable learnings from the current session and
  write them back into the right Codex guidance layer with minimal churn.

Older `spec-*` and `specs-*` skill names are deprecated and no longer the
canonical interface for this repository.

Here, `md` means the Markdown-based Codex guidance layer: `AGENTS.md`,
`specs/*.md`, and related skill docs. It does not mean `specs/*.md` only, and
it does not own mutable runtime state such as `.agents/state/*`.

## Repository Layout

```text
skills/
  codex-harness-state/
  codex-md-capture/
  codex-md-reconcile/
```

Each skill follows the Codex skill layout:

- `SKILL.md`: required instructions and trigger metadata
- `agents/openai.yaml`: optional Codex app metadata
- `references/`: optional supporting docs loaded only when needed

## When To Use These Skills

Use these skills when you want to keep Codex guidance clean, discoverable, and
durable across sessions without mixing stable docs with mutable session state.

## Mental Model

Think of the split like this:

1. `codex-harness-state` owns mutable session state.
   Files such as `.agents/state/progress.md`,
   `.agents/state/session-handoff.md`, and experiment/workstream trackers live
   here.
2. `codex-md-reconcile` owns guidance structure repair.
   Use it when `AGENTS.md`, `specs/*.md`, or related Codex docs are stale,
   duplicated, poorly routed, or need bootstrap/migration.
3. `codex-md-capture` owns narrow durable write-back.
   Use it after a session proves a concrete new rule, command, or project truth
   that should be written into the right guidance file with minimal churn.

Typical split:

1. Use `codex-harness-state` when a repo needs a lightweight `.agents/state/`
   layer for progress, handoff, or parallel experiment tracking.
2. Use `codex-md-reconcile` when the repo guidance needs bootstrap, migration,
   reconciliation, cleanup, or routing repair.
3. Use `codex-md-capture` after a session produces durable new project truth
   that should be written back into `AGENTS.md`, `specs/*.md`, or a related
   skill reference.

Common confusion to avoid:

- `codex-md-*` is not "specs only". It covers the broader Codex guidance layer.
- `codex-harness-state` is not a docs-reconcile skill. It manages mutable state
  scaffolding, not canonical guidance ownership.
- If the real problem is guidance shape or missing routing, start with
  `codex-md-reconcile`.
- If the real problem is "we learned one durable thing this session", start
  with `codex-md-capture`.

## Install

Official Codex docs use this personal skill directory:

```text
$HOME/.agents/skills/
```

In some local setups, `~/.codex/skills/` is also in active use, so either of
these user-level locations may be relevant in practice:

```text
$HOME/.agents/skills/
$HOME/.codex/skills/
```

For team or repo-local use, check them into:

```text
.agents/skills/
```

Example:

```bash
gh repo clone qiaoqinyu/codex-spec-skills
cp -a codex-spec-skills/skills/codex-harness-state ~/.agents/skills/
cp -a codex-spec-skills/skills/codex-md-reconcile ~/.agents/skills/
cp -a codex-spec-skills/skills/codex-md-capture ~/.agents/skills/
```

If your local Codex installation is using `~/.codex/skills/` instead, copy the
same folders there.

After installation, restart Codex if the new skills do not appear immediately.
