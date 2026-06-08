# Exemples — Assessing ART Performance

## Exemple : ART 4 équipes

**RTE :** "On a le PI Planning lundi — qui est en difficulté ?"

Données compare_projects : Équipe A cycleTime 18j (médiane 9j), throughput -40%, 5 blocages 8j moy → Score 76
Équipe B predictability 54%, 1 blocage 3j → Score 58
Équipe C dans la norme → Score 22
Équipe D au-dessus médiane → Score 14

**Réponse :**

## ART Performance — ART Phoenix — 17 mai — 4 équipes

| Rang | Équipe | Score | Niveau | Dimension critique |
|------|--------|-------|--------|--------------------|
| 1 | Squad Alpha | 76/100 | 🔴 En crise | Cycle time + Blocages |
| 2 | Squad Beta | 58/100 | 🟠 En difficulté | Predictability (54%) |
| 3 | Squad Gamma | 22/100 | 🟢 Performante | — |
| 4 | Squad Delta | 14/100 | 🟢 Performante | — |

Médiane ART : cycleTime 9j | throughput 5 items/sem

🔴 Squad Alpha — Score 76/100
Cycle time à 18j (2× la médiane ART) et 5 tickets bloqués depuis 8 jours en moyenne. 3 de ces blocages impliquent Squad Beta → risque de cascade PI. Aucun signal de problème de maturité agile.
→ Action RTE : Dependency workshop Alpha/Beta cette semaine. Escalader si non résolu sous 48h.

🟠 Squad Beta — Score 58/100
Predictability à 54% : 1 story sur 2 commitée ne sort pas du sprint. Commitment rate à 115% → sur-engagement systématique.
→ Action RTE : Demander à l'SM de revoir la vélocité de référence avant le PI Planning lundi.

Dépendances inter-équipes : ⚠️ Squad Alpha → Squad Beta : 3 tickets bloqués depuis 8 jours.
Points positifs : Squad Gamma et Delta au-dessus de la médiane sur toutes les dimensions.
