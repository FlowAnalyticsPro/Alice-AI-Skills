# Flow Analytics Pro Skills Marketplace

> **Skills MCP prêts à l'emploi pour Flow Analytics Pro**
> Répondez aux vraies questions de vos équipes agiles — en langage naturel, avec vos données réelles.

---

## Qu'est-ce qu'une skill Flow Analytics Pro ?

Une **skill** est un ensemble de fichiers `.md` qui orchestre votre serveur MCP Flow Analytics Pro pour répondre à une question métier précise. Chaque dossier de skill contient :

- `SKILL.md` — le **system prompt** qui dit au LLM comment raisonner, quels tools appeler et dans quel ordre
- `rules.md` — les **règles d'interprétation** pour transformer les données en verdict
- `output.md` — le **format de sortie** standardisé et actionnable
- `examples.md` — des **exemples de conversations** illustrant la skill en action

```
Vous posez une question en langage naturel
         ↓
Le LLM lit la skill
         ↓
Il appelle les tools Flow Analytics Pro dans l'ordre
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
- Les modules Flow Analytics Pro activés selon les skills choisies (Flow, DORA, Assessment)

---

## Les 16 skills — par persona

### 👤 Product Owner

| Skill | Question | Fréquence d'usage | Tools principaux |
|---|---|---|---|
| [`forecasting-delivery`](./skills/forecasting-delivery/SKILL.md) | Cette feature sera-t-elle livrée à temps ? | Avant chaque engagement | `get_forecast`, `get_flow_metrics` |
| [`planning-capacity`](./skills/planning-capacity/SKILL.md) | Combien d'items puis-je engager sur le prochain cycle ? | Avant chaque sprint | `get_sprint_metrics`, `get_flow_metrics` |
| [`tracking-commitment-risk`](./skills/tracking-commitment-risk/SKILL.md) | Quels items risquent de faire dérailler mes engagements ? | Quotidien / standup | `get_due_date_analysis`, `get_blocked_tickets` |

---

### 🔄 Scrum Master / Flow Master

| Skill | Question | Fréquence d'usage | Tools principaux |
|---|---|---|---|
| [`diagnosing-flow-health`](./skills/diagnosing-flow-health/SKILL.md) | Notre flow est-il sain aujourd'hui ? | Hebdomadaire | `get_flow_metrics`, `get_step_analysis` |
| [`measuring-predictability`](./skills/measuring-predictability/SKILL.md) | L'équipe est-elle prévisible ? | Mensuel / par sprint | `get_sprint_metrics`, `get_flow_trends` |
| [`detecting-bottlenecks`](./skills/detecting-bottlenecks/SKILL.md) | Où sont les goulots dans notre workflow ? | Rétro / kaizen | `get_step_analysis`, `get_blocked_tickets` |

---

### 🚂 Release Train Engineer (SAFe)

| Skill | Question | Fréquence d'usage | Tools principaux |
|---|---|---|---|
| [`assessing-art-performance`](./skills/assessing-art-performance/SKILL.md) | Quelles équipes de l'ART sont en difficulté ? | Hebdomadaire / ART Sync | `get_programs`, `get_blocked_tickets` |
| [`assessing-pi-risk`](./skills/assessing-pi-risk/SKILL.md) | Le PI va-t-il tenir ses objectifs ? | Bi-hebdomadaire | `get_forecast`, `get_due_date_analysis` |
| [`assessing-devops-maturity`](./skills/assessing-devops-maturity/SKILL.md) | Quelle est la maturité DevOps de mes équipes ? | Mensuel | `get_dora_metrics`, `get_dora_trends` |

---

### 📊 Engineering Manager / Director

| Skill | Question | Fréquence d'usage | Tools principaux |
|---|---|---|---|
| [`tracking-team-commitments`](./skills/tracking-team-commitments/SKILL.md) | Nos équipes tiennent-elles leurs engagements ? | Mensuel / trimestriel | `get_sprint_metrics`, `get_due_date_analysis` |
| [`assessing-agile-transformation`](./skills/assessing-agile-transformation/SKILL.md) | Où en est notre transformation agile ? | Trimestriel | `get_assessments`, `get_assessment_compare` |
| [`measuring-delivery-capacity`](./skills/measuring-delivery-capacity/SKILL.md) | Quelle est notre capacité réelle de delivery ? | Mensuel / roadmap | `get_dimension_metrics`, `get_flow_trends` |

---

### 🎯 CEO / CPO

| Skill | Question | Fréquence d'usage | Tools principaux |
|---|---|---|---|
| [`analyzing-delivery-trend`](./skills/analyzing-delivery-trend/SKILL.md) | Livrons-nous plus vite qu'avant ? | Trimestriel / QBR | `get_flow_trends`, `get_dora_trends` |
| [`analyzing-innovation-vs-debt`](./skills/analyzing-innovation-vs-debt/SKILL.md) | Quelle part va à l'innovation vs la dette ? | Trimestriel / budget | `get_dimension_metrics`, `get_dora_metrics` |
| [`measuring-team-improvement`](./skills/measuring-team-improvement/SKILL.md) | Nos équipes s'améliorent-elles ? | Semestriel / annuel | `get_assessment_compare`, `get_flow_trends`, `get_dora_trends` |

---

### 🔍 Transversal

| Skill | Question | Fréquence d'usage | Tools principaux |
|---|---|---|---|
| [`tracking-commitment-risk`](./skills/tracking-commitment-risk/SKILL.md) | Quels engagements sont à risque en ce moment ? | Quotidien | `get_due_date_analysis`, `get_blocked_tickets`, `get_aging_wip` |

---

## Structure du repo

```
Alice-AI-Skills/
│
├── README.md                          ← version anglaise
├── README.fr.md                       ← ce fichier (français)
│
├── template/                          ← template pour créer de nouvelles skills
│   ├── SKILL.md
│   ├── rules.md
│   ├── output.md
│   └── examples.md
│
└── skills/
    ├── forecasting-delivery/
    ├── planning-capacity/
    ├── tracking-commitment-risk/
    ├── diagnosing-flow-health/
    ├── measuring-predictability/
    ├── detecting-bottlenecks/
    ├── assessing-art-performance/
    ├── assessing-pi-risk/
    ├── assessing-devops-maturity/
    ├── tracking-team-commitments/
    ├── assessing-agile-transformation/
    ├── measuring-delivery-capacity/
    ├── analyzing-delivery-trend/
    ├── analyzing-innovation-vs-debt/
    ├── measuring-team-improvement/
    └── (chaque dossier contient SKILL.md, rules.md, output.md, examples.md)
```

---

## Comment utiliser une skill

### Option 1 — Claude Desktop (recommandé)

1. Configurez le serveur MCP Flow Analytics Pro dans votre `claude_desktop_config.json`
2. Ouvrez le fichier `SKILL.md` de la skill souhaitée
3. Copiez son contenu et collez-le comme **system prompt** dans votre conversation
4. Posez votre question en langage naturel

```json
{
  "mcpServers": {
    "fap": {
      "command": "node",
      "args": ["/path/to/fap-mcp-server/dist/index.js"],
      "env": {
        "FAP_API_URL": "https://app.flowanalyticspro.com",
        "FAP_API_KEY": "votre-clé-api"
      }
    }
  }
}
```

### Option 2 — Cursor

1. Ajoutez le serveur MCP Flow Analytics Pro dans les settings Cursor
2. Ouvrez le fichier `SKILL.md` comme contexte
3. Posez votre question dans le chat

### Option 3 — Intégration dans votre propre interface

Le fichier `SKILL.md` de chaque skill contient un system prompt prêt à l'emploi. Intégrez-le dans votre application via l'API Anthropic avec les tools MCP Flow Analytics Pro activés.

---

## Couverture des 26 tools MCP Flow Analytics Pro

### 📊 Portfolio & Projets

| Tool | Skills qui l'utilisent |
|---|---|
| `get_portfolio` | forecasting-delivery, planning-capacity, tracking-commitment-risk, diagnosing-flow-health, measuring-predictability, detecting-bottlenecks |
| `get_project` | planning-capacity, measuring-predictability |
| `get_programs` | assessing-art-performance, assessing-pi-risk, assessing-devops-maturity, tracking-team-commitments, assessing-agile-transformation, measuring-delivery-capacity, analyzing-delivery-trend, analyzing-innovation-vs-debt, measuring-team-improvement |

### 🔄 Flow Metrics

| Tool | Skills qui l'utilisent |
|---|---|
| `get_flow_metrics` | forecasting-delivery, planning-capacity, diagnosing-flow-health, measuring-predictability, detecting-bottlenecks, tracking-team-commitments |
| `get_flow_trends` | diagnosing-flow-health, measuring-predictability, detecting-bottlenecks, assessing-pi-risk, measuring-delivery-capacity, analyzing-delivery-trend, analyzing-innovation-vs-debt, measuring-team-improvement |
| `get_issues` | tracking-commitment-risk, diagnosing-flow-health, planning-capacity |
| `get_sprint_metrics` | planning-capacity, measuring-predictability, assessing-art-performance, tracking-team-commitments |
| `get_step_analysis` | diagnosing-flow-health, detecting-bottlenecks, planning-capacity |
| `get_blocked_tickets` | forecasting-delivery, tracking-commitment-risk, diagnosing-flow-health, assessing-art-performance, assessing-pi-risk, measuring-delivery-capacity |
| `get_dimension_metrics` | detecting-bottlenecks, measuring-predictability, measuring-delivery-capacity, analyzing-innovation-vs-debt |
| `get_due_date_analysis` | forecasting-delivery, tracking-commitment-risk, assessing-art-performance, assessing-pi-risk, tracking-team-commitments |
| `get_forecast` | forecasting-delivery, planning-capacity, assessing-pi-risk, tracking-team-commitments, measuring-delivery-capacity |
| `get_aging_wip` | tracking-commitment-risk, diagnosing-flow-health |
| `get_ticket_analysis` | *(disponible pour les skills V2)* |

### 🚀 DORA Metrics

| Tool | Skills qui l'utilisent |
|---|---|
| `get_dora_views` | assessing-devops-maturity, analyzing-delivery-trend, measuring-team-improvement |
| `get_dora_metrics` | assessing-devops-maturity, analyzing-delivery-trend, analyzing-innovation-vs-debt |
| `get_dora_trends` | assessing-devops-maturity, analyzing-delivery-trend, measuring-team-improvement |

### 🎯 Assessment

| Tool | Skills qui l'utilisent |
|---|---|
| `get_competency_frameworks` | assessing-agile-transformation |
| `get_assessments` | assessing-art-performance, assessing-agile-transformation, assessing-devops-maturity |
| `get_assessment_detail` | *(disponible pour les skills V2)* |
| `get_assessment_compare` | assessing-agile-transformation, measuring-team-improvement |
| `get_assessment_trends` | assessing-agile-transformation, measuring-team-improvement |

---

## Modules FAP requis par persona

| Persona | Flow Metrics | DORA Metrics | Assessment |
|---|---|---|---|
| Product Owner | ✅ Requis | — | — |
| Scrum Master | ✅ Requis | — | — |
| RTE | ✅ Requis | ✅ Requis | Recommandé |
| Manager | ✅ Requis | Recommandé | ✅ Requis |
| CEO / CPO | ✅ Requis | Recommandé | Recommandé |

---

## Contribuer

Ces skills sont maintenues et enrichies par l'équipe Flow Analytics Pro.
Pour suggérer une nouvelle skill ou signaler un problème :

- **Ouvrir une issue** sur ce repo avec le tag `skill-request`
- **Proposer une PR** en suivant le template dans [`template/SKILL.md`](./template/SKILL.md)
- **Contacter l'équipe** via [flowanalyticspro.com](https://flowanalyticspro.com)

### Critères d'acceptation d'une nouvelle skill

- Répond à une question métier réelle d'un persona identifié
- Mobilise au moins 3 tools Flow Analytics Pro en séquence logique
- Inclut des règles d'interprétation avec seuils explicites
- Produit un format de sortie actionnable avec verdict + action

---

## Roadmap V2

| Persona | Skill | Question |
|---|---|---|
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

*Flow Analytics Pro Skills Marketplace — v1.0.0*
*16 skills • 5 personas • 26 tools MCP*

---

## Licence

© 2026 AGILE4ME — Flow Analytics Pro. Ces skills sont publiées sous licence [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/) : utilisation et partage autorisés, usage commercial interdit sans accord.
