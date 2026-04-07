# Asset Spec

How an asset is described, versioned, and tracked across A Player OS.

## Format

Every asset carries YAML frontmatter:

```yaml
---
name: [human-readable identifier]
type: [tokens | specs | code | decisions | components | models]
created-by: [stage/skill that produced it]
last-touched-by: [stage/skill that last modified it]
compounds-via: [operation or playbook that keeps it current]
status: [active | stale | deprecated]
created: [ISO date]
last-touched: [ISO date]
---
```

## Required fields

| Field | Required | Why |
|-------|----------|-----|
| `name` | Yes | Human-readable identifier. Must be unique within its type directory. |
| `type` | Yes | Determines which directory it lives in. |
| `created-by` | Yes | Provenance. Which stage produced this asset. |
| `status` | Yes | Current state. Defaults to `active` on creation. |

## Optional fields

| Field | When to use |
|-------|------------|
| `last-touched-by` | Updated automatically whenever a stage modifies the asset. |
| `compounds-via` | Name the operation or playbook that keeps this asset current. An asset without this field is undefended. |
| `created` | ISO 8601 date. Set on creation. |
| `last-touched` | ISO 8601 date. Updated on every modification. |

## Status lifecycle

```
active → stale → deprecated
```

- **active** — asset is being compounded. An operation runs against it or a playbook maintains it.
- **stale** — asset hasn't been touched in multiple cycles. A debrief should flag it.
- **deprecated** — asset is no longer needed. Retained for history. Can be archived.

## Naming conventions

- Use kebab-case: `ee-design-tokens`, not `EE Design Tokens`
- Be specific: `tpa-npc-api-contract`, not `api-contract`
- Include the client or project prefix when the asset is client-specific

## Directory structure

Assets are organised by type:

```
assets/
├── tokens/[name].md
├── specs/[name].md
├── code/[name].md
├── decisions/[name].md
├── components/[name].md
└── models/[name].md
```

Each asset is a markdown file with YAML frontmatter and a body describing the asset, its purpose, and how it compounds.
