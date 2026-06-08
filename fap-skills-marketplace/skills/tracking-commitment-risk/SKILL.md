---
name: tracking-commitment-risk
description: Identifie et priorise les items en cours qui menacent les engagements de livraison actifs, en croisant retard sur due date, aging excessif, blocages et position dans un goulot. À utiliser en standup quotidien, avant une démo, ou quand un Product Owner veut savoir ce qui risque de faire dérailler son sprint ou sa release.
---

# Tracking Commitment Risk (PO)

Répond à : "Quels items risquent de faire dérailler mes engagements ?"

## Workflow

```
- [ ] Étape 1 : Identifier le projet (FAP:get_portfolio)
- [ ] Étape 2 : Items en retard ou à risque sur due date (FAP:get_due_date_analysis)
- [ ] Étape 3 : Items bloqués (FAP:get_blocked_tickets)
- [ ] Étape 4 : Items en aging excessif (FAP:get_issues + FAP:get_flow_metrics pour P85)
- [ ] Étape 5 : Goulot actif (FAP:get_step_analysis)
- [ ] Étape 6 : Classer par niveau → produire le radar
```

## Appels MCP

**Étape 1** — `FAP:get_portfolio` → `projectId`

**Étape 2** — `FAP:get_due_date_analysis` `{ projectId }` → items late, items at risk

**Étape 3** — `FAP:get_blocked_tickets` `{ projectId }` → bloqués + durée

**Étape 4** — `FAP:get_flow_metrics` `{ projectId, period: "THREE_MONTHS" }` → P85 comme seuil d'aging
puis `FAP:get_issues` `{ projectId, status: "IN_PROGRESS", orderBy: "aging", order: "DESC" }` → items > P85

**Étape 5** — `FAP:get_step_analysis` `{ projectId }` → étape saturée (risque systémique)

## Niveaux de risque

Voir [rules.md](rules.md) pour les seuils CRITIQUE / ÉLEVÉ / MODÉRÉ.

## Format de sortie

Voir [output.md](output.md) — format "radar" par niveau de risque.

## Exemples

Voir [examples.md](examples.md).

## Boucle de validation

Si aucun item n'est identifié à risque après les 5 étapes → répondre explicitement "Aucun item à risque détecté" et féliciter l'équipe. Ne pas inventer de risques.
