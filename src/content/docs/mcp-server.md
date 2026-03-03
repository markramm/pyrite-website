---
title: MCP Server
description: Three-tier MCP tools for read, write, and admin access to your knowledge base.
order: 5
section: concepts
---

Pyrite includes a built-in MCP server that lets any compatible AI agent (Claude Desktop, Claude Code, Cursor, etc.) interact with your knowledge bases.

## Three permission tiers

Each tier includes the tools from lower tiers.

| Tier | Tools |
|------|-------|
| **read** (14) | `kb_list`, `kb_search`, `kb_get`, `kb_timeline`, `kb_tags`, `kb_backlinks`, `kb_stats`, `kb_schema`, `kb_orient`, `kb_batch_read`, `kb_list_entries`, `kb_recent`, `kb_qa_validate`, `kb_qa_status` |
| **write** (+6) | read + `kb_create`, `kb_bulk_create`, `kb_update`, `kb_delete`, `kb_link`, `kb_qa_assess` |
| **admin** (+4) | write + `kb_index_sync`, `kb_manage`, `kb_commit`, `kb_push` |

## Starting the server

```bash
# Full access (default)
pyrite mcp

# Read-only (safe for untrusted agents)
pyrite mcp --tier read

# Write access (no admin tools)
pyrite mcp --tier write
```

## Key tools

- **`kb_search`** — keyword, semantic, or hybrid search with pagination and field projection
- **`kb_orient`** — one-shot KB summary for agent onboarding (types, stats, recent activity)
- **`kb_batch_read`** — fetch multiple entries in a single call
- **`kb_bulk_create`** — create up to 50 entries per call with best-effort semantics
- **`kb_schema`** — inspect type definitions, field schemas, and validation rules

All paginated tools support `limit`/`offset` params and return a `has_more` flag. Search results return snippets by default — use `include_body` for full text, `fields` for projection.

## Prompts and resources

The MCP server also exposes:

- **4 prompts**: `research_topic`, `summarize_entry`, `find_connections`, `daily_briefing`
- **Resources**: `pyrite://kbs`, `pyrite://kbs/{name}/entries`, `pyrite://entries/{id}`

## Plugin tools

Plugins add their own tools per tier. For example, the software-kb extension adds `sw_adrs`, `sw_backlog`, `sw_new_adr`, `sw_components`, and `sw_standards`.
