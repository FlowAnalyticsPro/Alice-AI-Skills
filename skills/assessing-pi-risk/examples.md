# Exemples — Assessing PI Risk

## Exemple : PI semaine 7, 1 équipe OFF TRACK

**RTE :** "On est en semaine 7 — le PI va tenir ?"  (fin PI = 20 juin)

Données : Équipe A P85 = 15 juin (+5j) → AT RISK | Équipe B P85 = 2 juillet (-12j) → OFF TRACK | Équipe C P85 = 18 juin (+2j) → AT RISK | Équipe D P85 = 28 mai (+23j) → ON TRACK | 3 tickets bloqués A→B depuis 7j

**Réponse :**

## PI Risk Assessment — ART Phoenix — Semaine 7/10

Verdict PI : ⚠️ AT RISK

| Équipe | P85 forecast | Fin PI | Écart | Statut |
|--------|-------------|--------|-------|--------|
| Squad Alpha | 15 juin | 20 juin | +5j | 🟡 AT RISK |
| Squad Beta | 2 juillet | 20 juin | -12j | 🔴 OFF TRACK |
| Squad Gamma | 18 juin | 20 juin | +2j | 🟡 AT RISK |
| Squad Delta | 28 mai | 20 juin | +23j | 🟢 ON TRACK |

Dépendances critiques :
🔴 CRITIQUE — Squad Alpha → Squad Beta : 3 tickets bloqués depuis 7 jours. Si non résolu sous 48h, Alpha bascule OFF TRACK.

Tendance ART : sem-3 18 items | sem-2 16 items | sem-1 14 items → ↘ Décélération — signal aggravant.

Actions critiques — 48h :
1. Dependency workshop Alpha/Beta — Qui : RTE — Conséquence : Alpha bascule OFF TRACK, 2 PI Objectives à risque
2. Plan de scope réduit pour Beta — Qui : RTE + PO Beta — Conséquence : sans priorisation, aucun item ne sera livré avant fin PI
