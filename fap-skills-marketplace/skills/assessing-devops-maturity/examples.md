# Exemples — Assessing DevOps Maturity

## Exemple : 2 équipes, niveaux différents

**RTE :** "Où en sont mes équipes sur DORA ?"

Données Squad A : DeployFreq=Elite, LeadTime=High, TimeToRestore=High, CFR=Medium → Score 82
Données Squad B : DeployFreq=Medium, LeadTime=Medium, TimeToRestore=Low, CFR=High → Score 52

**Réponse :**

## Maturité DevOps — ART Phoenix — 3 derniers mois

| Équipe | Deploy Freq | Lead Time | Time to Restore | CFR | Score | Niveau |
|--------|------------|-----------|-----------------|-----|-------|--------|
| Squad A | 🏆 Elite | 🥇 High | 🥇 High | 🥈 Medium | 82 | 🥇 High |
| Squad B | 🥈 Medium | 🥈 Medium | 🥉 Low | 🥇 High | 52 | 🥈 Medium |

**Squad A — 🥇 High (82/100)**
Point fort : Deployment Frequency Elite — déploie plusieurs fois par jour.
Métrique bride : Change Failure Rate Medium (32% d'échecs).
Tendance : CFR en amélioration depuis 6 semaines (38% → 32%).
→ Action : Renforcer les tests de régression automatisés — objectif CFR < 30% (niveau High) d'ici 2 sprints.

**Squad B — 🥈 Medium (52/100)**
Point fort : Change Failure Rate High — déploiements fiables quand ils ont lieu.
Métrique bride : Time to Restore Low (> 1 semaine en moyenne).
Tendance : Stable depuis 3 mois — pas de progression.
→ Action : Créer des runbooks pour les 3 incidents les plus fréquents. Organiser un premier game day ce sprint.

Recommandation ART : Squad A est sur la bonne trajectoire. Concentrer l'investissement coaching sur Squad B, priorité Time to Restore — c'est le levier avec le plus grand impact sur la fiabilité perçue par les utilisateurs.
