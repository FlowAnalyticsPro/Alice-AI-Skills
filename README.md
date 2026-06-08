# FAP Skills Marketplace

> **Skills MCP prêts à l'emploi pour Flow Analytics Pro**  
> Répondez aux vraies questions de vos équipes agiles — en langage naturel, avec vos données réelles.

---

## Qu'est-ce qu'une skill FAP ?

Une **skill** est un fichier `.md` qui orchestre votre serveur MCP FAP pour répondre à une question métier précise. Elle contient :

- Un **system prompt** qui dit au LLM comment raisonner
- Une **séquence d'appels MCP** vers vos 26 tools FAP
- Des **règles d'interprétation** pour transformer les données en verdict
- Un **format de sortie** standardisé et actionnable

```
Vous posez une question en langage naturel
         ↓
Le LLM lit la skill
         ↓
Il appelle les tools FAP dans l'ordre
         ↓
Il interprète les données selon les règles
         ↓
Il répond en langage métier — pas en métriques
```

**Vous n'avez pas besoin de connaître les 26 tools.** Vous choisissez votre rôle, posez votre question, obtenez une réponse.

---

## Prérequis

- **Flow Analytics Pro** avec le serveur MCP configuré (port 3030)
- Un client compatible MCP : Claude Desktop, Cursor, ou tout LLM supportant le protocole MCP
- Les modules FAP activés selon les skills choisies (Flow, DORA, Assessment)

---

## Les 15 skills — par persona

### 👤 Product Owner

| Skill | Question | Fréquence d'usage | Tools principaux |
|-------|----------|------------------|-----------------|
| [`delivery-forecast`](./skills/po/delivery-forecast.md) | Cette feature sera-t-elle livrée à temps ? | Avant chaque engagement | `get_forecast`, `get_flow_metrics` |
| [`capacity-planning`](./skills/po/capacity-planning.md) | Combien d'items puis-je engager sur le prochain cycle ? | Avant chaque sprint | `get_sprint_metrics`, `get_flow_metrics` |
| [`commitment-risk`](./skills/po/commitment-risk.md) | Quels items risquent de faire dérailler mes engagements ? | Quotidien / standup | `get_due_date_analysis`, `get_blocked_tickets` |

---

### 🔄 Scrum Master / Flow Master

| Skill | Question | Fréquence d'usage | Tools principaux |
|-------|----------|------------------|-----------------|
| [`flow-health`](./skills/sm/flow-health.md) | Notre flow est-il sain aujourd'hui ? | Hebdomadaire | `get_flow_metrics`, `get_step_analysis` |
| [`predictability`](./skills/sm/predictability.md) | L'équipe est-elle prévisible ? | Mensuel / par sprint | `get_sprint_metrics`, `get_flow_trends` |
| [`bottleneck-detection`](./skills/sm/bottleneck-detection.md) | Où sont les goulots dans notre workflow ? | Rétro / kaizen | `get_step_analysis`, `get_blocked_tickets` |

---

### 🚂 Release Train Engineer (SAFe)

| Skill | Question | Fréquence d'usage | Tools principaux |
|-------|----------|------------------|-----------------|
| [`art-performance`](./skills/rte/art-performance.md) | Quelles équipes de l'ART sont en difficulté ? | Hebdomadaire / ART Sync | `compare_projects`, `get_blocked_tickets` |
| [`pi-risk`](./skills/rte/pi-risk.md) | Le PI va-t-il tenir ses objectifs ? | Bi-hebdomadaire | `get_forecast`, `get_due_date_analysis` |
| [`devops-maturity`](./skills/rte/devops-maturity.md) | Quelle est la maturité DevOps de mes équipes ? | Mensuel | `get_dora_metrics`, `get_dora_trends` |

---

### 📊 Engineering Manager / Director

| Skill | Question | Fréquence d'usage | Tools principaux |
|-------|----------|------------------|-----------------|
| [`commitment-tracking`](./skills/manager/commitment-tracking.md) | Nos équipes tiennent-elles leurs engagements ? | Mensuel / trimestriel | `get_sprint_metrics`, `get_due_date_analysis` |
| [`agile-transformation`](./skills/manager/agile-transformation.md) | Où en est notre transformation agile ? | Trimestriel | `get_assessments`, `get_assessment_trends` |
| [`delivery-capacity`](./skills/manager/delivery-capacity.md) | Quelle est notre capacité réelle de delivery ? | Mensuel / roadmap | `get_dimension_metrics`, `compare_projects` |

---

### 🎯 CEO / CPO

| Skill | Question | Fréquence d'usage | Tools principaux |
|-------|----------|------------------|-----------------|
| [`delivery-trend`](./skills/ceo/delivery-trend.md) | Livrons-nous plus vite qu'avant ? | Trimestriel / QBR | `get_flow_trends`, `get_dora_trends` |
| [`innovation-vs-debt`](./skills/ceo/innovation-vs-debt.md) | Quelle part va à l'innovation vs la dette ? | Trimestriel / budget | `get_dimension_metrics`, `get_dora_metrics` |
| [`team-improvement`](./skills/ceo/team-improvement.md) | Nos équipes s'améliorent-elles ? | Semestriel / annuel | `get_assessment_trends`, `get_flow_trends`, `get_dora_trends` |

---

## Structure du repo

```
fap-skills-marketplace/
│
├── README.md                          ← ce fichier
│
├── skills/
│   ├── po/
│   │   ├── delivery-forecast.md
│   │   ├── capacity-planning.md
│   │   └── commitment-risk.md
│   │
│   ├── sm/
│   │   ├── flow-health.md
│   │   ├── predictability.md
│   │   └── bottleneck-detection.md
│   │
│   ├── rte/
│   │   ├── art-performance.md
│   │   ├── pi-risk.md
│   │   └── devops-maturity.md
│   │
│   ├── manager/
│   │   ├── commitment-tracking.md
│   │   ├── agile-transformation.md
│   │   └── delivery-capacity.md
│   │
│   └── ceo/
│       ├── delivery-trend.md
│       ├── innovation-vs-debt.md
│       └── team-improvement.md
│
└── docs/
    ├── how-skills-work.md             ← guide technique
    ├── mcp-tools-reference.md         ← référence des 26 tools
    └── faq.md                         ← questions fréquentes
```

---

## Comment utiliser une skill

### Option 1 — Claude Desktop (recommandé)

1. Configurez le serveur MCP FAP dans votre `claude_desktop_config.json`
2. Copiez le contenu du fichier skill souhaité
3. Collez-le comme **system prompt** dans votre conversation
4. Posez votre question en langage naturel

```json
{
  "mcpServers": {
    "fap": {
      "command": "node",
      "args": ["/path/to/fap-mcp-server/dist/index.js"],
      "env": {
        "FAP_API_KEY": "votre-clé-api",
        "FAP_API_URL": "https://votre-instance.flowanalyticspro.com"
      }
    }
  }
}
```

### Option 2 — Cursor

1. Ajoutez le serveur MCP FAP dans les settings Cursor
2. Ouvrez le fichier skill comme contexte
3. Posez votre question dans le chat

### Option 3 — Intégration dans votre propre interface

Chaque skill contient un **system prompt** prêt à l'emploi. Intégrez-le dans votre application via l'API Anthropic avec les tools MCP FAP activés.

---

## Couverture des 26 tools MCP FAP

Les 15 skills couvrent l'ensemble des tools disponibles :

### 📊 Portfolio & Projets
| Tool | Skills qui l'utilisent |
|------|----------------------|
| `get_portfolio` | delivery-forecast, capacity-planning, commitment-risk, flow-health, predictability, bottleneck-detection |
| `get_project` | capacity-planning, predictability |
| `get_programs` | art-performance, pi-risk, devops-maturity, commitment-tracking, agile-transformation, delivery-capacity, delivery-trend, innovation-vs-debt, team-improvement |
| `compare_projects` | art-performance, pi-risk, commitment-tracking, delivery-capacity, innovation-vs-debt, team-improvement |

### 🔄 Flow Metrics
| Tool | Skills qui l'utilisent |
|------|----------------------|
| `get_flow_metrics` | delivery-forecast, capacity-planning, flow-health, predictability, bottleneck-detection, commitment-tracking |
| `get_flow_trends` | flow-health, predictability, bottleneck-detection, pi-risk, delivery-capacity, delivery-trend, innovation-vs-debt, team-improvement |
| `get_issues` | commitment-risk, flow-health, capacity-planning |
| `get_sprint_metrics` | capacity-planning, predictability, art-performance, commitment-tracking |
| `get_step_analysis` | flow-health, bottleneck-detection, capacity-planning |
| `get_blocked_tickets` | delivery-forecast, commitment-risk, flow-health, art-performance, pi-risk, delivery-capacity |
| `get_dimension_metrics` | bottleneck-detection, predictability, delivery-capacity, innovation-vs-debt |
| `get_due_date_analysis` | delivery-forecast, commitment-risk, art-performance, pi-risk, commitment-tracking |
| `get_forecast` | delivery-forecast, capacity-planning (Scrum), pi-risk, commitment-tracking, delivery-capacity |
| `get_ticket_analysis` | *(disponible pour skills V2)* |

### 🚀 DORA Metrics
| Tool | Skills qui l'utilisent |
|------|----------------------|
| `get_dora_views` | devops-maturity, delivery-trend, team-improvement |
| `get_dora_metrics` | devops-maturity, delivery-trend, innovation-vs-debt |
| `get_dora_trends` | devops-maturity, delivery-trend, team-improvement |

### 🎯 Assessment
| Tool | Skills qui l'utilisent |
|------|----------------------|
| `get_competency_frameworks` | agile-transformation |
| `get_assessments` | art-performance, agile-transformation, devops-maturity |
| `get_assessment_detail` | *(disponible pour skills V2)* |
| `get_assessment_tasks` | agile-transformation |
| `get_assessment_compare` | agile-transformation, team-improvement |
| `get_assessment_trends` | agile-transformation, team-improvement |

---

## Modules FAP requis par persona

| Persona | Flow Metrics | DORA Metrics | Assessment |
|---------|:------------:|:------------:|:----------:|
| Product Owner | ✅ Requis | — | — |
| Scrum Master | ✅ Requis | — | — |
| RTE | ✅ Requis | ✅ Requis | Recommandé |
| Manager | ✅ Requis | Recommandé | ✅ Requis |
| CEO / CPO | ✅ Requis | Recommandé | Recommandé |

---

## Exemples de conversations

### Product Owner — Delivery Forecast
```
PO : "On a promis à Airbus une livraison fin mai. On est réalistes ?"

FAP : Prévision de livraison — Projet Core Platform
      Verdict : ⚠️ RISQUE MODÉRÉ
      
      Prévision P85 : livraison probable avant le 2 juin (+3 jours)
      Cycle time médian : 8 jours (P85 : 14 jours)
      Tickets bloqués : 2 depuis 6 jours en moyenne
      
      La date est atteignable mais 2 stories sont bloquées depuis plus 
      d'une semaine et consomment de la capacité. Si non débloquées 
      sous 48h, la livraison fin mai devient incertaine.
      
      Action : Identifier et débloquer WPM-34 et WPM-41 aujourd'hui.
```

### CEO — Delivery Trend
```
CEO : "On livre plus vite qu'il y a un an ?"

FAP : Delivery Trend — Organisation (6 mois)
      Verdict : 📈 AMÉLIORATION RÉGULIÈRE — Score +62/100
      
      Vitesse : cycle time 12j → 8j (-33% plus rapide)
      Volume : throughput +18% sur 6 mois
      Déploiements : niveau Medium → High sur 3 équipes core
      Couverture : 6 équipes sur 8 progressent
      
      L'organisation livre aujourd'hui une fonctionnalité en 4 jours 
      de moins qu'il y a 6 mois, avec 18% de volume supplémentaire.
      
      Décision : Protéger l'investissement en transformation — 
      ne pas sacrifier les pratiques d'amélioration au profit 
      du scope court terme.
```

---

## Contribuer

Ces skills sont maintenues et enrichies par l'équipe FAP.  
Pour suggérer une nouvelle skill ou signaler un problème :

- **Ouvrir une issue** sur ce repo avec le tag `skill-request`
- **Proposer une PR** en suivant le template de skill dans `docs/skill-template.md`
- **Contacter l'équipe** via [flowanalyticspro.com](https://flowanalyticspro.com)

### Critères d'acceptation d'une nouvelle skill
- Répond à une question métier réelle d'un persona identifié
- Mobilise au moins 3 tools FAP en séquence logique
- Inclut des règles d'interprétation avec seuils explicites
- Produit un format de sortie actionnable avec verdict + action

---

## Roadmap V2

Skills prévues pour la prochaine version :

| Persona | Skill | Question |
|---------|-------|----------|
| SM | `sprint-retrospective` | Quels sont les points clés pour notre rétro ? |
| RTE | `dependency-map` | Quelles sont les dépendances critiques inter-équipes ? |
| Manager | `team-health` | Quel est l'état de santé de mes équipes ? |
| CEO | `competitive-benchmark` | Comment se compare-t-on aux standards industrie ? |
| PO | `backlog-health` | Mon backlog est-il prêt pour le prochain cycle ? |

---

## À propos

**Flow Analytics Pro (FAP)** est une plateforme SaaS et Jira Add-on qui fournit Flow Metrics, DORA Metrics et Assessments pour les équipes agiles.

Développé par [AGILE4ME](https://flowanalyticspro.com) — Châtillon, France.

---

*FAP Skills Marketplace — v1.0.0*  
*15 skills • 5 personas • 26 tools MCP*

## Licence

© 2026 AGILE4ME — Flow Analytics Pro. Ces skills sont publiées sous licence [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/) : utilisation et partage autorisés, usage commercial interdit sans accord.
