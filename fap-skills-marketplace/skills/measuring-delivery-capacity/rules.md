# Règles — Measuring Delivery Capacity

## Décisions selon les ratios

| Signal | Décision recommandée |
|--------|---------------------|
| Ratio Valeur < 40% | Décision stratégique sur la dette avant tout ajout de scope |
| Ratio Efficience < 20% | Recruter n'aidera pas — réduire les inefficiences d'abord |
| Tendance throughput ↘ | Investiguer avant de promettre sur le roadmap |
| Ratio Gel > 25% | Débloquer les items bloqués = gain immédiat sans recrutement |

## Calcul capacité perdue

```
Perte_attente  = Capacité_brute × (1 - efficiency)
Perte_bloquée  = items_bloqués × throughput_moyen_par_item
Perte_bugs     = max(0, Bugs_actuels - Bugs_seuil_sain)
Gain_potentiel = Perte_attente + Perte_bloquée + Perte_bugs
```

## Mapping types d'items → catégories

```
🚀 Innovation : Features, Stories, Epics, R&D
🔧 Dette tech  : Tech Debt, Refactoring, Migration, Architecture
🐛 Maintenance : Bugs, Hotfixes, Regressions
⚙️ Ops         : Tasks, Spikes, Support, Documentation
```
