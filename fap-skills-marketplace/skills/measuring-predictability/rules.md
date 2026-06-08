# Règles — Measuring Predictability

## Scoring

### Scrum
| Score | Predictability | Commitment Rate | Variabilité vélocité |
|-------|---------------|-----------------|---------------------|
| 🟢 Prévisible | ≥ 80% | 80-100% | ≤ 20% |
| 🟡 Instable | 60-80% | < 80% ou > 110% | 20-40% |
| 🔴 Imprévisible | < 60% | < 70% ou > 130% | > 40% |

> Commitment rate > 100% = sur-engagement systématique → signal négatif.

### Kanban
| Score | Ratio P85/P50 | Variabilité |
|-------|--------------|-------------|
| 🟢 Prévisible | ≤ 1.5 | ≤ 25% |
| 🟡 Instable | 1.5-2.5 | 25-50% |
| 🔴 Imprévisible | > 2.5 | > 50% |

## Diagnostic des causes

| Signaux | Cause probable | Levier |
|---------|---------------|--------|
| Commitment rate > 110% | Sur-engagement | Réviser la vélocité de référence en planning |
| Variabilité élevée + mix Bug/Story | Backlog hétérogène | Séparer SLA par type d'item |
| Throughput erratique + blocages récurrents | WIP incontrôlé | Implémenter/renforcer les limites WIP |
| P85/P50 > 2.5 + Spikes fréquents | Items trop larges | Découper les items > seuil de taille |
