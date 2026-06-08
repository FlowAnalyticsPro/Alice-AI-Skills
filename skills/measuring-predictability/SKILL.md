---
name: measuring-predictability
description: Mesure la fiabilité des engagements d'une équipe dans le temps en analysant la variabilité du cycle time, le commitment rate et la predictability sprint par sprint. À utiliser par un Scrum Master quand le PO se plaint que l'équipe ne tient pas ses promesses, avant un audit agile, ou pour répondre à "peut-on faire confiance à ce que l'équipe dit qu'elle va livrer ?".
---

# Measuring Predictability (SM)

Répond à : "L'équipe est-elle prévisible ?"

## Workflow

```
- [ ] Étape 1 : Identifier le projet et son type (FAP:get_portfolio + FAP:get_project)
- [ ] Étape 2A (Scrum) : Métriques sprint (FAP:get_sprint_metrics)
- [ ] Étape 2B (Kanban) : Variabilité cycle time (FAP:get_flow_metrics)
- [ ] Étape 3 : Tendance dans le temps (FAP:get_flow_trends)
- [ ] Étape 4 : Variabilité par type d'item (FAP:get_dimension_metrics)
- [ ] Étape 5 : Scorer + identifier la cause → produire le verdict
```

## Appels MCP

**Étape 2A — Scrum** : `FAP:get_sprint_metrics` `{ projectId }` → predictability, commitmentRate, velocity P50/P85, variability

**Étape 2B — Kanban** : `FAP:get_flow_metrics` `{ projectId, period: "THREE_MONTHS" }` → cycleTime P50/P85/P98, variability

**Étape 3** : `FAP:get_flow_trends` `{ projectId, metric: "throughput", granularity: "WEEKLY" }` (Kanban) ou `metric: "velocity", granularity: "SPRINT"` (Scrum)

**Étape 4** : `FAP:get_dimension_metrics` `{ projectId, dimension: "issueType" }` → variabilité par type (Bug, Story, Spike...)

## Indicateurs clés

**Scrum** : predictability ≥ 80% ✅ | commitment rate 80-100% ✅ | variabilité vélocité ≤ 20% ✅

**Kanban** : ratio P85/P50 ≤ 1.5 ✅ | variabilité ≤ 25% ✅

Voir [rules.md](rules.md) pour la table de diagnostic des causes.

## Format de sortie

Voir [output.md](output.md).

## Exemples

Voir [examples.md](examples.md).
