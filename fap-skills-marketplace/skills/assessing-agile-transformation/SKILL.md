---
name: assessing-agile-transformation
description: Évalue l'avancement de la transformation agile en croisant scores d'assessment par domaine, tendances de progression et métriques Flow réelles pour détecter les knowing-doing gaps. À utiliser par un Engineering Manager pour un bilan de transformation, une réunion avec un coach agile, ou pour justifier l'investissement en accompagnement.
---

# Assessing Agile Transformation (Manager)

Répond à : "Où en est notre transformation agile ?"

## Workflow

```
- [ ] Étape 1 : Périmètre + référentiels (FAP:get_programs + FAP:get_competency_frameworks)
- [ ] Étape 2 : Scores actuels par équipe (FAP:get_assessments)
- [ ] Étape 3 : Évolution dans le temps (FAP:get_assessment_trends × N équipes)
- [ ] Étape 4 : Comparaison cross-équipes (FAP:get_assessment_compare)
- [ ] Étape 5 : Tâches d'amélioration (FAP:get_assessment_tasks)
- [ ] Étape 6 : Métriques Flow pour corrélation (FAP:compare_projects)
- [ ] Étape 7 : Calculer Knowing-Doing Gap → recommandations
```

## Appels MCP

**Étape 2** — `FAP:get_assessments` `{ programId }` → scores par domaine, date dernière mesure

**Étape 3** — `FAP:get_assessment_trends` `{ assessmentId }` par équipe → progression mesure par mesure

**Étape 4** — `FAP:get_assessment_compare` `{ assessmentIds: [...] }` → comparaison cross-équipes par domaine

**Étape 5** — `FAP:get_assessment_tasks` `{ programId }` → TODO / IN_PROGRESS / DONE

**Étape 6** — `FAP:compare_projects` `{ projectIds: [...] }` → métriques Flow pour croiser avec assessment

## Knowing-Doing Gap

```
KDG = Score_assessment - Score_flow_normalisé
KDG > 25 pts → ⚠️ Gap significatif (pratiques connues, non appliquées)
KDG 10-25    → 🟡 Gap modéré (normal en phase d'apprentissage)
KDG < 10     → 🟢 Alignement sain
```

Voir [rules.md](rules.md) pour la vitesse de progression par domaine et les 5 profils d'équipe.

## Format de sortie

Voir [output.md](output.md).

## Pré-requis

Au moins **2 mesures d'assessment** par équipe pour calculer une tendance. Avec 1 seule mesure, signaler que seul le niveau actuel est disponible.
