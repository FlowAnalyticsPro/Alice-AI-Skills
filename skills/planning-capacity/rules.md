# Règles — Planning Capacity

## Buffers de sécurité

| Condition | Buffer à appliquer |
|-----------|-------------------|
| Scrum predictability < 70% | -20% de la capacité nette |
| Kanban variability > 30% | -15% de la capacité nette |
| ≥ 2 items bloqués | Déduire explicitement leur équivalent en points/items |
| Étape saturée détectée | Signaler que la capacité est contrainte par le goulot |

## Scrum — Calcul

```
Capacité brute     = velocity.P50
Charge en cours    = somme points items IN_PROGRESS non terminés
Charge bloquée     = somme points items bloqués
Capacité nette     = brute - en_cours - bloquée
Recommandation     = nette × buffer_predictability (arrondi inférieur)
```

## Kanban — Calcul

```
Durée cycle cible  = précisée par PO ou déduite du contexte (en semaines)
Capacité brute     = throughput.P50 × durée_cycle
WIP actuel         = count items IN_PROGRESS
Items bloqués      = count items bloqués
Capacité nette     = brute - WIP_actuel - bloqués
Recommandation     = nette × buffer_variability (arrondi inférieur)
```

## Niveaux de confiance

| Recommandation | Niveau | Message |
|---------------|--------|---------|
| Résultat > 0, aucun goulot | 🟢 Sain | Engager jusqu'à la recommandation |
| Résultat > 0, goulot détecté | 🟡 Contrainte | Engager à 80% — résoudre le goulot d'abord |
| Résultat ≤ 0 | 🔴 Saturé | Ne pas ajouter — terminer avant de commencer |
