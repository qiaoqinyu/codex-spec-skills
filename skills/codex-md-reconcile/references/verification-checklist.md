# Verification Checklist

Run this after drafting and again after applying approved edits.

## Repository Reality

- referenced paths exist
- referenced commands have a real source in the repo
- secondary routers point to real files and directories
- environment instructions still match config reality
- dangerous operations are still gated correctly

## Structure

- `AGENTS.md` remains short and routing-focused
- topic detail was pushed into `specs/*.md` instead of copied into the entrypoint
- duplicate rules were removed or trimmed to pointers
- no invented files were introduced without clear need
- no extra navigation layer was added without meeting the threshold

## Routing

- `AGENTS.md` points to the real topic docs when they exist
- canonical home for each major rule is clear
- primary and secondary routers have clearly separated jobs
- moved or condensed content still has a readable pointer from the old location

## Change Budget

- the fix stayed minimal for the problem being solved
- no broad rewrite happened when a narrow repair would do
- `specs/index.md` or `rules/` was not introduced by default

## Proof Of Work

- files inspected are listed in the report
- commands used for verification are listed in the report
- routers verified are listed in the report
- any ambiguity left open is stated explicitly
- any `leave alone` decision has a stated reason

## Failure Handling

If any check fails:

- report the exact failed check
- include the path or command involved
- mark the proposal as incomplete instead of pretending success
