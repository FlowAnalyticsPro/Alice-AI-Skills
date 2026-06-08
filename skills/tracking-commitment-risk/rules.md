# Règles — Tracking Commitment Risk

## Niveaux de risque par item

### 🔴 CRITIQUE — Action immédiate
Au moins une condition :
- Due date déjà dépassée
- Bloqué depuis > 5 jours
- Aging > P85 × 1.5
- Bloqué ET en retard simultanément

### 🟠 ÉLEVÉ — Action aujourd'hui
Au moins une condition :
- Due date dans ≤ 3 jours, avancement insuffisant
- Bloqué depuis 2 à 5 jours
- Aging entre P85 et P85 × 1.5
- Positionné dans l'étape identifiée comme goulot principal

### 🟡 MODÉRÉ — À surveiller
- Due date dans ≤ 5 jours sans blocage actif
- Aging entre P50 et P85
- Étape secondaire avec temps médian élevé

## Alerte systémique (goulot)

Si `FAP:get_step_analysis` identifie une étape avec bottleneckScore élevé ET plusieurs items en attente → signaler en section séparée. L'action porte sur le process, pas sur les items individuels.
