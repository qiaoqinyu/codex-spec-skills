# Harness Quality Checklist

Use this checklist after creating or refactoring a spec-first harness.

## Passing Shape

A strong harness has:

- Thin root adapter files
- A clear `specs/index.md` that routes into the rest of the knowledge base
- A shared `specs/` knowledge base
- Clear task routing from adapters into specs
- Stable truths separated from volatile history
- Important invariants enforced mechanically where possible
- Cross-links that actually resolve

## Review Rubric

Score each area as `strong`, `acceptable`, or `needs work`.

### 1. Navigation Quality

Check:

- Can a new agent find the right spec quickly?
- Does the root adapter act like a map rather than a manual?
- Does `specs/index.md` make the rest of the docs discoverable without guesswork?
- Are task categories or scenarios obvious?
- Do the root adapters actually point to `specs/index.md`?

Needs work when:

- The adapter is a monolith
- `specs/index.md` is missing or vague
- Key specs are missing from the route map
- The agent would need to guess where a fact lives
- Research and implementation context are mixed together unnecessarily

### 2. Single Source of Truth

Check:

- Does each important fact have one clear canonical home?
- Are shared truths stored in `specs/` rather than repeated per agent?

Needs work when:

- `AGENTS.md` and `CLAUDE.md` each carry their own version of the same fact
- The same command is maintained in multiple places

### 3. Progressive Disclosure

Check:

- Does the harness start small and lead to deeper context only when needed?
- Are always-loaded files limited to truly common context?
- Has compression removed noise without deleting critical implementation detail?

Needs work when:

- Every reference is auto-loaded
- Bulky archives or deep references sit in root adapters
- Important gotchas, contracts, or checklists were stripped out in the name of
  brevity

### 4. Scope Control

Check:

- Are any remaining scoped compatibility shims still justified?
- Are shared truths still shared, rather than copied into each shim?

Needs work when:

- Scoped shims duplicate full specs
- Local adapters repeat the repo root adapter almost verbatim

### 5. Freshness

Check:

- Do linked files exist?
- Do commands still match the repo?
- Does the structure still reflect the actual code layout?

Needs work when:

- Dead links exist
- Moved code invalidates the specs
- Old instructions remain as zombie guidance

### 6. Stability vs. Volatility

Check:

- Are stable lessons kept separate from raw history?
- Are plans and archives clearly marked as non-normative when appropriate?
- Are experiment results, debugging notes, and metric snapshots stored in
  archive files rather than normative specs?

Needs work when:

- Root docs contain experiment-by-experiment logs
- Historical metrics crowd out reusable guidance

### 7. Mechanical Enforcement

Check:

- Have critical invariants been pushed into code, tests, or CI where possible?
- Does documentation avoid acting as the only guardrail for hard requirements?

Needs work when:

- A fragile invariant exists only in markdown
- Agents must remember too many constraints that the repo could enforce directly

## Anti-Patterns

Flag these immediately:

- One huge adapter file with everything inline
- Agent-specific copies of the same repo truth
- `specs/` used as an uncurated markdown dump
- `specs/` reduced to shallow summaries that no longer prevent real mistakes
- Archive material mixed into normative specs
- Legacy Claude-specific shims left in place without a reason
- Over-splitting into dozens of files with no useful index

## Quick Validation Commands

Use simple repository checks after edits:

```bash
find specs -type f | sort
rg -n "specs/" AGENTS.md CLAUDE.md GEMINI.md 2>/dev/null
rg -n "TODO|TBD|FIXME" specs AGENTS.md CLAUDE.md GEMINI.md 2>/dev/null
```

Add project-specific validation as needed:

- Link checking
- Command verification
- Spec freshness lints
- Structural tests for architecture invariants
