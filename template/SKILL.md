---
name: skill-name
description: [One sentence describing what this skill measures or produces, who uses it (CEO, CPO, Team Lead…), and when to trigger it (board meeting, sprint review, quarterly report…).]
---

# [Skill Title] ([Audience])

Answers: "[Core question this skill answers in plain language]"

## Workflow

```
- [ ] Step 1: [First step — e.g. map the organisation or gather context]
- [ ] Step 2: [Second step — e.g. fetch primary metric over the relevant period]
- [ ] Step 3: [Third step — e.g. fetch secondary metric]
- [ ] Step 4: [Fourth step — e.g. cross-reference or compare across teams/projects]
- [ ] Step 5: [Fifth step — e.g. calculate composite score → verdict + 1 decision]
```

## MCP Calls

**Required granularity: [WEEKLY / MONTHLY / QUARTERLY]** — justification if non-obvious.

**Step 2** — `FAP:<tool_name>` `{ param1: "value", param2: "value" }` — description of what this fetches

**Step 3** — `FAP:<tool_name>` `{ param1: "value" }` — description

**Step 4** — `FAP:<tool_name>` `{ param1: "value" }` — description

## [Skill Name] Score

```
Score = Delta_metricA × 0.XX   (what a positive value means)
      + Delta_metricB × 0.XX   (what a positive value means)
      + Delta_metricC × 0.XX   (what a positive value means)
```

See [rules.md](rules.md) for the verdict logic and key figures to produce.

## Output Format

See [output.md](output.md) — maximum [N] figures, 1 decision.

## [Audience] Rules

- [Rule 1 — e.g. never more than N numbers in the response]
- [Rule 2 — e.g. always translate metrics into business language]
- [Rule 3 — e.g. one strategic decision only, not a list of actions]
