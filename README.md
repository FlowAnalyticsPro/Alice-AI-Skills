# Flow Analytics Pro Skills Marketplace

> **Ready-to-use MCP skills for Flow Analytics Pro**
> Answer real questions from your agile teams — in natural language, with your actual data.

---

## What is a Flow Analytics Pro skill?

A **skill** is a set of `.md` files that orchestrates your Flow Analytics Pro MCP server to answer a specific business question. Each skill folder contains:

- `SKILL.md` — the **system prompt** that tells the LLM how to reason, which tools to call, and in what order
- `rules.md` — **interpretation rules** to turn data into a verdict
- `output.md` — the standardised, actionable **output format**
- `examples.md` — **conversation examples** illustrating the skill in action

```
You ask a question in natural language
         ↓
The LLM reads the skill
         ↓
It calls the Flow Analytics Pro tools in order
         ↓
It interprets the data according to the rules
         ↓
It answers in business language — not in metrics
```

**You don't need to know the 26 tools.** Pick your role, ask your question, get an answer.

---

## Prerequisites

- **Flow Analytics Pro** with the MCP server configured (port 3030)
- An MCP-compatible client: Claude Desktop, Cursor, or any LLM supporting the MCP protocol
- The Flow Analytics Pro modules enabled for the skills you choose (Flow, DORA, Assessment)

---

## The 16 skills — by persona

### 👤 Product Owner

| Skill | Question | Usage frequency | Main tools |
|---|---|---|---|
| [`forecasting-delivery`](./skills/forecasting-delivery/SKILL.md) | Will this feature be delivered on time? | Before each commitment | `get_forecast`, `get_flow_metrics` |
| [`planning-capacity`](./skills/planning-capacity/SKILL.md) | How many items can I commit to in the next cycle? | Before each sprint | `get_sprint_metrics`, `get_flow_metrics` |
| [`tracking-commitment-risk`](./skills/tracking-commitment-risk/SKILL.md) | Which items risk derailing my commitments? | Daily / standup | `get_due_date_analysis`, `get_blocked_tickets` |

---

### 🔄 Scrum Master / Flow Master

| Skill | Question | Usage frequency | Main tools |
|---|---|---|---|
| [`diagnosing-flow-health`](./skills/diagnosing-flow-health/SKILL.md) | Is our flow healthy today? | Weekly | `get_flow_metrics`, `get_step_analysis` |
| [`measuring-predictability`](./skills/measuring-predictability/SKILL.md) | Is the team predictable? | Monthly / per sprint | `get_sprint_metrics`, `get_flow_trends` |
| [`detecting-bottlenecks`](./skills/detecting-bottlenecks/SKILL.md) | Where are the bottlenecks in our workflow? | Retro / kaizen | `get_step_analysis`, `get_blocked_tickets` |

---

### 🚂 Release Train Engineer (SAFe)

| Skill | Question | Usage frequency | Main tools |
|---|---|---|---|
| [`assessing-art-performance`](./skills/assessing-art-performance/SKILL.md) | Which ART teams are struggling? | Weekly / ART Sync | `get_programs`, `get_blocked_tickets` |
| [`assessing-pi-risk`](./skills/assessing-pi-risk/SKILL.md) | Will the PI meet its objectives? | Bi-weekly | `get_forecast`, `get_due_date_analysis` |
| [`assessing-devops-maturity`](./skills/assessing-devops-maturity/SKILL.md) | What is the DevOps maturity of my teams? | Monthly | `get_dora_metrics`, `get_dora_trends` |

---

### 📊 Engineering Manager / Director

| Skill | Question | Usage frequency | Main tools |
|---|---|---|---|
| [`tracking-team-commitments`](./skills/tracking-team-commitments/SKILL.md) | Are our teams meeting their commitments? | Monthly / quarterly | `get_sprint_metrics`, `get_due_date_analysis` |
| [`assessing-agile-transformation`](./skills/assessing-agile-transformation/SKILL.md) | Where are we in our agile transformation? | Quarterly | `get_assessments`, `get_assessment_compare` |
| [`measuring-delivery-capacity`](./skills/measuring-delivery-capacity/SKILL.md) | What is our actual delivery capacity? | Monthly / roadmap | `get_dimension_metrics`, `get_flow_trends` |

---

### 🎯 CEO / CPO

| Skill | Question | Usage frequency | Main tools |
|---|---|---|---|
| [`analyzing-delivery-trend`](./skills/analyzing-delivery-trend/SKILL.md) | Are we delivering faster than before? | Quarterly / QBR | `get_flow_trends`, `get_dora_trends` |
| [`analyzing-innovation-vs-debt`](./skills/analyzing-innovation-vs-debt/SKILL.md) | What share goes to innovation vs. debt? | Quarterly / budget | `get_dimension_metrics`, `get_dora_metrics` |
| [`measuring-team-improvement`](./skills/measuring-team-improvement/SKILL.md) | Are our teams improving? | Semi-annual / annual | `get_assessment_compare`, `get_flow_trends`, `get_dora_trends` |

---

### 🔍 Cross-persona

| Skill | Question | Usage frequency | Main tools |
|---|---|---|---|
| [`tracking-commitment-risk`](./skills/tracking-commitment-risk/SKILL.md) | Which commitments are at risk right now? | Daily | `get_due_date_analysis`, `get_blocked_tickets`, `get_aging_wip` |

---

## Repository structure

```
Alice-AI-Skills/
│
├── README.md                          ← this file (English)
├── README.fr.md                       ← French version
│
├── template/                          ← skill template to create new skills
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
    └── (each folder contains SKILL.md, rules.md, output.md, examples.md)
```

---

## How to use a skill

### Option 1 — Claude Desktop (recommended)

1. Configure the Flow Analytics Pro MCP server in your `claude_desktop_config.json`
2. Open the `SKILL.md` file of the desired skill
3. Copy its content and paste it as a **system prompt** in your conversation
4. Ask your question in natural language

```json
{
  "mcpServers": {
    "fap": {
      "command": "node",
      "args": ["/path/to/fap-mcp-server/dist/index.js"],
      "env": {
        "FAP_API_URL": "https://app.flowanalyticspro.com",
        "FAP_API_KEY": "your-api-key"
      }
    }
  }
}
```

### Option 2 — Cursor

1. Add the Flow Analytics Pro MCP server in the Cursor settings
2. Open the `SKILL.md` file as context
3. Ask your question in the chat

### Option 3 — Integration into your own interface

Each skill's `SKILL.md` contains a ready-to-use system prompt. Integrate it into your application via the Anthropic API with the Flow Analytics Pro MCP tools enabled.

---

## Coverage of the 26 Flow Analytics Pro MCP tools

### 📊 Portfolio & Projects

| Tool | Skills using it |
|---|---|
| `get_portfolio` | forecasting-delivery, planning-capacity, tracking-commitment-risk, diagnosing-flow-health, measuring-predictability, detecting-bottlenecks |
| `get_project` | planning-capacity, measuring-predictability |
| `get_programs` | assessing-art-performance, assessing-pi-risk, assessing-devops-maturity, tracking-team-commitments, assessing-agile-transformation, measuring-delivery-capacity, analyzing-delivery-trend, analyzing-innovation-vs-debt, measuring-team-improvement |

### 🔄 Flow Metrics

| Tool | Skills using it |
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
| `get_ticket_analysis` | *(available for V2 skills)* |

### 🚀 DORA Metrics

| Tool | Skills using it |
|---|---|
| `get_dora_views` | assessing-devops-maturity, analyzing-delivery-trend, measuring-team-improvement |
| `get_dora_metrics` | assessing-devops-maturity, analyzing-delivery-trend, analyzing-innovation-vs-debt |
| `get_dora_trends` | assessing-devops-maturity, analyzing-delivery-trend, measuring-team-improvement |

### 🎯 Assessment

| Tool | Skills using it |
|---|---|
| `get_competency_frameworks` | assessing-agile-transformation |
| `get_assessments` | assessing-art-performance, assessing-agile-transformation, assessing-devops-maturity |
| `get_assessment_detail` | *(available for V2 skills)* |
| `get_assessment_compare` | assessing-agile-transformation, measuring-team-improvement |
| `get_assessment_trends` | assessing-agile-transformation, measuring-team-improvement |

---

## Flow Analytics Pro modules required by persona

| Persona | Flow Metrics | DORA Metrics | Assessment |
|---|---|---|---|
| Product Owner | ✅ Required | — | — |
| Scrum Master | ✅ Required | — | — |
| RTE | ✅ Required | ✅ Required | Recommended |
| Manager | ✅ Required | Recommended | ✅ Required |
| CEO / CPO | ✅ Required | Recommended | Recommended |

---

## Contributing

These skills are maintained and expanded by the Flow Analytics Pro team.
To suggest a new skill or report an issue:

- **Open an issue** on this repo with the `skill-request` tag
- **Submit a PR** following the skill template in [`template/SKILL.md`](./template/SKILL.md)
- **Contact the team** via [flowanalyticspro.com](https://flowanalyticspro.com)

### Acceptance criteria for a new skill

- Answers a real business question from an identified persona
- Uses at least 3 Flow Analytics Pro tools in a logical sequence
- Includes interpretation rules with explicit thresholds
- Produces an actionable output format with verdict + action

---

## V2 Roadmap

| Persona | Skill | Question |
|---|---|---|
| SM | `sprint-retrospective` | What are the key takeaways for our retro? |
| RTE | `dependency-map` | What are the critical cross-team dependencies? |
| Manager | `team-health` | What is the health status of my teams? |
| CEO | `competitive-benchmark` | How do we compare to industry standards? |
| PO | `backlog-health` | Is my backlog ready for the next cycle? |

---

## About

**Flow Analytics Pro (FAP)** is a SaaS platform and Jira Add-on providing Flow Metrics, DORA Metrics, and Assessments for agile teams.

Developed by [AGILE4ME](https://flowanalyticspro.com) — Châtillon, France.

---

*Flow Analytics Pro Skills Marketplace — v1.0.0*
*16 skills • 5 personas • 26 MCP tools*

---

## License

© 2026 AGILE4ME — Flow Analytics Pro. These skills are published under the [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/) license: use and sharing allowed, commercial use prohibited without agreement.
