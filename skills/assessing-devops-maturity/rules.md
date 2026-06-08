# Règles — Assessing DevOps Maturity

## Niveaux DORA par métrique

| Métrique | Elite | High | Medium | Low |
|----------|-------|------|--------|-----|
| Deployment Frequency | Plusieurs/jour | Quotidien-hebdo | Hebdo-mensuel | < mensuel |
| Lead Time for Changes | < 1 heure | 1j-1sem | 1sem-1mois | 1-6 mois |
| Time to Restore | < 1 heure | < 1 jour | < 1 semaine | > 1 semaine |
| Change Failure Rate | 0-15% | 16-30% | 31-45% | > 45% |

## Score global → Niveau

| Score normalisé | Niveau |
|-----------------|--------|
| 85-100 | 🏆 Elite |
| 65-84 | 🥇 High |
| 40-64 | 🥈 Medium |
| 0-39 | 🥉 Low |

## Actions par métrique bride

| Métrique bride | Levier prioritaire |
|----------------|-------------------|
| Deployment Frequency | Automatiser le pipeline CI/CD, trunk-based development |
| Lead Time for Changes | Feature flags, revues de code < 24h, shift-left testing |
| Time to Restore | Monitoring proactif, runbooks, game days |
| Change Failure Rate | Tests automatisés, déploiements progressifs (canary/blue-green) |
