---
name: detecting-bottlenecks
description: Identifie le goulot principal dans le workflow d'une équipe en calculant un Score de Contrainte par étape, en croisant temps médian, accumulation d'items et blocages concentrés. À utiliser par un Scrum Master avant une rétro ciblée, un kaizen, ou quand le cycle time monte sans explication visible.
---

# Detecting Bottlenecks (SM)

Répond à : "Où sont les goulots dans notre workflow ?"

## Workflow

```
- [ ] Étape 1 : Identifier le projet et ses étapes (FAP:get_portfolio + FAP:get_project)
- [ ] Étape 2 : Temps médian par étape (FAP:get_step_analysis)
- [ ] Étape 3 : Efficience globale (FAP:get_flow_metrics)
- [ ] Étape 4 : Blocages par étape (FAP:get_blocked_tickets)
- [ ] Étape 5 : Variabilité par type d'item (FAP:get_dimension_metrics)
- [ ] Étape 6 : Tendance du cycle time (FAP:get_flow_trends)
- [ ] Étape 7 : Calculer le Score de Contrainte → identifier le goulot principal
```

## Appels MCP

**Étape 2** — `FAP:get_step_analysis` `{ projectId }` → medianTimePerStep, itemsPerStep, bottleneckScore

**Étape 3** — `FAP:get_flow_metrics` `{ projectId, period: "THREE_MONTHS" }` → efficiency globale

**Étape 4** — `FAP:get_blocked_tickets` `{ projectId }` → répartition des blocages par étape

**Étape 5** — `FAP:get_dimension_metrics` `{ projectId, dimension: "issueType" }` → types qui saturent une étape

**Étape 6** — `FAP:get_flow_trends` `{ projectId, metric: "cycleTime", granularity: "WEEKLY" }` → goulot nouveau vs chronique

## Score de Contrainte par étape

```
Score = (temps_médian_étape / moyenne_toutes_étapes) × 0.5
      + (items_en_attente_étape / total_WIP) × 0.3
      + (blocages_étape / total_blocages) × 0.2
```

L'étape avec le score le plus élevé = **goulot principal**.

Voir [rules.md](rules.md) pour la classification STRUCTUREL / CONJONCTUREL / LATENT.

## Règle ToC

Il y a toujours exactement **un** goulot principal. Ne recommander d'améliorer qu'une seule étape à la fois.

## Format de sortie

Voir [output.md](output.md).

## Exemples

Voir [examples.md](examples.md).
