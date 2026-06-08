# Règles — Assessing PI Risk

## Risque scope par équipe

| Score | Condition |
|-------|-----------|
| 🟢 ON TRACK | Écart > 10 jours |
| 🟡 AT RISK | Écart 0-10 jours |
| 🔴 OFF TRACK | Écart < 0 jours |

## Risque dépendances

| Niveau | Condition |
|--------|-----------|
| CRITIQUE | Bloqué > 5j ET implique autre équipe de l'ART OU sur chemin critique PI Objective |
| ÉLEVÉ | Bloqué 2-5j ET équipe externe à l'ART OU due date PI dans ≤ 2 semaines |

## Verdict global PI

| Verdict | Conditions |
|---------|-----------|
| ✅ ON TRACK | 0 OFF TRACK + 0 dépendance CRITIQUE + throughput ART stable/↗ |
| ⚠️ AT RISK | 1 OFF TRACK OU 1 dépendance CRITIQUE OU throughput ↘ |
| 🚨 OFF TRACK | ≥ 2 OFF TRACK OU ≥ 2 dépendances CRITIQUES |
| 🔥 PI COMPROMIS | Majorité équipes OFF TRACK OU dépendances en cascade |

## Actions critiques — règle des 48h

Produire exactement 2-3 actions maximum avec : qui / quoi / conséquence si non fait sous 48h.
