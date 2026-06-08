# Exemples — Measuring Delivery Capacity

## Exemple : Roadmap planning

**Manager :** "Le business veut 20 features en Q3 — est-ce réaliste ?"

Données : throughput 12 items/sem dont 5 features, 3 bugs, 2 TechDebt, 2 ops. Efficiency 22%. 3 bloqués. Tendance stable.

**Réponse :**

## Capacité de Delivery — Engineering — Avril-Juin 2025

Capacité brute consolidée : 12 items/semaine

🚀 Features  [████████] 5 items/sem (42%)
🐛 Bugs      [████]     3 items/sem (25%)
🔧 Tech Debt [███]      2 items/sem (17%)
⚙️ Ops       [██]       2 items/sem (16%)

→ Capacité nette business : **5 features/semaine ≈ 60 features sur 12 semaines de Q3**

Pertes identifiées :
| Source | Impact | % capacité |
|--------|--------|-----------|
| Temps d'attente (efficiency 22%) | ~3 items/sem | 25% |
| Items bloqués (3 tickets, 4j moy.) | ~1 item/sem | 8% |
| Total | ~4 items/sem | 33% |
→ Gain potentiel : +16 features/mois si efficience amenée à 35%

Projection Q3 : P50 ~58 features | P85 ~48 features

Décision recommandée : 20 features est atteignable (P50 = 60 sur 12 semaines), mais avec peu de marge. Tout imprévu — bug critique, scope creep — réduit ce chiffre. Recommander de s'engager sur 15 features et de présenter les 5 restantes comme "best effort".

Message : "La capacité nette en features est de 5 par semaine soit ~60 sur Q3. Un engagement sur 20 features est techniquement réaliste mais sans marge pour les imprévus. Recommandation : s'engager sur 15 et présenter 5 en best effort — ce qui protège la fiabilité vis-à-vis du business."
