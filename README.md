# gameball-mcp-codex

Per-tool documentation for the [Gameball MCP server](https://github.com/Gameball-Engineering/gameball-mcp).

Each `<tool_name>.md` file is a detailed codex entry for one MCP tool — filter syntax, parameter semantics, examples, and protocols. The MCP server exposes them on demand at `codex://tools/<tool_name>` so callers fetch them only when needed (keeps per-session token usage low).

## How the MCP server consumes this repo

The server reads docs from `CODEX_PATH` (a local directory). When `CODEX_REPO` also points here, the server clones this repo into `CODEX_PATH` on boot and pulls the latest `CODEX_REF` (default `main`) on a schedule and on webhook trigger. See the [server README](https://github.com/Gameball-Engineering/gameball-mcp/blob/main/README.md#configuration) for env-var details.

A doc edit landed on `main` here will be live on every running server within `CODEX_SYNC_INTERVAL_MS` (default 10 min) — no server redeploy.

## Partial transclusion

Some shared instruction blocks (template-flow, core-required fields, update-flow) are referenced inside docs as `{{> partial_name}}` markers. The MCP server replaces these at read time using constants defined in its `src/tools/shared.ts`. **Do not** manually expand the markers in this repo — the source of truth for partial content lives in the server.

Available partials:
- `{{> template_flow}}` — template-first creation flow used by campaign create tools
- `{{> core_required}}` — required fields callers must always provide
- `{{> update_flow}}` — GET-then-PUT pattern for update tools

## Editing guidelines

- One file per tool, matching the tool's registered name (e.g. `get_customers.md` for the `get_customers` tool).
- Use Markdown headings, tables, and fenced code blocks freely.
- Prefer concrete examples over abstract descriptions.
- Don't include the tool's parameter schema — the MCP SDK already exposes it from the tool's `inputSchema`.
- Front-load the most important content: filters, gotchas, ID-resolution requirements.

## Sync triggers

1. **Boot** — every server start clones (if missing) or pulls.
2. **Interval** — periodic pull every `CODEX_SYNC_INTERVAL_MS`.
3. **Webhook** — `POST /admin/codex-sync` with `X-Hub-Signature-256` HMAC triggers an immediate pull. Wire this from the git provider's webhook on `push` to `main` for instant updates.
