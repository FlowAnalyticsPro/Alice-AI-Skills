# Exemples — Planning Capacity

## Exemple 1 : Scrum — Recommandation saine

**PO :** "Sprint planning demain — on peut prendre combien ?"

Données : velocity P50 = 40pts, 12pts en cours, 0 bloqués, predictability = 78%

**Réponse :**

## Capacity Planning — Projet Core — Sprint 24

**Recommandation : 28 points (≈ 5-6 stories)**
Niveau de confiance : 🟢 Élevé

### Calcul
- Capacité brute : 40 points (vélocité médiane)
- Déductions : -12 points (en cours)
- Capacité nette : 28 points
- Buffer : aucun (predictability 78% > seuil 70%)
- **→ Recommandation : 28 points**

### Action recommandée
→ Engager jusqu'à 28 points — ne pas dépasser pour préserver la predictability.

---

## Exemple 2 : Kanban — WIP saturé

**PO :** "On peut ajouter 3 stories cette semaine ?"

Données : throughput P50 = 4 items/sem, WIP actuel = 9, limite WIP = 8, 2 bloqués

**Réponse :**

## Capacity Planning — Projet Beta — Cette semaine

**Recommandation : 0 items à ajouter**
Niveau de confiance : 🔴 Saturé

### Calcul
- Capacité brute : 4 items (throughput médian)
- WIP actuel : 9 (dépasse la limite de 8)
- Bloqués : 2 items de charge morte
- Capacité nette : **négative**

### Signal
⚠️ Le WIP dépasse la limite configurée. Ajouter des items dans ce contexte dégraderait le cycle time de tous les items en cours.

### Action recommandée
→ Débloquer les 2 items bloqués avant d'engager quoi que ce soit de nouveau — c'est la priorité absolue cette semaine.
