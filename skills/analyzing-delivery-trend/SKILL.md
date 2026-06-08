---
name: analyzing-delivery-trend
description: Mesure si l'organisation engineering livre plus vite et plus souvent qu'avant, sur 6 à 12 mois, en croisant l'évolution du cycle time, du throughput et de la fréquence de déploiement DORA. À utiliser par un CEO ou CPO pour un board meeting, un rapport trimestriel, ou pour répondre à "est-ce que nos équipes tech s'améliorent ?".
---

# Analyzing Delivery Trend (CEO/CPO)

Répond à : "Livrons-nous plus vite qu'avant ?"

## Workflow

```
- [ ] Étape 1 : Cartographier l'organisation (FAP:get_programs + FAP:get_portfolio)
- [ ] Étape 2 : Tendance cycle time 6-12 mois (FAP:get_flow_trends × tous projets)
- [ ] Étape 3 : Tendance throughput 6-12 mois (FAP:get_flow_trends × tous projets)
- [ ] Étape 4 : Tendance déploiement DORA (FAP:get_dora_views + FAP:get_dora_trends)
- [ ] Étape 5 : Niveau DORA actuel (FAP:get_dora_metrics)
- [ ] Étape 6 : Vue cross-équipes (FAP:compare_projects)
- [ ] Étape 7 : Calculer Score Vélocité → verdict + 1 décision
```

## Appels MCP

**Granularité obligatoire : MENSUELLE** — pas hebdomadaire pour ce niveau.

**Étape 2+3** — `FAP:get_flow_trends` `{ projectId, metric: "cycleTime", granularity: "MONTHLY" }` et `metric: "throughput"` — pour chaque projet sur 6-12 mois

**Étape 4** — `FAP:get_dora_views` puis `FAP:get_dora_trends` `{ viewId, metric: "deploymentFrequency" }` — granularité MONTHLY

**Étape 5** — `FAP:get_dora_metrics` `{ viewId }` → niveau Elite/High/Medium/Low actuel

## Score Vélocité Organisationnelle

```
Score = Variation_cycleTime × 0.40   (positif = on va plus vite)
      + Variation_throughput × 0.35  (positif = on livre plus)
      + Variation_deployFreq × 0.25  (positif = on déploie plus souvent)
```

Voir [rules.md](rules.md) pour le verdict et les 5 chiffres clés à produire.

## Format de sortie

Voir [output.md](output.md) — maximum 5 chiffres, 1 décision.

## Règles CEO

- Jamais plus de 5 chiffres dans la réponse
- Toujours traduire les métriques en langage business (pas de "P85" ni "variabilité")
- 1 seule décision stratégique — pas une liste d'actions
