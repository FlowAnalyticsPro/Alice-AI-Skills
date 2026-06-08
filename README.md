# Flow Analytics Pro Skills Marketplace

> **Ready-to-use MCP skills for Flow Analytics Pro**  
> Answer real questions from your agile teams — in natural language, with your actual data.

---

## What is a Flow Analytics Pro skill?

A **skill** is a `.md` file that orchestrates your Flow Analytics Pro MCP server to answer a specific business question. It contains:

- A **system prompt** that tells the LLM how to reason
- A **sequence of MCP calls** to your 26 Flow Analytics Pro tools
- **Interpretation rules** to turn data into a verdict
- A standardised, actionable **output format**

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

## The 15 skills — by persona

### 👤 Product Owner

| Skill                                                   | Question                                          | Usage frequency        | Main tools                                     |
| ------------------------------------------------------- | ------------------------------------------------- | ---------------------- | ---------------------------------------------- |
| [`delivery-forecast`](./skills/po/delivery-forecast.md) | Will this feature be delivered on time?           | Before each commitment | `get_forecast`, `get_flow_metrics`             |
| [`capacity-planning`](./skills/po/capacity-planning.md) | How many items can I commit to in the next cycle? | Before each sprint     | `get_sprint_metrics`, `get_flow_metrics`       |
| [`commitment-risk`](./skills/po/commitment-risk.md)     | Which items risk derailing my commitments?        | Daily / standup        | `get_due_date_analysis`, `get_blocked_tickets` |

---

### 🔄 Scrum Master / Flow Master

| Skill                                                         | Question                                   | Usage frequency      | Main tools                                 |
| ------------------------------------------------------------- | ------------------------------------------ | -------------------- | ------------------------------------------ |
| [`flow-health`](./skills/sm/flow-health.md)                   | Is our flow healthy today?                 | Weekly               | `get_flow_metrics`, `get_step_analysis`    |
| [`predictability`](./skills/sm/predictability.md)             | Is the team predictable?                   | Monthly / per sprint | `get_sprint_metrics`, `get_flow_trends`    |
| [`bottleneck-detection`](./skills/sm/bottleneck-detection.md) | Where are the bottlenecks in our workflow? | Retro / kaizen       | `get_step_analysis`, `get_blocked_tickets` |

---

### 🚂 Release Train Engineer (SAFe)

| Skill                                                | Question                                 | Usage frequency   | Main tools                                |
| ---------------------------------------------------- | ---------------------------------------- | ----------------- | ----------------------------------------- |
| [`art-performance`](./skills/rte/art-performance.md) | Which ART teams are struggling?          | Weekly / ART Sync | `compare_projects`, `get_blocked_tickets` |
| [`pi-risk`](./skills/rte/pi-risk.md)                 | Will the PI meet its objectives?         | Bi-weekly         | `get_forecast`, `get_due_date_analysis`   |
| [`devops-maturity`](./skills/rte/devops-maturity.md) | What is the DevOps maturity of my teams? | Monthly           | `get_dora_metrics`, `get_dora_trends`     |

---

### 📊 Engineering Manager / Director

| Skill                                                              | Question                                  | Usage frequency     | Main tools                                    |
| ------------------------------------------------------------------ | ----------------------------------------- | ------------------- | --------------------------------------------- |
| [`commitment-tracking`](./skills/manager/commitment-tracking.md)   | Are our teams meeting their commitments?  | Monthly / quarterly | `get_sprint_metrics`, `get_due_date_analysis` |
| [`agile-transformation`](./skills/manager/agile-transformation.md) | Where are we in our agile transformation? | Quarterly           | `get_assessments`, `get_assessment_trends`    |
| [`delivery-capacity`](./skills/manager/delivery-capacity.md)       | What is our actual delivery capacity?     | Monthly / roadmap   | `get_dimension_metrics`, `compare_projects`   |

---

### 🎯 CEO / CPO

| Skill                                                      | Question                                | Usage frequency      | Main tools                                                    |
| ---------------------------------------------------------- | --------------------------------------- | -------------------- | ------------------------------------------------------------- |
| [`delivery-trend`](./skills/ceo/delivery-trend.md)         | Are we delivering faster than before?   | Quarterly / QBR      | `get_flow_trends`, `get_dora_trends`                          |
| [`innovation-vs-debt`](./skills/ceo/innovation-vs-debt.md) | What share goes to innovation vs. debt? | Quarterly / budget   | `get_dimension_metrics`, `get_dora_metrics`                   |
| [`team-improvement`](./skills/ceo/team-improvement.md)     | Are our teams improving?                | Semi-annual / annual | `get_assessment_trends`, `get_flow_trends`, `get_dora_trends` |

---

## Repository structure

```
Flow Analytics Pro-skills-marketplace/
│
├── README.md                          ← this file
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
    ├── how-skills-work.md             ← technical guide
    ├── mcp-tools-reference.md         ← reference for the 26 tools
    └── faq.md                         ← frequently asked questions
```

---

## How to use a skill

### Prerequisites

### Accessing the Flow Analytics Pro MCP server

Configure the MCP server in your generative AI tool:

- [Claude](https://claude.ai/customize/connectors?modal=add-custom-connector)
- [ChatGPT](https://chatgpt.com/#settings/Connectors/Advanced)
- [Mistral](https://docs.mistral.ai/vibe/work/connectors/mcp-connectors#custom-connectors)

### Option 1 — Claude Desktop (recommended)

<del>
1. Configure the Flow Analytics Pro MCP server in your `claude_desktop_config.json`
2. Copy the content of the desired skill file
3. Paste it as a **system prompt** in your conversation
4. Ask your question in natural language

```json
{
  "mcpServers": {
    "Flow Analytics Pro": {
      "command": "node",
      "args": ["/path/to/Flow Analytics Pro-mcp-server/dist/index.js"],
      "env": {
        "Flow Analytics Pro_API_URL": "https://app.flowanalyticspro.com",
        "Flow Analytics Pro_API_KEY": "your-api-key"
      }
    }
  }
}
```

</del>

### <del>Option 2 — Cursor</del>

<del>
1. Add the Flow Analytics Pro MCP server in the Cursor settings
2. Open the skill file as context
3. Ask your question in the chat
</del>

### <del>Option 3 — Integration into your own interface</del>

<del>Each skill contains a ready-to-use **system prompt**. Integrate it into your application via the Anthropic API with the Flow Analytics Pro MCP tools enabled.</del>

---

## Coverage of the 26 Flow Analytics Pro MCP tools

The 15 skills cover all available tools:

### 📊 Portfolio & Projects

| Tool               | Skills using it                                                                                                                                               |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `get_portfolio`    | delivery-forecast, capacity-planning, commitment-risk, flow-health, predictability, bottleneck-detection                                                      |
| `get_project`      | capacity-planning, predictability                                                                                                                             |
| `get_programs`     | art-performance, pi-risk, devops-maturity, commitment-tracking, agile-transformation, delivery-capacity, delivery-trend, innovation-vs-debt, team-improvement |
| `compare_projects` | art-performance, pi-risk, commitment-tracking, delivery-capacity, innovation-vs-debt, team-improvement                                                        |

### 🔄 Flow Metrics

| Tool                    | Skills using it                                                                                                                     |
| ----------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| `get_flow_metrics`      | delivery-forecast, capacity-planning, flow-health, predictability, bottleneck-detection, commitment-tracking                        |
| `get_flow_trends`       | flow-health, predictability, bottleneck-detection, pi-risk, delivery-capacity, delivery-trend, innovation-vs-debt, team-improvement |
| `get_issues`            | commitment-risk, flow-health, capacity-planning                                                                                     |
| `get_sprint_metrics`    | capacity-planning, predictability, art-performance, commitment-tracking                                                             |
| `get_step_analysis`     | flow-health, bottleneck-detection, capacity-planning                                                                                |
| `get_blocked_tickets`   | delivery-forecast, commitment-risk, flow-health, art-performance, pi-risk, delivery-capacity                                        |
| `get_dimension_metrics` | bottleneck-detection, predictability, delivery-capacity, innovation-vs-debt                                                         |
| `get_due_date_analysis` | delivery-forecast, commitment-risk, art-performance, pi-risk, commitment-tracking                                                   |
| `get_forecast`          | delivery-forecast, capacity-planning (Scrum), pi-risk, commitment-tracking, delivery-capacity                                       |
| `get_ticket_analysis`   | _(available for V2 skills)_                                                                                                         |

### 🚀 DORA Metrics

| Tool               | Skills using it                                     |
| ------------------ | --------------------------------------------------- |
| `get_dora_views`   | devops-maturity, delivery-trend, team-improvement   |
| `get_dora_metrics` | devops-maturity, delivery-trend, innovation-vs-debt |
| `get_dora_trends`  | devops-maturity, delivery-trend, team-improvement   |

### 🎯 Assessment

| Tool                        | Skills using it                                        |
| --------------------------- | ------------------------------------------------------ |
| `get_competency_frameworks` | agile-transformation                                   |
| `get_assessments`           | art-performance, agile-transformation, devops-maturity |
| `get_assessment_detail`     | _(available for V2 skills)_                            |
| `get_assessment_tasks`      | agile-transformation                                   |
| `get_assessment_compare`    | agile-transformation, team-improvement                 |
| `get_assessment_trends`     | agile-transformation, team-improvement                 |

---

## Flow Analytics Pro modules required by persona

| Persona       | Flow Metrics | DORA Metrics | Assessment  |
| ------------- | :----------: | :----------: | :---------: |
| Product Owner | ✅ Required  |      —       |      —      |
| Scrum Master  | ✅ Required  |      —       |      —      |
| RTE           | ✅ Required  | ✅ Required  | Recommended |
| Manager       | ✅ Required  | Recommended  | ✅ Required |
| CEO / CPO     | ✅ Required  | Recommended  | Recommended |

---

## Conversation examples

### Product Owner — Delivery Forecast

```
PO: "We promised Airbus a delivery by end of May. Are we being realistic?"

Flow Analytics Pro: Delivery Forecast — Core Platform Project
      Verdict: ⚠️ MODERATE RISK

      P85 forecast: likely delivery before June 2nd (+3 days)
      Median cycle time: 8 days (P85: 14 days)
      Blocked tickets: 2 blocked for an average of 6 days

      The date is achievable but 2 stories have been blocked for over
      a week and are consuming capacity. If not unblocked within 48h,
      end-of-May delivery becomes uncertain.

      Action: Identify and unblock WPM-34 and WPM-41 today.
```

### CEO — Delivery Trend

```
CEO: "Are we delivering faster than a year ago?"

Flow Analytics Pro: Delivery Trend — Organisation (6 months)
      Verdict: 📈 STEADY IMPROVEMENT — Score +62/100

      Speed: cycle time 12d → 8d (-33% faster)
      Volume: throughput +18% over 6 months
      Deployments: Medium → High level on 3 core teams
      Coverage: 6 out of 8 teams improving

      The organisation today delivers a feature 4 days faster
      than 6 months ago, with 18% more volume.

      Decision: Protect the transformation investment —
      do not sacrifice improvement practices in favour of
      short-term scope.
```

---

## Contributing

These skills are maintained and expanded by the Flow Analytics Pro team.  
To suggest a new skill or report an issue:

- **Open an issue** on this repo with the `skill-request` tag
- **Submit a PR** following the skill template in `template/SKILL.md`
- **Contact the team** via [flowanalyticspro.com](https://flowanalyticspro.com)

### Acceptance criteria for a new skill

- Answers a real business question from an identified persona
- Uses at least 3 Flow Analytics Pro tools in a logical sequence
- Includes interpretation rules with explicit thresholds
- Produces an actionable output format with verdict + action

---

## V2 Roadmap

Skills planned for the next version:

| Persona | Skill                   | Question                                       |
| ------- | ----------------------- | ---------------------------------------------- |
| SM      | `sprint-retrospective`  | What are the key takeaways for our retro?      |
| RTE     | `dependency-map`        | What are the critical cross-team dependencies? |
| Manager | `team-health`           | What is the health status of my teams?         |
| CEO     | `competitive-benchmark` | How do we compare to industry standards?       |
| PO      | `backlog-health`        | Is my backlog ready for the next cycle?        |

---

## About

**Flow Analytics Pro (FAP)** is a SaaS platform and Jira Add-on providing Flow Metrics, DORA Metrics, and Assessments for agile teams.

Developed by [AGILE4ME](https://flowanalyticspro.com) — Châtillon, France.

---

_Flow Analytics Pro Skills Marketplace — v1.0.0_  
_15 skills • 5 personas • 26 MCP tools_

## License

© 2026 AGILE4ME — Flow Analytics Pro. These skills are published under the [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/) license: use and sharing allowed, commercial use prohibited without agreement.
