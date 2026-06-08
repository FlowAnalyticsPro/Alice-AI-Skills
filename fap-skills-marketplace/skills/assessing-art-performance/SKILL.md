---
name: assessing-art-performance
description: Compare les équipes d'un Agile Release Train sur throughput, cycle time, prédictabilité, blocages et retards de due dates, puis produit un classement par Score de Difficulté. À utiliser par un RTE avant un PI Planning, un ART Sync, ou quand il doit identifier quelles équipes nécessitent son attention en priorité.
---

# Assessing ART Performance (RTE)

Répond à : "Quelles équipes de l'ART sont en difficulté ?"

## Workflow

```
- [ ] Étape 1 : Identifier l'ART et ses équipes (FAP:get_programs)
- [ ] Étape 2 : Comparaison cross-équipes (FAP:compare_projects)
- [ ] Étape 3 : Blocages par équipe en difficulté (FAP:get_blocked_tickets)
- [ ] Étape 4 : Due dates par équipe (FAP:get_due_date_analysis)
- [ ] Étape 5 : Sprint metrics équipes Scrum (FAP:get_sprint_metrics)
- [ ] Étape 6 : Assessments si disponibles (FAP:get_assessments)
- [ ] Étape 7 : Calculer Score de Difficulté → classer les équipes
```

## Appels MCP

**Étape 1** — `FAP:get_programs` `{}` → programId, liste des projectIds membres

**Étape 2** — `FAP:compare_projects` `{ projectIds: [...] }` → cycleTime, throughput, variability par équipe (appel unique, toutes équipes)

**Étapes 3-4-5** — Appeler pour chaque équipe identifiée à risque uniquement (pas toutes)

**Étape 6** — `FAP:get_assessments` `{ programId }` → scores de maturité (si configuré)

## Score de Difficulté

```
Score = score_cycleTime × 0.25 + score_throughput × 0.25
      + score_predictability × 0.20 + score_blocages × 0.20
      + score_dueDates × 0.10
```

Voir [rules.md](rules.md) pour le calcul de chaque score composant et la classification.

## Format de sortie

Voir [output.md](output.md).

## Exemples

Voir [examples.md](examples.md).

## Règle clé

`FAP:compare_projects` est l'appel pivot — il couvre toutes les équipes en un seul appel. Ne détailler par équipe (étapes 3-5) que pour celles classées 🟠 ou 🔴.
