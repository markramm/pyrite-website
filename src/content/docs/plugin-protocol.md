---
title: Plugin Protocol
description: Extend Pyrite with custom entry types, MCP tools, CLI commands, validators, and lifecycle hooks.
order: 9
section: build
---

Pyrite's plugin protocol lets extensions hook into nearly every part of the system. A plugin is a Python class that implements one or more methods from the protocol.

## Extension points

| Method | Purpose |
|--------|---------|
| `get_entry_classes()` | Custom entry types with serialization |
| `get_type_metadata()` | Field definitions, AI instructions, presets |
| `get_collection_types()` | Custom collection types |
| `get_mcp_tools(tier)` | Per-tier MCP tools |
| `get_cli_app()` | Typer sub-commands |
| `get_validators()` | Entry validation rules |
| `get_migrations()` | Schema migration functions |
| `get_relationship_types()` | Semantic relationship definitions |
| `before_save` / `after_save` | Lifecycle hooks on write |
| `before_delete` / `after_delete` | Lifecycle hooks on delete |

## Minimal plugin

```python
# my_plugin/__init__.py
class MyPlugin:
    name = "my-plugin"

    def get_type_metadata(self):
        return {
            "recipe": {
                "description": "A cooking recipe",
                "fields": {
                    "prep_time": {"type": "number"},
                    "cuisine": {
                        "type": "select",
                        "options": ["italian", "japanese", "mexican"],
                    },
                    "ingredients": {
                        "type": "list",
                        "items": {"type": "text"},
                    },
                },
            },
        }
```

Register via Python entry points in `pyproject.toml`:

```toml
[project.entry-points."pyrite.plugins"]
my-plugin = "my_plugin:MyPlugin"
```

## Shipping extensions

Six extensions ship with Pyrite:

| Extension | Purpose | Key Types |
|-----------|---------|-----------|
| **software-kb** | Software project management | ADRs, components, backlog items, standards, runbooks |
| **zettelkasten** | CEQRC maturity workflow | Notes with maturity progression |
| **encyclopedia** | Articles with review workflow | Articles, reviews, voting |
| **social** | Engagement tracking | Social interactions |
| **cascade** | Timeline research | Timeline events, actors, capture lanes |
| **task** | Work coordination | 7-state task workflow with atomic claim and decomposition |

## Installing extensions

```bash
pip install -e extensions/software-kb
pip install -e extensions/zettelkasten
pip install -e extensions/encyclopedia
pip install -e extensions/social
pip install -e extensions/cascade
pip install -e extensions/task
```

Plugins are discovered automatically via entry points — no configuration needed.
