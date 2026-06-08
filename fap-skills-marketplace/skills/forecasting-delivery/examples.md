# Exemples — Delivery Forecast

## Exemple 1 : Verdict OUI

**PO :** "On a promis au client la feature de login SSO pour le 15 juin. On est réalistes ?"

**Appels effectués :**
- `FAP:get_forecast` → P50 : 8 juin / P85 : 12 juin
- `FAP:get_flow_metrics` → cycleTime P50 : 7j, P85 : 11j, variabilité : 22%
- `FAP:get_due_date_analysis` → 0 items en retard
- `FAP:get_blocked_tickets` → 0 tickets bloqués

**Réponse :**

## Prévision de livraison — Projet Core

**Verdict : OUI ✅**

### Données
- Prévision P85 : livraison quasi-certaine avant le **12 juin** (3 jours avant la deadline)
- Cycle time médian : 7 jours (P85 : 11 jours)
- Variabilité : 22% → équipe prévisible
- Tickets bloqués : 0 / Items en retard : 0

### Analyse
L'équipe livre 85% de ses items en moins de 11 jours, avec une bonne régularité. Aucun signal de risque actif. La date du 15 juin laisse une marge de 3 jours sur le scénario conservateur.

### Action recommandée
→ Confirmer l'engagement au client — la date est tenue avec une confiance élevée.

---

## Exemple 2 : Verdict RISQUE MODÉRÉ

**PO :** "J'ai une démo Airbus vendredi dans 9 jours. On peut compter dessus ?"

**Appels effectués :**
- `FAP:get_forecast` → P50 : 7 jours / P85 : 13 jours
- `FAP:get_flow_metrics` → variabilité : 38%
- `FAP:get_due_date_analysis` → 1 item en retard (2 jours)
- `FAP:get_blocked_tickets` → 2 tickets bloqués depuis 4 jours

**Réponse :**

## Prévision de livraison — Projet Core

**Verdict : RISQUE MODÉRÉ ⚠️**

### Données
- Prévision P50 : dans **7 jours** (avant la démo) / P85 : dans 13 jours (après)
- Variabilité : 38% → équipe peu prévisible en ce moment
- Tickets bloqués : 2 depuis 4 jours en moyenne
- Items en retard : 1

### Analyse
La livraison avant vendredi est probable (scénario médian) mais pas garantie — le scénario à 85% de confiance dépasse la date de la démo. Deux tickets bloqués depuis 4 jours représentent le principal risque : s'ils ne débloqueront pas dans 48h, le scénario médian devient compromis.

### Action recommandée
→ Débloquer WPM-34 et WPM-41 aujourd'hui — c'est le seul levier pour sécuriser la démo vendredi.

---

## Exemple 3 : Verdict NON

**PO :** "Le management veut qu'on livre les 8 stories restantes d'ici la semaine prochaine. C'est faisable ?"

**Appels effectués :**
- `FAP:get_forecast` → P50 : 18 jours / P85 : 26 jours
- `FAP:get_flow_metrics` → variabilité : 55%
- `FAP:get_due_date_analysis` → 4 items en retard
- `FAP:get_blocked_tickets` → 3 tickets bloqués depuis 7 jours

**Réponse :**

## Prévision de livraison — Projet Core

**Verdict : NON ❌**

### Données
- Prévision P50 : dans **18 jours** / P85 : dans 26 jours
- Demande management : dans 7 jours
- Variabilité : 55% → équipe très imprévisible
- Tickets bloqués : 3 depuis 7 jours / Items en retard : 4

### Analyse
Les 8 stories restantes ne peuvent pas être livrées en une semaine. Au rythme actuel, le scénario médian est à 18 jours — soit 11 jours au-delà de la deadline. Les 3 blocages actifs et les 4 items en retard aggravent encore la situation.

### Action recommandée
→ Proposer au management un scope réduit pour la semaine prochaine : identifier les 2-3 stories les plus critiques et négocier un livrable partiel plutôt qu'un engagement non tenu.
