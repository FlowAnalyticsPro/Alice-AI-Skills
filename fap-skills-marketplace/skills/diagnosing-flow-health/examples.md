# Exemples — Diagnosing Flow Health

## Exemple : Flow sous tension

**SM :** "C'est quoi l'état de santé de notre flow cette semaine ?"

Données : WIP = 12 (limite 10), 25% items > P85, efficiency = 28%, 1 bloqué 3j, throughput stable

**Réponse :**

## Flow Health — Projet Core — 17 mai

Verdict : ⚠️ SOUS TENSION

| Dimension | Score | Indicateur clé |
|-----------|-------|----------------|
| WIP | 🔴 | 12 items (limite : 10 — dépassée) |
| Aging | 🟡 | 25% items dépassent le P85 (12 jours) |
| Efficience | 🟡 | 28% temps actif (72% d'attente) |
| Blocages | 🟡 | 1 bloqué depuis 3 jours |
| Throughput | 🟢 | 5 items/sem — stable |

Point positif : Le throughput reste stable malgré la tension — l'équipe continue de livrer.
Problème principal : Le WIP dépasse la limite. Chaque item ajouté dégrade mécaniquement le cycle time de tous les autres.
Tendance : Cycle time en légère hausse depuis 2 semaines (+1.5j) — signal précoce à traiter maintenant.

Action prioritaire : → Bloquer tout nouvel item entrant jusqu'à ce que le WIP repasse sous 10 — finir avant de commencer.
