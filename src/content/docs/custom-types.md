---
title: Custom Types
description: Define domain-specific entry types with schema validation in kb.yaml.
order: 6
section: concepts
---

Pyrite entries are typed. Each type defines fields with validation rules, so your knowledge base enforces structure automatically.

## Defining types

Types are defined in your `kb.yaml` file:

```yaml
name: legal-research
kb_type: generic
types:
  case:
    description: "Legal case or proceeding"
    fields:
      jurisdiction:
        type: select
        options: [federal, state, international]
      status:
        type: select
        options: [active, decided, appealed, settled]
      filing_date:
        type: date
      parties:
        type: list
        items:
          type: text
```

## Field types

| Type | Description |
|------|-------------|
| `text` | Free text string |
| `number` | Numeric value |
| `date` | Date (YYYY-MM-DD) |
| `datetime` | Date and time |
| `checkbox` | Boolean true/false |
| `select` | Single choice from options list |
| `multi-select` | Multiple choices from options list |
| `object-ref` | Reference to another entry by ID |
| `list` | Array of typed items |
| `tags` | Tag list |

## Schema versioning

Types support versioning for safe schema evolution:

```yaml
types:
  case:
    version: 2
    fields:
      methodology:
        type: text
        required: true
        since_version: 2  # required for new entries, warning-only for legacy
```

Entries track their schema version in `_schema_version` frontmatter. Use `pyrite schema migrate` to apply registered migrations — it produces a reviewable git diff.

```bash
# See what changed between versions
pyrite schema diff --kb=research

# Apply migrations
pyrite schema migrate --kb=research
```

## Built-in types

Ten entry types ship out of the box: `note`, `person`, `organization`, `event`, `document`, `topic`, `relationship`, `timeline`, `collection`, `qa_assessment`.

All entries support `aliases` for alternate names that resolve in wikilinks and autocomplete.
