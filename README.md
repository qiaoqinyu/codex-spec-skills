# codex-spec-skills

OpenAI Codex skills for specs-first repository setup and maintenance.

This repository contains three reusable skills:

- `spec-initialize`: bootstrap a new `specs/` layout or migrate a repo from
  legacy instruction surfaces such as `AGENTS.md`, `CLAUDE.md`, or
  `.claude/rules`.
- `specs-optimize`: audit an existing specs-first setup, report issues, and
  apply targeted cleanup.
- `specs-capture`: write durable conclusions from the current session back into
  the canonical files under `specs/`.

## Repository Layout

```text
skills/
  spec-initialize/
  specs-capture/
  specs-optimize/
```

Each skill follows the Codex skill layout:

- `SKILL.md`: required instructions and trigger metadata
- `agents/openai.yaml`: optional Codex app metadata
- `references/`: optional supporting docs loaded only when needed

## When To Use These Skills

Use these skills when you want a repo to keep shared agent guidance in a
`specs/` knowledge base instead of scattering durable project truth across
multiple prompts and instruction files.

Typical progression:

1. Run `spec-initialize` once when the repo has no clean specs-first setup.
2. Use `specs-optimize` for ongoing cleanup and routing improvements.
3. Use `specs-capture` after a session produces durable new project truth.

## Install

Official Codex docs use this personal skill directory:

```text
$HOME/.agents/skills/
```

In your current local setup, `~/.codex/skills/` is also in active use, so
either of these user-level locations may be relevant in practice:

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
cp -a codex-spec-skills/skills/spec-initialize ~/.agents/skills/
cp -a codex-spec-skills/skills/specs-optimize ~/.agents/skills/
cp -a codex-spec-skills/skills/specs-capture ~/.agents/skills/
```

If your local Codex installation is using `~/.codex/skills/` instead, copy the
same folders there.

After installation, restart Codex if the new skills do not appear immediately.
