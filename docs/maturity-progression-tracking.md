# Maturity Progression Tracking

## Overview

A single maturity assessment tells you where an organization stands at a point in time. Progression tracking tells you whether the improvement program is working, at what rate, and whether progress is distributed evenly across domains or concentrated in areas receiving focused investment.

This document describes the operational model for running repeated TDMM assessments, measuring progression velocity, identifying stagnation, and communicating progress to leadership.

---

## Assessment Cadence

### Initial Baseline Assessment (Month 1)

The first assessment establishes the baseline. It should be a full 8-domain assessment following the methodology in `assessment-scorecard.md`. Common pitfalls at baseline:

- **Over-estimation bias**: Assessors who were involved in implementing controls tend to rate their effectiveness higher than an external reviewer would. Where possible, use a cross-team assessment panel — engineers from Team A assess Team B's CI/CD security, and vice versa.
- **Documentation vs. reality gap**: A policy document may describe a control that is not consistently applied in practice. Baseline assessment should prioritize evidence of actual control operation, not policy documentation existence.
- **Scope inconsistency**: The baseline must define scope explicitly — which teams, which environments, which products are in scope. If the scope changes between assessments, progress comparisons are invalid.

Document scope and assessment methodology at baseline. Changes to scope or methodology in subsequent assessments must be noted explicitly in the progression report.

### Quarterly Spot Assessments

Between full assessments, run targeted spot assessments on the 2–3 domains receiving active improvement investment. A spot assessment takes 2–4 hours per domain and produces a domain-level score and key finding update, without re-assessing the full 8-domain scope.

Spot assessments answer: "Is the improvement program for Domain X working?" They do not update the official maturity level (that requires a full assessment) but provide early signal on trajectory.

### Semi-Annual Full Assessments

Conduct a full 8-domain assessment every 6 months for organizations in active transformation (typically Levels 1–3). At higher maturity levels (4–5), annual full assessments are sufficient if quarterly spot assessments cover priority domains.

Semi-annual full assessments produce the official maturity level for each domain and the aggregate TDMM score used in executive reporting.

---

## Progression Metrics

### Domain Score

The primary progression metric is the domain score for each of the 8 TDMM domains, expressed as the current maturity level (1–5) and a decimal sub-level score (e.g., 2.7 = solidly Level 2, approaching Level 3) derived from the proportion of Level 3 criteria met.

**Domain score calculation:**
```
Domain Score = Current Level + (Level N+1 criteria met / Total Level N+1 criteria)
```
Example: An organization at Level 2 in Secure Development has met 4 of 8 Level 3 criteria → Domain Score = 2 + (4/8) = 2.5

**Aggregate TDMM Score:**
```
Aggregate Score = Average of all 8 domain scores (equally weighted)
```
Some organizations weight domains differently based on their risk profile. A financial services firm may weight compliance automation and access control more heavily. Document the weighting rationale if non-equal weights are used, and apply the same weights consistently across all assessments.

### Progression Velocity

Progression velocity measures the rate of score improvement per assessment period. Measure at both domain and aggregate level.

```
Velocity = (Current Score − Prior Score) / Months Between Assessments
```
A velocity of +0.1 per month indicates the organization will advance one full maturity level in approximately 10 months — a reasonable pace for well-resourced transformations. Velocity below +0.05/month for more than two consecutive periods indicates stagnation requiring investigation.

### Domain Dispersion

A well-functioning DevSecOps transformation improves all domains in reasonable proportion. High dispersion — where one or two domains advance rapidly while others stagnate — indicates:
- Uneven investment (resources concentrated in visible domains while foundational domains lag)
- Organizational bottlenecks (domains that require cross-team coordination or policy changes advance slower than technical domains)
- Assessment inconsistency (different assessment rigor across domains in different periods)

**Dispersion index:**
```
Dispersion Index = Standard Deviation of domain scores across all 8 domains
```
Target: Dispersion Index ≤ 0.8 at any assessment. A dispersion index above 1.2 indicates materially uneven development that should be surfaced to leadership.

---

## Tracking Dashboard

Maintain a progression tracking spreadsheet or dashboard with the following structure:

### Assessment History Table

| Assessment | Date | Domain 1 | Domain 2 | Domain 3 | Domain 4 | Domain 5 | Domain 6 | Domain 7 | Domain 8 | Aggregate | Dispersion |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Baseline | 2026-01 | 1.3 | 1.8 | 2.1 | 1.5 | 2.0 | 1.2 | 1.6 | 1.4 | 1.61 | 0.29 |
| Q2 Full | 2026-07 | 1.8 | 2.3 | 2.6 | 1.9 | 2.4 | 1.7 | 2.1 | 1.9 | 2.09 | 0.29 |
| Q4 Full | 2027-01 | 2.4 | 2.7 | 3.1 | 2.5 | 2.9 | 2.3 | 2.6 | 2.4 | 2.61 | 0.25 |

*TDMM Domain reference:*
1. Culture & Organization
2. Security Requirements
3. Secure Development
4. CI/CD Security
5. Cloud Security
6. Compliance Automation
7. Incident Response & Forensics
8. AI & Agentic Security

### Domain Progression Chart

For each domain, maintain a time-series chart showing:
- Actual score at each assessment point (solid line)
- Target trajectory to reach next level (dashed line, based on committed timeline)
- Spot assessment datapoints (marked distinctly from full assessment points)

When actual falls below target trajectory for two consecutive assessments in a domain, flag for leadership review.

### Velocity Heatmap

A heatmap view with domains on the Y-axis, assessment periods on the X-axis, and color representing velocity (progression rate per month):
- Dark green: Velocity > 0.1/month
- Light green: 0.05–0.10/month
- Yellow: 0.02–0.05/month (slow progress, investigate)
- Orange: 0.00–0.02/month (stagnation, escalate)
- Red: Negative velocity (regression, immediate attention)

---

## Identifying and Addressing Stagnation

### Stagnation Signals

**Technical stagnation**: The domain has reached the ceiling of what can be improved with tool deployment alone. The next capability level requires organizational change (cross-team processes, policy approval, budget allocation for different tooling). Example: CI/CD Security reaches 2.8 but cannot advance further without executive mandate to block deployments on policy failures.

**Organizational stagnation**: A specific team or function is blocking domain progress. A compliance domain may stagnate because the legal team has not approved the automated exception management workflow. Identify the specific organizational blocker, escalate to the appropriate level, and track unblocking as a dependency in the improvement roadmap.

**Resource stagnation**: The improvement program lacks the staffing, tooling budget, or time allocation to implement next-level capabilities. The stagnation is not a technical or organizational problem but a resource constraint. Escalate to leadership with a quantified ask and expected velocity improvement if the resource is provided.

**Measurement stagnation**: The organization has been measuring the same things and calling them improved, but the assessment methodology has not kept pace with the framework's higher-level criteria. At Level 2 moving to Level 3, the assessment must shift from "does a tool exist?" to "does the tool produce actionable results that are acted upon?" Stagnation can be artificial if the assessment does not faithfully apply Level 3 criteria.

### Intervention Framework

For any domain with velocity below 0.02/month for two consecutive periods:

1. **Diagnose the stagnation type** (technical / organizational / resource / measurement) using interviews with domain owners and review of the improvement backlog
2. **Identify the specific blocked capability** — which Level N+1 criterion has been stuck and why
3. **Define an unblocking action** — the single action that would most directly address the root cause
4. **Assign an owner and deadline** for the unblocking action
5. **Review in 30 days** — if the unblocking action is complete, re-assess the affected criteria; if not, escalate

---

## Leadership Communication

### Quarterly Progress Brief (10 minutes)

Structure for a quarterly executive update on TDMM progression:

```
DevSecOps Maturity Progress — Q[N] [YYYY]

AGGREGATE SCORE: [X.X] → [X.X] (+ [delta] vs. Q[N-1])
Target trajectory: on track / ahead / behind by [N] months

DOMAIN HIGHLIGHTS
  Fastest progressing: [Domain] (+ [delta], now [score])
  Attention required:  [Domain] (+ [delta], stagnation detected in [sub-capability])

NEXT LEVEL PROJECTIONS (at current velocity)
  [Domain]: Level [N] → [N+1] in ~[M] months
  [Domain]: Level [N] → [N+1] in ~[M] months

BLOCKERS REQUIRING LEADERSHIP DECISION
  [Specific unresolved organizational or resource blocker]
  Required action: [decision or resource request]
  Impact if unresolved: [M]-month delay to [Domain] Level [N+1]

NEXT ASSESSMENT: [date]
```

### Annual Board Summary

At an annual cadence, present a summary to the board or audit committee:
- Baseline vs. current aggregate score (absolute improvement)
- Mapping to peer benchmarks if available (e.g., "Level 2.8 aggregate places the organization in the top quartile of organizations at similar scale and compliance scope")
- Regulatory and audit readiness correlation: how the maturity improvement translates to compliance posture and audit performance
- Investment summary: what the maturity improvement program cost and what specific capability advances resulted

---

## Integrating Progression Data with Other Frameworks

TDMM progression data enriches several adjacent data streams:

**Compliance posture**: Domain 6 (Compliance Automation) score correlates directly with Control Pass Rate and Evidence Freshness Rate from `continuous-compliance-operations.md`. Use TDMM to explain why compliance metrics are improving or lagging.

**Incident response effectiveness**: Domain 7 (Incident Response & Forensics) score correlates with MTTR metrics from security operations. Lower MTTR values should accompany progression from Level 2 to Level 3 in this domain.

**AI security readiness**: Domain 8 (AI & Agentic Security) score provides the organizational readiness context for deploying AI components in the pipeline. Organizations below Level 2 in this domain should not deploy autonomous agents in production pipelines. Use this threshold as a formal gate in AI adoption programs.

**DORA metrics**: TDMM progression in Domain 3 (Secure Development) and Domain 4 (CI/CD Security) correlates with improvement in Change Failure Rate and Lead Time for Changes. Track both sets of metrics together to confirm that security controls are improving delivery performance (as they should) rather than degrading it.
