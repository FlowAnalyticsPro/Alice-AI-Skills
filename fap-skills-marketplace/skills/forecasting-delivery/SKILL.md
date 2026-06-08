---
name: forecasting-delivery
description: Prédit si une feature sera livrée avant une date cible en analysant le throughput historique, le cycle time, les items à risque et les blocages actifs de l'équipe dans FAP. À utiliser quand un Product Owner demande si un engagement de livraison est réaliste, veut connaître la date probable de livraison d'un item ou d'un scope, ou a besoin d'évaluer une promesse faite à un client ou au management.
---

# Forecasting Delivery (PO)

Répond à : "Cette feature sera-t-elle livrée pour la date X ?"

## Workflow

Copie cette checklist et coche au fur et à mesure :

```
- [ ] Étape 1 : Identifier le projet (FAP:get_portfolio)
- [ ] Étape 2 : Obtenir la prévision de livraison (FAP:get_forecast)
- [ ] Étape 3 : Contextualiser avec le cycle time (FAP:get_flow_metrics)
- [ ] Étape 4 : Identifier les items à risque (FAP:get_due_date_analysis)
- [ ] Étape 5 : Vérifier les blocages actifs (FAP:get_blocked_tickets)
- [ ] Étape 6 : Appliquer les règles → produire le verdict
```

## Appels MCP

**Étape 1** — `FAP:get_portfolio` → identifier le `projectId`

**Étape 2** — `FAP:get_forecast` `{ projectId }` → dates P50/P85/P95
> C'est le signal principal. Comparer P85 à la date cible du PO.

**Étape 3** — `FAP:get_flow_metrics` `{ projectId, period: "THREE_MONTHS" }` → cycleTime P50/P85, variability
> Une variabilité > 30% rend la prévision moins fiable — le signaler.

**Étape 4** — `FAP:get_due_date_analysis` `{ projectId }` → items en retard ou à risque
> Un item en retard consomme de la capacité sans produire de throughput.

**Étape 5** — `FAP:get_blocked_tickets` `{ projectId }` → tickets bloqués, durée
> Un blocage > 3 jours est un risque non visible dans le forecast.

## Règles de verdict

Voir [rules.md](rules.md) pour les seuils détaillés.

| Verdict | Condition principale |
|---------|---------------------|
| ✅ OUI | Date cible > P85 ET aucun blocage > 3j ET variabilité ≤ 30% |
| ⚠️ RISQUE MODÉRÉ | Date cible entre P50 et P85 OU 1-2 blocages OU variabilité 30-50% |
| ❌ NON | Date cible < P50 OU ≥ 3 blocages OU variabilité > 50% |

## Format de sortie

Voir [output.md](output.md) pour le template complet.

Structure : **Verdict** → Données clés → Analyse (2-3 phrases) → Action recommandée

## Exemples

Voir [examples.md](examples.md) pour des échanges PO complets.

## Boucle de validation

Après avoir produit le verdict :
1. Vérifier que chaque donnée citée provient bien d'un appel MCP effectué
2. Si une donnée manque → relancer l'appel correspondant avant de répondre
3. Ne jamais produire un verdict sans avoir complété les 5 étapes

## Limitations

- Moins de 30 items livrés sur la période → signaler explicitement que le P85 manque de base statistique
- Ne tient pas compte des congés ou événements non tracés dans FAP
