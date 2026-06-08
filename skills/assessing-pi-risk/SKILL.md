---
name: assessing-pi-risk
description: Évalue le risque d'atteinte des objectifs du Program Increment en cours en croisant les prévisions de livraison de chaque équipe, les blocages inter-équipes et la tendance du throughput ART. À utiliser par un RTE en ART Sync bi-hebdomadaire, avant un System Demo, ou quand il doit savoir si le PI est on track.
---

# Assessing PI Risk (RTE)

Répond à : "Le PI va-t-il tenir ses objectifs ?"

## Workflow

```
- [ ] Étape 1 : Identifier l'ART (FAP:get_programs)
- [ ] Étape 2 : Prévision de livraison par équipe (FAP:get_forecast × N équipes)
- [ ] Étape 3 : Items à risque sur due dates (FAP:get_due_date_analysis × N équipes)
- [ ] Étape 4 : Blocages inter-équipes (FAP:get_blocked_tickets × N équipes)
- [ ] Étape 5 : Comparaison trajectoire (FAP:compare_projects)
- [ ] Étape 6 : Tendance throughput équipes à risque (FAP:get_flow_trends)
- [ ] Étape 7 : Calculer écarts P85 vs fin PI → verdict
```

## Appels MCP

**Étape 2** — `FAP:get_forecast` `{ projectId }` pour chaque équipe → date P85 à comparer à la date de fin PI

**Étape 4** — `FAP:get_blocked_tickets` → repérer les blocages impliquant une autre équipe de l'ART

**Étape 5** — `FAP:get_compare_projects` `{ projectIds: [...] }` → vue cross-équipes

**Étape 6** — `FAP:get_flow_trends` `{ projectId, metric: "throughput", granularity: "WEEKLY" }` → équipes qui accélèrent ou décrochent

## Calcul du risque scope

```
Écart = Date_fin_PI - Date_P85_équipe (jours)
> 10j  → 🟢 ON TRACK
0-10j  → 🟡 AT RISK
< 0j   → 🔴 OFF TRACK
```

Voir [rules.md](rules.md) pour les niveaux de risque dépendances et le verdict global PI.

## Format de sortie

Voir [output.md](output.md).

## Paramètre obligatoire

Demander la **date de fin du PI** au RTE si elle n'est pas dans le contexte — sans elle, l'écart ne peut pas être calculé.
