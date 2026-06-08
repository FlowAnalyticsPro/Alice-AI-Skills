# Règles — Detecting Bottlenecks

## Classification du goulot

### 🔴 STRUCTUREL
- Temps médian > 2× moyenne des autres étapes
- Présent depuis > 4 semaines
- Cause : capacité insuffisante, compétence rare, critère de sortie flou
- Levier : changement organisationnel (semaines à mois)

### 🟠 CONJONCTUREL
- Temps médian élevé mais récent (< 4 semaines) OU lié à un type d'item spécifique
- Cause : pic de charge, Bugs urgents, dépendance externe temporaire
- Levier : action tactique (1-2 semaines)

### 🟡 LATENT
- Accumulation d'items sans temps médian encore anormal
- Cause : limite WIP non respectée en amont qui pousse trop d'items
- Levier : préventif — agir maintenant

## Impact quantifié

Calculer l'amélioration potentielle si le goulot atteint le temps médian moyen :
`gain_cycle_time ≈ (temps_médian_goulot - temps_médian_moyen) × % items passant par cette étape`
