# Benchmarking Notes

These are observations about typical TDMM maturity baselines in different industries, based on practitioner experience across regulated and unregulated environments.

> **Disclaimer:** These are field observations, not formal statistics. Use them as orientation, not as benchmarks for performance evaluation.

## Typical baselines by industry

### Financial Services (Tier-1 banks, payment networks)

- **Typical baseline:** 3.0 – 3.5
- **Strong domains:** Compliance Automation (often 4+), Operations & Incident Response (4+)
- **Weak domains:** Threat Modeling (often 2–3, especially for non-flagship products), Software Supply Chain (3 — SBOM adoption inconsistent)
- **Notable:** Regulatory pressure drives compliance maturity but does not always translate to engineering practice maturity.

### Fintech (Series B+ to public, regulated)

- **Typical baseline:** 2.5 – 3.0
- **Strong domains:** CI/CD Security (3.5+, modern stack), Cloud & Container Security (3.5+)
- **Weak domains:** Strategy & Governance (often 2 — strategy implicit, not written), Compliance Automation (2.5 — manual processes lingering)
- **Notable:** Engineering culture is mature; formal governance lags.

### Healthcare (large hospital systems, payers)

- **Typical baseline:** 2.0 – 2.5
- **Strong domains:** Compliance Automation (3+, HIPAA-driven), Operations & Incident Response (3+)
- **Weak domains:** Secure SDLC (2 — legacy systems dominate), CI/CD Security (2)
- **Notable:** Constrained by legacy platforms and risk-averse change management.

### Federal Contractors

- **Typical baseline:** 2.5 – 3.5 (wide variance)
- **Strong domains:** Compliance Automation (often 4 — FedRAMP-driven), Strategy & Governance (3.5)
- **Weak domains:** Software Supply Chain (2.5 — EO 14028 adoption underway), Threat Modeling (2.5)
- **Notable:** Strong governance maturity; engineering practice catching up.

### Cloud-Native Startups (Series A-B)

- **Typical baseline:** 2.0 – 2.5
- **Strong domains:** CI/CD Security (3+), Cloud & Container Security (3+)
- **Weak domains:** Compliance Automation (1.5 — none), Strategy & Governance (1.5)
- **Notable:** Strong technical practice, weak formalization.

### Enterprise (non-regulated)

- **Typical baseline:** 1.5 – 2.5
- **Strong domains:** Operations & Incident Response (2.5)
- **Weak domains:** Strategy & Governance (1.5 — security is reactive)
- **Notable:** Maturity highly varies by engineering leadership culture.

## Trajectory patterns

In organizations that commit to a 12-month maturity improvement program:

- **Realistic year-1 movement:** +0.5 to +1.0 on overall score
- **Where most progress is made:** Strategy & Governance, CI/CD Security, Compliance Automation
- **Where progress is slowest:** Threat Modeling (requires culture change), Operations & Incident Response (requires investment)

## How to use these notes

When presenting TDMM results to leadership:
- Provide your organization's overall score
- Provide industry-typical baseline for context
- Identify the 2–3 domains where the gap to your target state is largest
- Recommend the first 90-day intervention in those domains (use `docs/PHASE_GATE_CRITERIA.md` from `devsecops-methodology`)
