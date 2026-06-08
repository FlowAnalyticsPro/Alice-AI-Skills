---
name: measuring-team-improvement
description: Mesure si les équipes engineering s'améliorent sur les 3 dimensions fondamentales — maturité agile (Assessment), maturité DevOps (DORA) et performance de delivery (Flow) — et calcule un Score d'Amélioration Organisationnelle global. À utiliser par un CEO ou CPO pour un bilan annuel, une revue stratégique RH, ou pour répondre à "est-ce que notre investissement en transformation engineering paie ?".
---

# Measuring Team Improvement (CEO/CPO)

Répond à : "Nos équipes s'améliorent-elles ?"

## Workflow

```
- [ ] Étape 1 : Cartographier (FAP:get_programs)
- [ ] Étape 2 : Progression maturité agile (FAP:get_assessment_trends + FAP:get_assessment_compare)
- [ ] Étape 3 : Progression maturité DevOps (FAP:get_dora_views + FAP:get_dora_trends × 2 métriques)
- [ ] Étape 4 : Progression performance delivery (FAP:get_flow_trends × tous projets)
- [ ] Étape 5 : Vue cross-équipes (FAP:compare_projects)
- [ ] Étape 6 : Calculer Score Amélioration → verdict + ROI + 1 décision
```

## Appels MCP

**Granularité : MENSUELLE — Horizon minimum : 6 mois**

**Étape 2** — `FAP:get_assessment_trends` `{ assessmentId }` + `FAP:get_assessment_compare` `{ assessmentIds: [...] }` → progression par équipe et domaine

**Étape 3** — `FAP:get_dora_trends` `{ viewId, metric: "deploymentFrequency" }` + `"leadTimeForChanges"` → métriques DORA prioritaires

**Étape 4** — `FAP:get_flow_trends` `{ projectId, metric: "cycleTime", granularity: "MONTHLY" }` + `metric: "throughput"` → tendance mensuelle

## Score d'Amélioration par dimension

```
Score_agile    = (variation_assessment_pts/mois / 5) × 100   [5pts/mois = max]
Score_devops   = (niveau_DORA_fin - niveau_DORA_début) / 3 × 100
Score_delivery = moyenne(variation_cycleTime, variation_throughput)

Score_global = Score_agile × 0.35 + Score_devops × 0.30 + Score_delivery × 0.35
```

Voir [rules.md](rules.md) pour la classification et les 5 profils d'équipe.

## Format de sortie

Voir [output.md](output.md) — score global + ROI en langage business + 1 décision.

## Règles CEO

- Maximum 5 chiffres
- Traduire en "l'organisation livre X jours de moins / X% de volume en plus"
- 1 seule décision — pas une liste d'actions
- Mentionner l'équipe la plus en progrès comme signal positif
