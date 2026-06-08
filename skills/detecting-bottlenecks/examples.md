# Exemples — Detecting Bottlenecks

## Exemple : Goulot Review

**SM :** "Notre cycle time monte depuis 3 semaines — c'est quoi le problème ?"

Données : Review = 6j médian (moyenne autres étapes : 2j), 4 items en attente, 3 blocages sur 4 en Review

Score de Contrainte Review = (6/2)×0.5 + (4/10)×0.3 + (3/4)×0.2 = 1.5 + 0.12 + 0.15 = **1.77** (le plus élevé)

**Réponse :**

## Détection de goulots — Projet Core — 17 mai

Goulot principal : **Review**
Type : 🟠 CONJONCTUREL (apparu il y a 3 semaines)
Impact : 4 items ralentis

Pourquoi c'est le goulot :
- Temps médian : 6 jours (vs moyenne workflow 2j — soit 3× plus long)
- Items en attente : 4
- Blocages concentrés ici : 3 sur 4 (75% des blocages de l'équipe)

Hypothèse de cause : 75% des blocages en Review suggèrent une dépendance externe récurrente (validation PO ou équipe sécurité) plutôt qu'un manque de capacité interne.

Impact quantifié : si Review passait à 2j, le cycle time global baisserait de ~3j (-25%).

Tendance : Le temps médian en Review a doublé en 3 semaines — goulot en aggravation active.

Action prioritaire : → Organiser un daily de 10 min SM/PO pour traiter les validations Review en attente — tester 2 sprints et mesurer l'impact sur le cycle time.
