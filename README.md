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

## Provenance and chain of custody

Every asset carries metadata — not just what it is, but who made it, when, why, who's touched it since, and what keeps it alive. Without provenance, an asset is an artefact. With it, an asset is evidence.

Every asset answers six questions:

1. **Who created it** — which stage and skill produced it
2. **When** — timestamp
3. **What was happening** — the context that led to this asset existing
4. **Where the proof is** — a commit, PR, or link traceable in under 60 seconds
5. **Who touched it since** — full chain of custody, every modification logged
6. **What keeps it alive** — which operation or playbook actively compounds it

An asset with no compounding operation is undefended. A debrief should flag it.

See [ASSET-SPEC.md](ASSET-SPEC.md) for the full schema, validity checks, confidence scoring, and status lifecycle.

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
