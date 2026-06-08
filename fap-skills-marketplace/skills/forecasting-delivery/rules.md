# Règles d'interprétation — Delivery Forecast

## Contenu
- Règles OUI (confiance élevée)
- Règles RISQUE MODÉRÉ (confiance partielle)
- Règles NON (confiance faible)
- Règles spéciales (données insuffisantes, équipes Scrum)

---

## ✅ OUI — Confiance élevée

Toutes les conditions suivantes réunies :
- Date cible ≥ date P85 retournée par `FAP:get_forecast`
- Aucun ticket bloqué depuis plus de **3 jours**
- Aucun item en retard dans `FAP:get_due_date_analysis`
- Variabilité du cycle time ≤ **30%**

Formulation : "La livraison est très probable avant le [date]. Les données ne montrent aucun signal de risque significatif."

---

## ⚠️ RISQUE MODÉRÉ — Confiance partielle

Au moins une condition à risque :
- Date cible entre P50 et P85 de `FAP:get_forecast`
- 1 à 2 tickets bloqués depuis 2 à 5 jours
- 1 à 2 items en retard sur leur due date
- Variabilité entre **30% et 50%**

Formulation : "La livraison est possible mais incertaine. [Nommer le signal de risque principal] représente le principal facteur d'incertitude."

---

## ❌ NON — Confiance faible

Au moins une condition critique :
- Date cible < date P50 de `FAP:get_forecast`
- ≥ 3 tickets bloqués
- Plusieurs items en retard sur leur due date
- Variabilité > **50%** (équipe très imprévisible)

Formulation : "La livraison dans les délais est peu probable. Au rythme actuel, la date P85 est le [date] — soit [N] jours après la date cible."

---

## Règles spéciales

### Données insuffisantes (< 30 items livrés)
→ Ajouter l'avertissement : "Note : l'équipe a livré moins de 30 items sur la période. Le P85 est indicatif mais pas statistiquement robuste."
→ Maintenir le verdict mais le qualifier de "prévision faible fiabilité".

### Projet Scrum
→ Exprimer la prévision en sprints si le PO le demande : "Au rythme actuel de X points/sprint, le scope restant de Y points sera couvert en [N] sprints."
→ Combiner avec `FAP:get_sprint_metrics` si la variabilité est élevée pour diagnostiquer l'imprévisibilité.

### Plusieurs items en scope
→ `FAP:get_forecast` retourne une prévision pour le backlog restant.
→ Si le PO demande une date pour un item spécifique, utiliser le cycle time P85 comme SLA proxy : "85% des items similaires sont livrés en moins de X jours."
