---
title: Quick Start
description: Install Pyrite, create a knowledge base, and connect to Claude in 5 minutes.
order: 1
section: get-started
---

## Install

```bash
pip install pyrite             # Core
pip install "pyrite[all]"      # Core + AI + semantic search + dev tools
pip install "pyrite[ai]"       # OpenAI + Anthropic + Gemini SDKs
pip install "pyrite[semantic]" # sentence-transformers + sqlite-vec
```

## Create a knowledge base

```bash
pyrite init --template research --path my-kb
cd my-kb
```

Templates available: `research`, `software`, `zettelkasten`, `empty`, and more.

## Add some entries

```bash
pyrite create -k my-kb --type person --title "Sarah Chen" \
  --body "Engineering lead. Considering move to consulting." --tags "team,engineering"

pyrite create -k my-kb --type note --title "Switch to async standups" \
  --body "Decided 2026-03-01. Reduces meeting load by 3hrs/week." --tags "process"
```

## Search

```bash
# Keyword search
pyrite search "career transition" -k my-kb

# Semantic search (finds conceptually related content)
pyrite search "team decisions" -k my-kb --mode=semantic

# Hybrid (both at once)
pyrite search "team decisions" -k my-kb --mode=hybrid
```

## Connect to Claude Desktop or Claude Code

Add to your MCP configuration:

```json
{
  "mcpServers": {
    "pyrite": {
      "command": "pyrite",
      "args": ["mcp"]
    }
  }
}
```

Now any AI that speaks MCP can search, read, and write your knowledge base.

## What just happened

Pyrite created markdown files with YAML frontmatter in a git-versioned directory. It built a SQLite FTS5 index on top for fast search, and the MCP server exposes that index to any AI agent.

Your files are the source of truth. The index is derived. Rebuild it any time with `pyrite index build`.
