# TDMM Scoring Rubric

This document is the scoring rubric for the TechStream DevSecOps Maturity Model (TDMM) 37-question, 5-level assessment instrument.

## Maturity levels

| Level | Name | Characteristics |
|---|---|---|
| 1 | Initial / Ad-hoc | Security activities exist but inconsistent, person-dependent |
| 2 | Repeatable | Documented processes; some automation; reactive posture |
| 3 | Defined | Standardized across teams; proactive controls; metrics emerging |
| 4 | Measured | Quantitatively managed; metrics drive decisions; continuous improvement |
| 5 | Optimizing | Adaptive; predictive; integrated with business outcomes; reference for industry |

## Eight domains × 37 questions

Each domain receives a score 1–5 based on the question responses within it.

### Domain 1 — Strategy & Governance (4 questions)

Q1: Is there a written DevSecOps strategy approved by executive leadership?
- L1: No strategy exists
- L2: Informal strategy in slides only
- L3: Written strategy reviewed annually
- L4: Strategy with measurable objectives tracked quarterly
- L5: Strategy integrated with business outcomes; updated continuously

[Additional questions Q2-Q4 follow the same pattern.]

### Domain 2 — Threat Modeling (4 questions)

[Q5-Q8]

### Domain 3 — Secure SDLC (5 questions)

[Q9-Q13]

### Domain 4 — Software Supply Chain (5 questions)

[Q14-Q18 — covers SBOM, signing, SLSA, dependency review, third-party risk]

### Domain 5 — CI/CD Security (5 questions)

[Q19-Q23]

### Domain 6 — Cloud & Container Security (5 questions)

[Q24-Q28]

### Domain 7 — Compliance Automation (4 questions)

[Q29-Q32]

### Domain 8 — Operations & Incident Response (5 questions)

[Q33-Q37]

## Scoring methodology

1. Each question is answered with a Level 1–5 by the respondent (or assessor).
2. Domain score = average of question scores in that domain (rounded to nearest 0.5).
3. Overall TDMM score = weighted average across domains (default: equal weight).
4. Gap analysis identifies the domains with largest distance to target state.

## Interpreting scores

| Overall score | Profile |
|---|---|
| 1.0 – 1.9 | Early-stage; foundational work needed across most domains |
| 2.0 – 2.9 | Repeatable; emerging program; tactical wins available |
| 3.0 – 3.9 | Defined program; standardization complete; metrics emerging |
| 4.0 – 4.9 | Measured; quantitatively managed; industry-typical for regulated environments |
| 5.0 | Optimizing; reference-class; rare in industry |

## Use in benchmarking

See `docs/BENCHMARKING_NOTES.md` for observations on typical baselines in different industries.

## Reference

This instrument is published as part of the TechStream framework portfolio at https://github.com/sotille/devsecops-maturity-model. It is released under Apache 2.0 and may be used by any organization at no cost. The methodology is documented in the April 2026 Medium article "The 4-Phase DevSecOps Transformation: A 90-Day Journey from Policy to Practice."
