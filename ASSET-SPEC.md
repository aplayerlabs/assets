# Asset Spec

How an asset is described, tracked, and trusted across A Player OS.

## Format

Every asset is a markdown file with YAML frontmatter. The frontmatter is the machine-readable contract. The body is the human-readable description.

```yaml
---
# Identity
name: [kebab-case identifier, unique within type]
type: [tokens | specs | code | decisions | components | models]
title: [human-readable name, one line]
description: [what this asset is and what it's for, 1-2 sentences]

# Provenance — who made it, when, where
created_by: [stage/skill that produced it — e.g. playbooks/design]
created_at: [ISO 8601 datetime]
origin_context: [what was happening when this asset was created, one sentence]
origin_reference: [link, commit SHA, or PR that produced it — traceable in under 60 seconds]

# Chain of custody — who touched it and why
last_touched_by: [stage/skill that last modified it]
last_touched_at: [ISO 8601 datetime]
touch_history:
  - who: [stage/skill]
    when: [ISO 8601]
    what: [one-line description of the change]
    reference: [commit, PR, or link]

# Compounding — what keeps this asset alive
compounds_via: [name of the operation or playbook that maintains it]
compound_cadence: [how often — daily, weekly, on-event, manual]
last_compound_cycle: [ISO 8601 datetime of last time the operation ran against this asset]

# Evaluation
status: [active | stale | deprecated]
confidence: [high | medium | low — how trustworthy is this asset right now]
review_status: [current | needs_review | under_review]
last_reviewed_by: [who last evaluated this asset]
last_reviewed_at: [ISO 8601 datetime]
staleness_threshold_days: [number — days without a touch before status auto-degrades to stale]

# Dependencies
depends_on: [list of other asset names this asset requires]
depended_on_by: [list of other asset names that require this asset]
---
```

## Provenance — The Chain of Custody

Provenance is the metadata that makes an asset trustworthy. Without it, an asset is an artefact. With it, an asset is evidence.

Every asset must answer these questions:

1. **Who created it.** Which stage and skill produced this asset. A design token created by `playbooks/design` carries different context than one created manually.

2. **When it was created.** Timestamp. Recency affects trust. A decision made yesterday may supersede one from three months ago.

3. **What was happening.** The `origin_context` field. Not just "created during design phase" — what specific problem or conversation led to this asset existing.

4. **Where the proof is.** The `origin_reference` field. A commit SHA, a PR link, a Figma URL. A reviewer can reach the original creation event in under 60 seconds.

5. **Who touched it since.** The `touch_history` array. Every modification is logged — who, when, what changed, and a reference to the change. This is the chain of custody.

6. **What keeps it alive.** The `compounds_via` field. Which operation or playbook actively maintains this asset. An asset with no `compounds_via` is undefended.

## Validity Checks

Every asset must pass these checks. An asset that fails any check should be flagged for review.

**1. Completeness.** All required frontmatter fields are populated. No placeholder text, no "unknown" where the answer exists.

**2. Traceability.** The asset links to its origin. `origin_reference` is populated and resolvable. A reviewer can find the creation event in under 60 seconds.

**3. Custody.** The `touch_history` has no gaps. Every change to the asset is logged with who, when, and what.

**4. Compounding.** The `compounds_via` field names a real operation or playbook. That operation has actually run against this asset within the `compound_cadence`. If it hasn't, the asset is stalling.

**5. Freshness.** The asset's `last_touched_at` is within the `staleness_threshold_days`. If it's been longer, status should be `stale` — not silently pretending to be `active`.

### Signal health

`(assets passing all 5 checks) / (total assets)` — target: 90%+. Below 70% means the asset layer is degrading — debriefs should flag this.

## Status Lifecycle

```
active → stale → deprecated
         ↑
         └── active (if touched/reviewed)
```

- **active** — asset is being compounded. An operation runs against it or a playbook maintains it. Confidence is high or medium.
- **stale** — asset hasn't been touched within its `staleness_threshold_days`. Still exists, still referenced, but trust is degrading. A debrief should flag it.
- **deprecated** — asset is no longer needed. Retained for history and traceability. Can be archived.

An asset's status should never be manually set to `active` without a corresponding touch in `touch_history`. Reactivation requires work, not just a flag flip.

## Confidence

| Level | Meaning |
|-------|---------|
| **high** | Asset was recently created or reviewed. Provenance is complete. Compounding operation is running. No known issues. |
| **medium** | Asset exists and is referenced, but hasn't been reviewed recently. Or: provenance has gaps. Or: the compounding operation exists but hasn't run this cycle. |
| **low** | Asset is stale, provenance is incomplete, or the compounding operation has stopped. Trust this asset with caution. |

Confidence is a human judgment, not a calculated score. Debriefs evaluate confidence. Operatives consume it as a signal.

## Required vs Optional Fields

| Field | Required | Why |
|-------|----------|-----|
| `name` | Yes | Identity |
| `type` | Yes | Determines directory |
| `title` | Yes | Human readability |
| `created_by` | Yes | Provenance — who made it |
| `created_at` | Yes | Provenance — when |
| `status` | Yes | Current state |
| `description` | Recommended | Context for anyone discovering the asset |
| `origin_context` | Recommended | Why this asset exists |
| `origin_reference` | Recommended | Traceability |
| `compounds_via` | Recommended | What keeps it alive |
| `confidence` | Recommended | How much to trust it |
| All others | Optional | Fill in as the asset matures |

## Naming Conventions

- Use kebab-case: `ee-design-tokens`, not `EE Design Tokens`
- Be specific: `tpa-npc-api-contract`, not `api-contract`
- Include client or project prefix when the asset is client-specific
- Asset names are unique within their type directory

## Directory Structure

```
assets/
├── tokens/[name].md      ← design primitives, brand, style
├── specs/[name].md       ← operative specs, deployment manifests
├── code/[name].md        ← shared application code, libraries
├── decisions/[name].md   ← decision logs, trade-off records
├── components/[name].md  ← shared patterns, templates
└── models/[name].md      ← trained models, prompts, agent configs
```

Each asset is a markdown file with YAML frontmatter and a body. The body describes the asset, its purpose, how it compounds, and any notes for maintainers.
