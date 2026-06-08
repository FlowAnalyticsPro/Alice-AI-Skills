---
name: tracking-team-commitments
description: Calcule le taux de fiabilité de livraison consolidé de plusieurs équipes en croisant commitment rate, ponctualité sur due dates et consistance, puis produit un bilan orienté reporting management. À utiliser par un Engineering Manager pour un business review trimestriel, une réunion CODIR, ou quand le business remet en question la fiabilité de l'engineering.
---

# Tracking Team Commitments (Manager)

Répond à : "Nos équipes tiennent-elles leurs engagements ?"

## Workflow

```
- [ ] Étape 1 : Identifier le périmètre (FAP:get_programs + FAP:get_portfolio)
- [ ] Étape 2 : Comparaison cross-équipes (FAP:compare_projects)
- [ ] Étape 3 : Commitment rate par équipe Scrum (FAP:get_sprint_metrics × N)
- [ ] Étape 4 : Ponctualité sur due dates (FAP:get_due_date_analysis × N)
- [ ] Étape 5 : Tendance de la fiabilité (FAP:get_flow_trends × N)
- [ ] Étape 6 : Prévisions à risque (FAP:get_forecast × équipes concernées)
- [ ] Étape 7 : Calculer Taux de Fiabilité → message CODIR
```

## Appels MCP

**Étape 2** — `FAP:compare_projects` `{ projectIds: [...] }` → vue consolidée

**Étape 3** — `FAP:get_sprint_metrics` `{ projectId }` → commitmentRate, predictability, velocity (équipes Scrum)

**Étape 4** — `FAP:get_due_date_analysis` `{ projectId }` → punctualityRate, ticketsLate

**Étape 5** — `FAP:get_flow_trends` `{ projectId, metric: "throughput", granularity: "WEEKLY" }` → tendance

## Taux de Fiabilité par équipe

```
Taux = commitmentRate × 0.40 + punctualityRate × 0.40 + (100 - variability) × 0.20
```

| Taux | Niveau | Message business |
|------|--------|-----------------|
| 85-100% | 🟢 Excellent | Fiabilité très élevée |
| 70-84% | 🟡 Acceptable | 2-3 équipes à surveiller |
| 55-69% | 🟠 Insuffisant | ~1 engagement sur 3 non tenu |
| < 55% | 🔴 Critique | En dessous des standards |

Voir [rules.md](rules.md) pour la traduction business de chaque métrique.

## Format de sortie

Voir [output.md](output.md) — inclut message CODIR prêt à l'emploi.

## Exemples

Voir [examples.md](examples.md).
