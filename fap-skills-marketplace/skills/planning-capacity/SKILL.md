---
name: planning-capacity
description: Calcule le nombre d'items qu'une équipe peut réellement absorber sur le prochain sprint ou cycle Kanban, en tenant compte du throughput historique, du WIP actuel et des blocages actifs. À utiliser quand un Product Owner prépare un sprint planning, veut calibrer ses engagements, ou se demande combien de stories son équipe peut prendre sans déraper.
---

# Planning Capacity (PO)

Répond à : "Combien d'items puis-je engager sur le prochain cycle ?"

## Workflow

```
- [ ] Étape 1 : Identifier le projet et son type (FAP:get_portfolio + FAP:get_project)
- [ ] Étape 2A (Scrum) : Vélocité historique (FAP:get_sprint_metrics)
- [ ] Étape 2B (Kanban) : Throughput historique (FAP:get_flow_metrics)
- [ ] Étape 3 : Items en cours (FAP:get_issues)
- [ ] Étape 4 : Blocages actifs (FAP:get_blocked_tickets)
- [ ] Étape 5 : Analyse par étape (FAP:get_step_analysis)
- [ ] Étape 6 : Calculer → produire la recommandation
```

## Appels MCP

**Étape 1** — `FAP:get_portfolio` puis `FAP:get_project` `{ projectId }`
> Détecter `boardType` (Scrum / Kanban) avant de bifurquer.

**Branche Scrum**
- `FAP:get_sprint_metrics` `{ projectId }` → velocity P50/P85, predictability, variability

**Branche Kanban**
- `FAP:get_flow_metrics` `{ projectId, period: "THREE_MONTHS" }` → throughput P50/P85, variability

**Étape 3** — `FAP:get_issues` `{ projectId, status: "IN_PROGRESS" }` → items déjà en cours (charge à déduire)

**Étape 4** — `FAP:get_blocked_tickets` `{ projectId }` → charge morte (WIP occupé sans throughput)

**Étape 5** — `FAP:get_step_analysis` `{ projectId }` → détecter une étape saturée qui contrainte la capacité

## Calcul rapide

**Scrum** : `velocity.P50 - points_en_cours - points_bloqués` → buffer si predictability < 70%

**Kanban** : `throughput.P50 × durée_cycle - WIP_actuel - items_bloqués` → buffer si variability > 30%

Voir [rules.md](rules.md) pour les buffers et seuils détaillés.

## Format de sortie

Voir [output.md](output.md) pour le template.

## Exemples

Voir [examples.md](examples.md).

## Boucle de validation

Après le calcul : vérifier que la recommandation ≤ capacité brute. Si le résultat est ≤ 0, ne pas recommander 0 — signaler que le WIP doit être réduit avant d'ajouter de nouveaux items (loi de Little).
