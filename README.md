# codex-spec-skills

OpenAI Codex skills for Codex guidance reconciliation and session capture.

This repository now contains two reusable skills:

- `codex-md-reconcile`: reconcile, bootstrap, or migrate Codex guidance such as
  `AGENTS.md`, `specs/*.md`, and related skill docs.
- `codex-md-capture`: capture durable learnings from the current session and
  write them back into the right Codex guidance layer with minimal churn.

Older `spec-*` and `specs-*` skill names are deprecated and no longer the
canonical interface for this repository.

## Repository Layout

```text
skills/
  codex-md-capture/
  codex-md-reconcile/
```

Each skill follows the Codex skill layout:

- `SKILL.md`: required instructions and trigger metadata
- `agents/openai.yaml`: optional Codex app metadata
- `references/`: optional supporting docs loaded only when needed

## When To Use These Skills

Use these skills when you want to keep Codex guidance clean, discoverable, and
durable across sessions.

Typical split:

1. Use `codex-md-reconcile` when the repo guidance needs bootstrap, migration,
   reconciliation, cleanup, or routing repair.
2. Use `codex-md-capture` after a session produces durable new project truth
   that should be written back into `AGENTS.md`, `specs/*.md`, or a related
   skill reference.

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
cp -a codex-spec-skills/skills/codex-md-reconcile ~/.agents/skills/
cp -a codex-spec-skills/skills/codex-md-capture ~/.agents/skills/
```

If your local Codex installation is using `~/.codex/skills/` instead, copy the
same folders there.

After installation, restart Codex if the new skills do not appear immediately.
