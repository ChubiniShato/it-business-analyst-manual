# KPI Design Guide (EN)

A practical framework for creating and governing **Key Performance Indicators (KPIs)**.

## 1) Start from goals (OKRs)
- **Objective (qualitative):** What outcome do we expect?
- **Key Results (quantitative):** 2–4 measurable results that indicate progress.
- Link each KR to one or more **KPIs**.

## 2) Choose the right KPI type
- **Input / Activity** — what we do (e.g., number of discovery interviews)
- **Process** — how well we do it (e.g., cycle time, P95 latency)
- **Output** — what we ship (e.g., releases, features shipped)
- **Outcome** — user/business impact (e.g., adoption, retention). Prefer **outcomes**.

## 3) KPI definition template
- **Name** — unique and clear
- **Goal** — why it matters
- **Owner** — accountable team/person
- **Definition** — exact formula and scope
- **Unit** — %, count, seconds, etc.
- **Direction** — higher / lower / target band
- **Target & thresholds** — target, warning, critical
- **Data sources** — tables, events, dashboards
- **Cadence** — daily / weekly / monthly
- **Breakdowns** — platform, locale, cohort
- **Notes** — exceptions, limitations

## 4) Good KPI checklist
- Aligned to a goal and **actionable**
- **Measurable** with accessible data
- **Unambiguous** formula, time window, and scope
- **Sensitive** enough to detect change
- **Comparable** over time (stable definitions)

## 5) Common formulas
- **Percent / Rate:** (success / total) × 100
- **Average:** sum(value) / n
- **Ratio:** numerator / denominator (define the time window)
- **Cohort retention (Week N):** active_in_week_N / cohort_size
- **Compliance rate:** compliant_days / total_days

## 6) Anti‑patterns to avoid
- Vanity metrics with no value link
- KPIs without owners or targets
- Changing definitions without versioning
- Measuring outputs only; ignoring outcomes
- Single‑metric fixation — use a **balanced set**

## 7) Governance
- Maintain a **KPI Register** (see `/templates/kpi/`)
- Version KPI definitions and data-source changes
- Review cadence: weekly (operational), monthly (strategic)
- Anchor dashboards to a **North Star** metric and 3–5 guardrails

---

## Examples — PKU Diet Planning App

**North Star:** *Share of limit‑compliant planned days per active user*

1. **Limits Compliance Rate (Outcome)**
   - *Definition:* compliant_days / total_days in the last 30 days
   - *Target:* ≥ 70% (v1)
   - *Breakdowns:* by locale, age group, plan type (day/week)

2. **Plan Completion Time (Process)**
   - *Definition:* median seconds from “Start Plan” → “Plan Saved”
   - *Target:* ≤ 90s median (P95 ≤ 180s)

3. **Recipe Adjustment Adoption (Output → Outcome proxy)**
   - *Definition:* % of plans that include at least one ingredient adjustment
   - *Target:* ≥ 40%

4. **Active Users (Outcome)**
   - *Definition:* DAU / WAU / MAU; returning users %
   - *Target:* WAU growth ≥ 10% MoM

5. **Data Quality Score (Input/Process)**
   - *Definition:* share of catalog items passing validation rules
   - *Target:* ≥ 98%
   
---

## Instrumentation (analytics events)
Track at minimum:
- `plan_created`, `plan_saved`, `plan_validated` (with status)
- `ingredient_changed` (delta, units)
- `limit_exceed_warning` (type, over_by)
- `catalog_sync` (version, duration, items_updated)

## Dashboard blueprint
- North Star + trend
- Guardrails: latency, error rate, data quality
- Funnels: plan started → plan saved → validated
- Cohorts: monthly retention by signup month
- Segments: locale, platform, age group
