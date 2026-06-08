# Règles — Analyzing Innovation vs Debt

## Signaux de Debt Spiral

```
Signal 1 : Ratio Maintenance en hausse sur 3 mois consécutifs
Signal 2 : Change Failure Rate > 30% (incidents fréquents en prod)
Signal 3 : Throughput Innovation en baisse malgré effectifs stables
Signal 4 : Cycle time en hausse (la dette ralentit tous les flux)

≥ 3 signaux → 🚨 DEBT SPIRAL PROBABLE
2 signaux   → ⚠️ RISQUE DE DETTE CROISSANTE
≤ 1 signal  → 🟢 DETTE SOUS CONTRÔLE
```

## Verdict et 1 décision

| Verdict | Décision |
|---------|---------|
| 🟢 ÉQUILIBRE SAIN | "Maintenir l'allocation — réévaluer dans 6 mois" |
| ⚠️ DÉSÉQUILIBRE MODÉRÉ | "Objectif de réduction dette de Xpts sur 2 trimestres — dans le roadmap comme non-négociable" |
| 🚨 DETTE DOMINANTE | "Stop/go sur features non critiques — allouer X% à la dette pendant N sprints" |
| 🔥 DEBT SPIRAL | "Décision urgente : stabiliser avant d'améliorer — diagnostiquer la cause racine en priorité absolue" |

## Coût de la dette en capacité

Calculer ce qu'on livrerait si Maintenance revenait au benchmark du stade :
`Gain = (Maintenance_actuelle - Maintenance_benchmark) × throughput_total`
Exprimer en "X features supplémentaires par mois".
