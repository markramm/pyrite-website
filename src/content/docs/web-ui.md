---
title: Web UI
description: SvelteKit frontend for browsing, editing, visualizing, and managing knowledge bases.
order: 8
section: reference
---

Pyrite includes an optional SvelteKit 2 + Svelte 5 frontend for browsing, visualization, and oversight.

## Editor

- WYSIWYG + markdown dual mode (Tiptap + CodeMirror)
- `[[wikilinks]]` with autocomplete, alias resolution, and pill decorations
- `![[transclusion]]` embedded content cards
- Block references: `[[entry#heading]]` and `[[entry^block-id]]`
- Slash commands in editor

## Navigation

- Quick switcher (Cmd+O)
- Command palette (Cmd+K)
- Backlinks panel
- Outline / table of contents
- Split panes

## Visualization

- Interactive knowledge graph (Cytoscape.js)
- Timeline visualization
- Collections with list, table, kanban, and gallery views
- Virtual collections via query DSL

## AI features (BYOK)

All AI features use your own API keys — no server-side inference costs.

- **Chat sidebar** (Cmd+Shift+K) — RAG chat with KB context and source citations
- **Summarize** — generate entry summaries
- **Auto-tag** — suggest tags from existing vocabulary with reasoning
- **Suggest links** — find related entries and suggest wikilinks

Supported providers: Anthropic, OpenAI, Google Gemini, OpenRouter, Ollama.

Configure in Settings > AI Provider.

## Other features

- Daily notes with calendar
- Version history with diff viewer
- Web clipper for URL content capture
- WebSocket multi-tab sync
- Starred entries
