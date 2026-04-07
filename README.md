# Assets

The center of A Player OS. Where compounding things live.

```
            PLAYBOOKS
             (build)
               ╱╲
              ╱  ╲
             ╱    ╲
            ╱      ╲
           ╱ ASSETS ╲
          ╱(compound) ╲
         ╱             ╲
        ╱               ╲
       ╱_________________╲
  DEBRIEFS          OPERATIVES
   (learn)             (run)
```

An asset is any durable artefact that compounds through reuse. Code, design systems, trained models, documented decisions, brand. Assets are the residue of playbooks running, operatives cycling, and debriefs refining. Every rotation should leave more than the last. An asset nobody's compounding is depreciating.

## How assets flow

**Playbooks** produce assets. A playbook runs and something durable comes out — application code, a design system, a deployed service, a documented decision.

**Operatives** consume and update assets. An operative runs against assets, finds what's broken, patches what's stale, and keeps them alive and current.

**Debriefs** evaluate assets. Which assets are compounding? Which are depreciating? What should the next playbook build or rebuild?

No stage owns an asset. All stages shape it. A Player OS accelerates because the assets at the center get better every turn.

## Asset types

| Type | What it is | Examples |
|------|-----------|---------|
| **tokens** | Design primitives. The smallest reusable units. | Colour palettes, spacing scales, typography, brand tokens |
| **specs** | Deployment manifests. The complete definition of something runnable. | OPERATIVES.md files, service configs, API contracts |
| **code** | Application code and infrastructure. | Apps, libraries, scripts, IaC |
| **decisions** | What was decided, why, and by whom. The institutional memory. | Architecture decisions, trade-off records, post-mortems |
| **components** | Shared patterns and templates. | UI component libraries, email templates, playbook templates |
| **models** | Trained models, prompts, and agent configurations. | Fine-tuned models, prompt libraries, agent orientations |

## Asset lifecycle

Every asset moves through A Player OS:

```
CREATED          CONSUMED          EVALUATED          IMPROVED
by a playbook → by an operative → by a debrief    → by the next playbook
  (build)          (run)            (learn)            (build better)
```

An asset that completes this cycle is compounding. An asset stuck at any stage is stalling. An asset untouched for multiple cycles is depreciating.

## Asset spec

Every asset carries metadata so A Player OS can track it:

```yaml
---
name: ee-design-tokens
type: tokens
created-by: playbooks/design
last-touched-by: operatives/brand-monitor
compounds-via: weekly brand audit operation
status: active
---
```

| Field | What it tracks |
|-------|---------------|
| `name` | Human-readable identifier |
| `type` | One of: tokens, specs, code, decisions, components, models |
| `created-by` | Which playbook or skill produced it |
| `last-touched-by` | Which stage last modified it |
| `compounds-via` | Which operation or playbook keeps it current |
| `status` | active, stale, deprecated |

An asset with no `compounds-via` is undefended. A debrief should flag it.

## Structure

```
assets/
├── tokens/        ← design primitives, brand, style
├── specs/         ← operative specs, deployment manifests
├── code/          ← shared application code, libraries
├── decisions/     ← decision logs, trade-off records
├── components/    ← shared patterns, templates
└── models/        ← trained models, prompts, agent configs
```

## Part of A Player OS

Assets is the compound stage of [A Player OS](https://github.com/aplayerlabs/os) by [A Player Labs](https://aplayerlabs.com).

| Stage | Repo |
|-------|------|
| Build | [aplayerlabs/playbooks](https://github.com/aplayerlabs/playbooks) |
| Run | [aplayerlabs/operatives](https://github.com/aplayerlabs/operatives) |
| Learn | [aplayerlabs/debriefs](https://github.com/aplayerlabs/debriefs) |
| Compound | **aplayerlabs/assets** (this repo) |

## License

MIT. See [LICENSE](LICENSE). Built by [A Player Labs](https://aplayerlabs.com).
