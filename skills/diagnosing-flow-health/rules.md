# Règles — Diagnosing Flow Health

## Scoring par dimension

| Dimension | 🟢 Sain | 🟡 Attention | 🔴 Critique |
|-----------|---------|------------|------------|
| WIP | ≤ limite ET distribution équilibrée | 80-100% limite OU 1 étape > 40% | > limite OU 1 étape > 60% |
| Aging | < 10% items > P85 | 10-30% items > P85 | > 30% items > P85 |
| Efficience | ≥ 40% | 20-40% | < 20% |
| Blocages | 0 bloqué OU durée moy < 2j | 1-2 bloqués, durée 2-5j | ≥ 3 bloqués OU durée moy > 5j |
| Throughput | Stable ou ↗ sur 4 semaines | Baisse légère < -20% | Baisse > -20% OU zéro 1+ semaine |

## Verdict global

| Verdict | Conditions |
|---------|-----------|
| ✅ FLOW SAIN | 0 CRITIQUE, ≤ 1 ATTENTION |
| ⚠️ SOUS TENSION | 0 CRITIQUE, ≥ 2 ATTENTION |
| 🚨 DÉGRADÉ | 1 dimension CRITIQUE |
| 🔥 EN CRISE | ≥ 2 dimensions CRITIQUES |
