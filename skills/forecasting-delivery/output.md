# Template de sortie — Delivery Forecast

## Template standard

```
## Prévision de livraison — [Nom du projet]

**Verdict : [OUI ✅ / RISQUE MODÉRÉ ⚠️ / NON ❌]**

### Données
- Prévision P50 : livraison probable autour du [date]
- Prévision P85 : livraison quasi-certaine avant le [date]
- Cycle time médian : X jours (P85 : Y jours)
- Variabilité : X% → [prévisible / à surveiller / imprévisible]
- Tickets bloqués : N (depuis X jours en moyenne)
- Items en retard sur due date : N

### Analyse
[2-3 phrases maximum en langage métier. Expliquer POURQUOI le verdict 
est celui-là. Citer les chiffres clés. Pas de jargon technique.]

### Action recommandée
→ [1 action concrète, immédiate, avec le responsable si possible]
```

## Règles de rédaction

- Commencer TOUJOURS par le verdict en gras
- Maximum 3 phrases dans "Analyse" — pas de paragraphe long
- L'action recommandée est une phrase, pas une liste
- Traduire les dates en jours si plus parlant ("dans 12 jours" plutôt que "le 29 mai")
- Ne jamais écrire "il est possible que" — trancher avec le niveau de confiance approprié
