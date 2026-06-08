# Exemples — Analyzing Innovation vs Debt

## Exemple : Stade croissance, déséquilibre modéré

**CEO :** "Pourquoi on livre si peu de nouvelles features malgré une équipe de 40 devs ?"

Données (stade Croissance) : Features 44%, Bugs 28%, TechDebt 18%, Ops 10%. Maintenance en hausse (+3%/mois depuis 4 mois). CFR 34%. Throughput Features stable malgré +20% d'effectifs.

**Réponse :**

## Innovation vs Dette — Engineering
Période : Nov 2024 → Avr 2025 — Stade : Croissance

Verdict : ⚠️ DÉSÉQUILIBRE MODÉRÉ
Debt Spiral : ⚠️ RISQUE (3 signaux sur 4 détectés)

🚀 Innovation  [████████████] 44%  (benchmark 55-65% : -11pts)
🐛 Maintenance [████████]     28%  (benchmark 10-15% : +13pts excess)
🔧 Dette tech  [█████]        18%  (benchmark 15-20% : ok)
⚙️ Opérations  [███]          10%  (ok)

Capital Innovation : 44% — Capital Maintenance (OpEx) : 38%
Écart vs benchmark : **-11pts d'innovation vs stade Croissance**

Tendance : Maintenance +3%/mois depuis 4 mois — la dette s'auto-alimente.
Signaux Debt Spiral : ✓ Maintenance en hausse ✓ CFR 34% (incidents fréquents) ✓ Throughput Features stable malgré +20% effectifs.

Coût de la dette : "Si Maintenance revenait à 15% (benchmark Croissance), +5 features supplémentaires par semaine — soit l'équivalent d'une équipe de 8 devs dédiés à l'innovation."

Une décision : → Allouer 25% de la capacité au remboursement de dette pendant 2 sprints, non-négociable dans le prochain roadmap — sans cela, chaque nouveau dev recruté produira autant de Bugs qu'il ne livre de Features.
