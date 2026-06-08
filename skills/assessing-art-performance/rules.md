# Règles — Assessing ART Performance

## Calcul des scores composants (0-100 chacun)

```
score_cycleTime      = (cycleTime_équipe / médiane_ART) × 50  [plafonné à 100]
score_throughput     = (1 - throughput_équipe / max_ART) × 100
score_predictability = (100 - predictability_%) [Scrum] OU variability_% [Kanban]
score_blocages       = min(100, count_bloqués × durée_moyenne × 5)
score_dueDates       = % items en retard × 100
```

## Classification

| Niveau | Score | Message |
|--------|-------|---------|
| 🟢 Performante | 0-25 | Flow sain, au-dessus de la médiane ART |
| 🟡 En tension | 25-50 | 1-2 dimensions à surveiller |
| 🟠 En difficulté | 50-75 | 3+ dimensions dégradées |
| 🔴 En crise | 75-100 | Intervention urgente |

## Dimension dominante par équipe

Identifier la dimension avec le score composant le plus élevé → c'est le point d'entrée de l'intervention RTE.

| Dimension dominante | Action RTE typique |
|--------------------|-------------------|
| Cycle time | Impediment workshop avec l'équipe |
| Throughput | Vérifier WIP et dépendances externes |
| Predictability | Revoir définition du ready/done |
| Blocages | Escalade des dépendances inter-équipes |
| Due dates | Réviser scope PI ou milestones |
