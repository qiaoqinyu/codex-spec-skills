---
name: tavily-hikari-local
description: Use the local Tavily Hikari CLI for direct HTTP search, extract, map, crawl, and research without relying on remote MCP transport.
compatibility: opencode
---
## What I do

- Call the bundled CLI at `scripts/tavily-hikari` from this skill directory.
- Talk directly to the Tavily Hikari HTTP API at `TAVILY_HIKARI_BASE_URL` or the default `https://tavily.ivanli.cc/api/tavily`.
- Use `TAVILY_HIKARI_TOKEN` for Bearer auth.
- Return raw JSON that is easy to inspect or summarize.

## When to use me

- Use this for Tavily-backed web search, page extraction, site mapping, crawling, and research.
- Prefer this over remote Tavily MCP when OpenCode's remote MCP transport is unstable or timing out.
- If the user asks for Tavily specifically, or wants to use the custom Hikari endpoint, use this skill first.

## Commands

- From this skill directory, run `./scripts/tavily-hikari ...`.
- Search:
  - `./scripts/tavily-hikari search "latest AI agent news" --search-depth fast --max-results 3`
- Extract:
  - `./scripts/tavily-hikari extract "https://openai.com/index/introducing-gpt-5/"`
- Map:
  - `./scripts/tavily-hikari map "https://docs.python.org" --limit 10`
- Crawl:
  - `./scripts/tavily-hikari crawl "https://docs.python.org/3/tutorial/" --limit 5`
- Research:
  - `./scripts/tavily-hikari research "latest AI agent news" --model mini`
  - `./scripts/tavily-hikari research-status "<request_id>"`
  - `./scripts/tavily-hikari research-poll "<request_id>" --wait-timeout 300`

## Notes

- Add `--json` when you want compact machine-friendly output.
- Add `--timeout 120` for slower endpoints like crawl or research.
- If the API returns an error, report it directly instead of pretending the request worked.
