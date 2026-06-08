---
name: diagnosing-flow-health
description: Diagnostique la santé du flow d'une équipe en évaluant 5 dimensions — WIP, aging, efficience, blocages, throughput — et produit un verdict global avec score par dimension. À utiliser par un Scrum Master ou Flow Master avant une rétrospective, un bilan hebdomadaire, ou quand l'équipe sent que quelque chose ne va pas sans pouvoir identifier quoi.
---

# Diagnosing Flow Health (SM)

Répond à : "Notre flow est-il sain aujourd'hui ?"

## Workflow

```
- [ ] Étape 1 : Identifier le projet (FAP:get_portfolio)
- [ ] Étape 2 : Métriques globales — WIP + Throughput (FAP:get_flow_metrics)
- [ ] Étape 3 : Aging des items en cours (FAP:get_issues + P85 de l'étape 2)
- [ ] Étape 4 : Blocages actifs (FAP:get_blocked_tickets)
- [ ] Étape 5 : Répartition par étape (FAP:get_step_analysis)
- [ ] Étape 6 : Tendance cycle time (FAP:get_flow_trends)
- [ ] Étape 7 : Scorer les 5 dimensions → verdict global
```

## Appels MCP

**Étape 2** — `FAP:get_flow_metrics` `{ projectId, period: "THREE_MONTHS" }` → throughput, cycleTime P50/P85, efficiency, variability

**Étape 3** — `FAP:get_issues` `{ projectId, status: "IN_PROGRESS", orderBy: "aging", order: "DESC" }` → items > P85

**Étape 4** — `FAP:get_blocked_tickets` `{ projectId }` → count, durée moyenne

**Étape 5** — `FAP:get_step_analysis` `{ projectId }` → items/étape, temps médian, bottleneckScore

**Étape 6** — `FAP:get_flow_trends` `{ projectId, metric: "cycleTime", granularity: "WEEKLY" }` → tendance

## Scoring des 5 dimensions

Voir [rules.md](rules.md) pour les seuils 🟢/🟡/🔴 par dimension et le verdict global.

## Format de sortie

Voir [output.md](output.md).

## Exemples

Voir [examples.md](examples.md).

## Règle obligatoire

Toujours mentionner un point positif, même si le verdict est 🔥 EN CRISE. Toujours terminer par une seule action prioritaire.
