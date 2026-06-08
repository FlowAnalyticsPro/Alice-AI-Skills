---
name: measuring-delivery-capacity
description: Mesure la capacité de delivery réelle d'un périmètre d'équipes en décomposant le throughput entre Innovation, Dette technique, Maintenance et Opérations, et identifie les pertes de capacité évitables. À utiliser par un Engineering Manager pour un roadmap planning, un arbitrage budgétaire, ou pour expliquer au business pourquoi l'équipe ne livre pas plus de features.
---

# Measuring Delivery Capacity (Manager)

Répond à : "Quelle est notre capacité réelle de delivery ?"

## Workflow

```
- [ ] Étape 1 : Identifier le périmètre (FAP:get_programs)
- [ ] Étape 2 : Throughput consolidé (FAP:compare_projects)
- [ ] Étape 3 : Répartition par type d'item (FAP:get_dimension_metrics × N projets)
- [ ] Étape 4 : Efficience (FAP:get_flow_metrics × N projets)
- [ ] Étape 5 : Charge bloquée (FAP:get_blocked_tickets × N projets)
- [ ] Étape 6 : Tendance sur 3 mois (FAP:get_flow_trends × N projets)
- [ ] Étape 7 : Projection 6 semaines (FAP:get_forecast × projets concernés)
- [ ] Étape 8 : Calculer les 4 ratios → message business
```

## Appels MCP

**Étape 2** — `FAP:compare_projects` `{ projectIds: [...] }` → throughput par équipe

**Étape 3** — `FAP:get_dimension_metrics` `{ projectId, dimension: "issueType" }` → Features / Bugs / TechDebt / Tasks

**Étape 4** — `FAP:get_flow_metrics` `{ projectId, period: "THREE_MONTHS" }` → efficiency

**Étape 6** — `FAP:get_flow_trends` `{ projectId, metric: "throughput", granularity: "WEEKLY" }` → tendance

## 4 Ratios clés

| Ratio | Formule | Sain | Alerte |
|-------|---------|------|--------|
| Ratio Valeur | Features / Total | > 60% | < 40% |
| Ratio Dette | (Bugs + TechDebt) / Total | < 30% | > 50% |
| Ratio Efficience | activeTime / totalTime | > 35% | < 20% |
| Ratio Gel | capacity_bloquée / Total | < 10% | > 25% |

Voir [rules.md](rules.md) pour les décisions recommandées selon les ratios.

## Format de sortie

Voir [output.md](output.md).

## Exemples

Voir [examples.md](examples.md).

## Règle clé

Si Ratio Valeur < 40% → signaler qu'une décision stratégique sur la dette est nécessaire AVANT d'ajouter du scope au roadmap. Si efficience < 20% → signaler que recruter n'améliorera pas la capacité sans réduire d'abord les inefficiences.
