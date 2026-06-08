---
name: analyzing-innovation-vs-debt
description: Révèle comment la capacité engineering est répartie entre innovation (nouvelles fonctionnalités), dette technique, maintenance et opérations, et détecte les signaux de debt spiral. À utiliser par un CEO ou CPO pour un comité stratégique, une revue budgétaire, ou pour répondre à "pourquoi l'engineering livre peu de nouvelles features malgré une grande équipe ?".
---

# Analyzing Innovation vs Debt (CEO/CPO)

Répond à : "Quelle part de notre capacité va à l'innovation vs la dette ?"

## Workflow

```
- [ ] Étape 1 : Cartographier l'organisation (FAP:get_programs + FAP:get_portfolio)
- [ ] Étape 2 : Répartition actuelle par type d'item (FAP:get_dimension_metrics × N projets)
- [ ] Étape 3 : Évolution de la répartition sur 6 mois (FAP:get_flow_trends × N projets)
- [ ] Étape 4 : Change Failure Rate — proxy dette (FAP:get_dora_metrics)
- [ ] Étape 5 : Vue comparative cross-produits (FAP:compare_projects)
- [ ] Étape 6 : Détecter Debt Spiral → produire l'allocation stratégique
```

## Appels MCP

**Étape 2** — `FAP:get_dimension_metrics` `{ projectId, dimension: "issueType" }` → throughput par type d'item

**Étape 3** — `FAP:get_flow_trends` `{ projectId, metric: "throughput", granularity: "MONTHLY" }` → évolution mensuelle par type

**Étape 4** — `FAP:get_dora_metrics` `{ viewId }` → changeFailureRate comme signal dette

## 4 catégories d'allocation

```
🚀 INNOVATION (CapEx) → Features, Epics, R&D
🔧 DETTE TECH (CapEx différé) → TechDebt, Refactoring, Migration
🐛 MAINTENANCE (OpEx) → Bugs, Hotfixes, Regressions
⚙️ OPÉRATIONS (OpEx) → Tasks, Spikes, Support, DevOps
```

## Benchmarks par stade

| Stade | Innovation | Dette | Maintenance | Alerte si |
|-------|-----------|-------|-------------|-----------|
| Startup | 70-80% | 10-15% | 5-10% | Innovation < 60% |
| Croissance | 55-65% | 15-20% | 10-15% | Innovation < 45% |
| Maturité | 40-55% | 20-30% | 15-20% | Innovation < 30% |
| Legacy | 20-35% | 25-35% | 25-35% | Maintenance > 50% |

Voir [rules.md](rules.md) pour la détection de Debt Spiral et la décision selon le verdict.

## Format de sortie

Voir [output.md](output.md) — barre de progression ASCII + 1 décision.

## Paramètre à préciser

Demander le **stade de l'entreprise** au CEO/CPO si non déduit du contexte — le benchmark diffère selon le stade.
