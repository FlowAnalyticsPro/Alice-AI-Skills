---
name: assessing-devops-maturity
description: Évalue la maturité DevOps de chaque équipe d'un ART via les 4 métriques DORA, produit une matrice de niveaux Elite/High/Medium/Low et identifie la métrique "bride" de chaque équipe. À utiliser par un RTE pour un bilan de transformation DevOps, une revue avec le CTO, ou avant d'investir dans des pratiques CI/CD.
---

# Assessing DevOps Maturity (RTE)

Répond à : "Quelle est la maturité DevOps de mes équipes ?"

## Workflow

```
- [ ] Étape 1 : Identifier l'ART et ses DoraViews (FAP:get_programs + FAP:get_dora_views)
- [ ] Étape 2 : Métriques DORA par équipe (FAP:get_dora_metrics × N DoraViews)
- [ ] Étape 3 : Tendances par métrique (FAP:get_dora_trends × N × 4 métriques)
- [ ] Étape 4 : Assessments DevOps si disponibles (FAP:get_assessments)
- [ ] Étape 5 : Calculer Score Maturité → identifier métrique bride par équipe
```

## Appels MCP

**Étape 1** — `FAP:get_programs` puis `FAP:get_dora_views` `{}` → associer viewId ↔ équipe

**Étape 2** — `FAP:get_dora_metrics` `{ viewId }` pour chaque DoraView → niveaux Elite/High/Medium/Low des 4 métriques

**Étape 3** — `FAP:get_dora_trends` `{ viewId, metric: "deploymentFrequency" }` + `"leadTimeForChanges"` (2 métriques prioritaires)

**Étape 4** — `FAP:get_assessments` `{ programId }` → si référentiel DORA configuré

## Score de Maturité par équipe

```
Convertir niveaux : Elite=4, High=3, Medium=2, Low=1
Score = (deployFreq × 0.30) + (leadTime × 0.30) + (timeToRestore × 0.20) + (CFR × 0.20)
Score normalisé = (score / 4) × 100
```

**Métrique bride** = métrique avec le niveau le plus bas → levier d'amélioration prioritaire.

Voir [rules.md](rules.md) pour les niveaux DORA et les actions typiques par métrique bride.

## Format de sortie

Voir [output.md](output.md).

## Exemples

Voir [examples.md](examples.md).
