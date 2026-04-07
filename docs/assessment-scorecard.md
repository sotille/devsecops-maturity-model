# DevSecOps Maturity Assessment Scorecard

This scorecard is a standalone, printable assessment tool derived from the [DevSecOps Maturity Framework](framework.md). It is designed to be completed by a cross-functional team in a 2–4 hour facilitated workshop. The output is a domain-level maturity score and a visual profile that informs roadmap prioritization.

Use the [Implementation Guide](implementation.md) for the full methodology, evidence collection guidance, and reporting templates.

---

## Instructions

1. **Assemble the right participants.** Include at least one representative from engineering, security, operations, and compliance/governance. A facilitated session produces more accurate scores than a self-assessment by a single person.

2. **Score each statement independently.** For each practice statement below, assign a score of 0–4 using the scoring key. Do not average in your head — record each score separately, then calculate domain averages at the end.

3. **Use evidence to justify scores.** A score of 3 or 4 requires observable evidence (tool output, policy document, meeting notes, dashboard screenshot). Scores assigned without evidence should be treated as provisional.

4. **Calibrate within your team.** If participants disagree on a score, use the lower score unless the higher score can be backed by evidence. Conservative scoring is more useful than optimistic scoring.

5. **Calculate totals.** Use the scoring tables at the end of each domain. The final maturity level is determined by the lowest domain score, not the average — a chain is as strong as its weakest link.

---

## Scoring Key

| Score | Label | Meaning |
|-------|-------|---------|
| 0 | Not started | Practice does not exist; not planned |
| 1 | Initial | Attempted informally; inconsistent; no documented process |
| 2 | Managed | Defined and documented; applied on some teams; not org-wide |
| 3 | Defined | Applied consistently across all teams; measurable; enforced |
| 4 | Optimizing | Continuously improved; data-driven; industry-leading execution |

---

## Domain 1: Culture and Organization

| # | Practice Statement | Score (0–4) | Evidence / Notes |
|---|--------------------|-------------|------------------|
| 1.1 | Security is treated as a shared responsibility between development, security, and operations — not solely the security team's job | | |
| 1.2 | A security champions program exists with active participation from development teams | | |
| 1.3 | Security requirements are discussed at project inception, not discovered at the end of delivery | | |
| 1.4 | Blameless post-mortems are conducted for security incidents with documented action items | | |
| 1.5 | Security training relevant to developers' roles is provided at least annually | | |
| 1.6 | Engineering OKRs or KPIs include measurable security objectives | | |

**Domain 1 Total: \_\_\_ / 24**
**Domain 1 Average: \_\_\_ (Total ÷ 6)**

---

## Domain 2: Security Requirements

| # | Practice Statement | Score (0–4) | Evidence / Notes |
|---|--------------------|-------------|------------------|
| 2.1 | Security requirements are defined for new features and user stories as part of the definition of ready | | |
| 2.2 | Abuse cases or misuse cases are identified alongside functional requirements | | |
| 2.3 | A threat modeling process is applied to significant design changes | | |
| 2.4 | Security acceptance criteria are included in the definition of done | | |
| 2.5 | Data classification is applied to all data assets, with handling requirements defined per classification level | | |

**Domain 2 Total: \_\_\_ / 20**
**Domain 2 Average: \_\_\_ (Total ÷ 5)**

---

## Domain 3: Secure Development

| # | Practice Statement | Score (0–4) | Evidence / Notes |
|---|--------------------|-------------|------------------|
| 3.1 | Developers have access to secure coding guidance specific to the languages and frameworks in use | | |
| 3.2 | Security-focused code review is performed on changes involving authentication, authorization, input handling, or sensitive data | | |
| 3.3 | Pre-commit hooks or local developer tools provide immediate feedback on obvious security issues (secrets, lint rules) | | |
| 3.4 | Dependency management policy is documented; direct dependency upgrades occur within a defined SLA | | |
| 3.5 | Developers can self-serve security findings for their own services through a dashboard or portal | | |

**Domain 3 Total: \_\_\_ / 20**
**Domain 3 Average: \_\_\_ (Total ÷ 5)**

---

## Domain 4: CI/CD Security

| # | Practice Statement | Score (0–4) | Evidence / Notes |
|---|--------------------|-------------|------------------|
| 4.1 | SAST runs on every pull request and blocks merges on CRITICAL findings | | |
| 4.2 | SCA (software composition analysis) runs on every build and enforces a vulnerability SLA | | |
| 4.3 | Secrets scanning runs on every commit; detected secrets trigger automatic response procedures | | |
| 4.4 | Container images are scanned before being pushed to the production registry | | |
| 4.5 | All build artifacts are signed and signatures are verified at every promotion gate | | |
| 4.6 | CI/CD credentials use short-lived, scoped tokens (OIDC federation) rather than long-lived service account keys | | |
| 4.7 | Pipeline configurations are stored in version-controlled, protected branches with required code review | | |
| 4.8 | Build runners are ephemeral and isolated per job; no shared state persists between builds | | |

**Domain 4 Total: \_\_\_ / 32**
**Domain 4 Average: \_\_\_ (Total ÷ 8)**

---

## Domain 5: Testing and Validation

| # | Practice Statement | Score (0–4) | Evidence / Notes |
|---|--------------------|-------------|------------------|
| 5.1 | DAST is performed against a running application in a staging environment before each production release | | |
| 5.2 | Infrastructure as Code is scanned for misconfigurations before deployment | | |
| 5.3 | API security testing (including authentication and authorization boundary testing) is part of the test suite | | |
| 5.4 | Security regression tests are written for confirmed vulnerabilities to prevent reintroduction | | |
| 5.5 | Penetration testing or red team exercises are conducted at least annually | | |

**Domain 5 Total: \_\_\_ / 20**
**Domain 5 Average: \_\_\_ (Total ÷ 5)**

---

## Domain 6: Infrastructure Security

| # | Practice Statement | Score (0–4) | Evidence / Notes |
|---|--------------------|-------------|------------------|
| 6.1 | All infrastructure is managed as code; manual console changes to production are prohibited | | |
| 6.2 | CIS Benchmark hardening is applied to all cloud accounts, VMs, and container environments | | |
| 6.3 | Network segmentation separates workloads by trust level; lateral movement requires explicit authorization | | |
| 6.4 | Secrets are stored in a dedicated secrets management system; no secrets in environment variables, config files, or repositories | | |
| 6.5 | Identity and access management follows least privilege; access is reviewed quarterly | | |
| 6.6 | Configuration drift from the declared IaC state is detected and alerted on | | |

**Domain 6 Total: \_\_\_ / 24**
**Domain 6 Average: \_\_\_ (Total ÷ 6)**

---

## Domain 7: Operations and Monitoring

| # | Practice Statement | Score (0–4) | Evidence / Notes |
|---|--------------------|-------------|------------------|
| 7.1 | Security events from all pipeline stages and production systems are collected in a centralized log aggregation system | | |
| 7.2 | Alerting rules exist for known attack patterns (brute force, credential stuffing, privilege escalation, anomalous API calls) | | |
| 7.3 | Mean time to detect (MTTD) for security incidents is tracked and improving | | |
| 7.4 | An incident response playbook exists and is tested at least annually (tabletop or live drill) | | |
| 7.5 | Audit logs are protected from modification; retention policy meets compliance requirements | | |
| 7.6 | Runtime threat detection is deployed in production (host-level, container-level, or network-level) | | |

**Domain 7 Total: \_\_\_ / 24**
**Domain 7 Average: \_\_\_ (Total ÷ 6)**

---

## Domain 8: Governance and Compliance

| # | Practice Statement | Score (0–4) | Evidence / Notes |
|---|--------------------|-------------|------------------|
| 8.1 | A defined set of security policies exists and is reviewed at least annually | | |
| 8.2 | Compliance requirements (SOC 2, PCI-DSS, ISO 27001, etc.) are mapped to specific technical controls | | |
| 8.3 | Compliance evidence collection is automated; manual evidence gathering for audits takes less than one week | | |
| 8.4 | Risk exceptions are documented, time-bounded, and reviewed by an accountable owner | | |
| 8.5 | Security metrics are reported to leadership on a regular cadence (quarterly or more frequent) | | |

**Domain 8 Total: \_\_\_ / 20**
**Domain 8 Average: \_\_\_ (Total ÷ 5)**

---

## Score Summary

| Domain | Max Score | Your Total | Your Average | Maturity Level |
|--------|-----------|------------|--------------|----------------|
| 1. Culture and Organization | 24 | | | |
| 2. Security Requirements | 20 | | | |
| 3. Secure Development | 20 | | | |
| 4. CI/CD Security | 32 | | | |
| 5. Testing and Validation | 20 | | | |
| 6. Infrastructure Security | 24 | | | |
| 7. Operations and Monitoring | 24 | | | |
| 8. Governance and Compliance | 20 | | | |
| **Overall** | **184** | | | |

**Maturity level per domain average:**

| Average | Maturity Level |
|---------|----------------|
| 0.0 – 0.9 | Level 1 — Initial |
| 1.0 – 1.9 | Level 2 — Managed |
| 2.0 – 2.9 | Level 3 — Defined |
| 3.0 – 3.4 | Level 4 — Quantitatively Managed |
| 3.5 – 4.0 | Level 5 — Optimizing |

**Overall organizational maturity level = lowest individual domain level**

---

## Maturity Profile Chart

Plot your domain averages on the radar chart below (or recreate it in your preferred diagramming tool). A balanced profile — where no domain lags far behind the others — indicates a well-rounded program. A spiked profile indicates overinvestment in one area at the expense of others.

```
                 Culture & Org (1)
                       │
                    4  │
                    3  │
  Governance (8)─ ─ 2  ─ ─ Security Req (2)
                    1  │
                    0  │
    Ops & Monitor (7)──┼──Secure Dev (3)
                       │
  Infra Security (6)─ ─ ─ ─CI/CD Security (4)
                       │
               Testing & Valid (5)
```

For a digital version, paste your domain averages into a radar chart tool using these domain names in order:
`Culture & Org, Security Requirements, Secure Development, CI/CD Security, Testing & Validation, Infrastructure Security, Operations & Monitoring, Governance & Compliance`

---

## Interpreting Results

### Your program is balanced if:
- No domain average is more than 1.5 points below the highest domain average
- All domains are at Level 2 or above before investing in Level 4/5 practices in any single domain

### Prioritize investments if:
- Domain 4 (CI/CD Security) or Domain 6 (Infrastructure Security) scores below 2.0 — these represent the highest risk exposure
- Domain 7 (Operations & Monitoring) scores below 1.5 — the ability to detect and respond to incidents is foundational
- Domain 8 (Governance & Compliance) scores below 2.0 and you are subject to compliance frameworks

### Common patterns:
| Profile Pattern | What It Means | Recommended Focus |
|-----------------|--------------|-------------------|
| High Culture, Low CI/CD | Good intentions, poor technical execution | Invest in toolchain and pipeline automation |
| High CI/CD, Low Culture | Tools-first adoption without organizational change | Security champions, training, blameless post-mortems |
| High Governance, Low Testing | Compliance-driven program without real security outcomes | DAST, penetration testing, security regression suites |
| Uniformly Low | Early-stage or legacy program | Start with quick wins: secrets scanning, SCA, IaC scanning |
| High everywhere except one domain | Mature program with a known gap | Target investment to close the specific gap |

---

## Worked Examples

These three profiles illustrate what scored assessments look like at different maturity stages. Use them to calibrate your team's scoring and to understand what a domain score means in practice.

### Profile A: Early-Stage SaaS Company (Level 2 — Managed)

A 40-person SaaS company, 3 years old, AWS + GitHub Actions. Has been running SAST and SCA for 6 months but adoption is inconsistent. No dedicated security engineer. One engineer acts as an informal champion.

| Domain | Total | Average | Level | Key Evidence |
|--------|-------|---------|-------|--------------|
| 1. Culture and Organization | 11 / 24 | 1.8 | L2 | Security responsibility informally shared; no formal champions program; one post-mortem run in past year |
| 2. Security Requirements | 7 / 20 | 1.4 | L2 | Security requirements occasionally discussed; no formal abuse cases or threat models |
| 3. Secure Development | 9 / 20 | 1.8 | L2 | SAST runs on main branch but not PRs; some pre-commit hooks; SCA runs weekly, not on every PR |
| 4. CI/CD Security | 13 / 32 | 1.6 | L2 | SAST and SCA on CI; no artifact signing; credentials are long-lived IAM keys; runners not ephemeral |
| 5. Testing and Validation | 5 / 20 | 1.0 | L1 | No DAST; IaC not scanned; no API security testing; pen test was 18 months ago |
| 6. Infrastructure Security | 12 / 24 | 2.0 | L3 | IaC used for most infra; GuardDuty enabled; no CIS benchmark hardening; drift not detected |
| 7. Operations and Monitoring | 8 / 24 | 1.3 | L2 | CloudTrail enabled; no SIEM alerting; no IR playbook; MTTD unknown |
| 8. Governance and Compliance | 6 / 20 | 1.2 | L2 | Basic security policy exists; no compliance mapping; evidence collection manual |
| **Overall** | **71 / 184** | **1.4** | **L2** | |

**Determined by lowest domain: Domain 5 (Testing and Validation) at Level 1.**

**Interpretation:** A solid starting position for an early-stage company. The tool adoption in CI/CD is ahead of the culture and governance that should surround it (AP-O3 anti-pattern risk). Priority investments: migrate CI/CD credentials to OIDC (Domain 4 quick win), add automated DAST to staging pipeline (Domain 5 critical gap), establish a formal SLA for vulnerability remediation (Domain 3/4 gap).

---

### Profile B: Scale-Up Engineering Organization (Level 3 — Defined)

A 250-person B2B SaaS company, Series C, multi-cloud (AWS primary, Azure secondary). Two dedicated application security engineers. Active security champions program with 12 champions across 15 teams. SOC 2 Type II certified.

| Domain | Total | Average | Level | Key Evidence |
|--------|-------|---------|-------|--------------|
| 1. Culture and Organization | 19 / 24 | 3.2 | L4 | Champions program active; security OKRs in engineering; blameless post-mortems standard |
| 2. Security Requirements | 15 / 20 | 3.0 | L4 | Threat modeling on significant features; security acceptance criteria in Definition of Done |
| 3. Secure Development | 15 / 20 | 3.0 | L4 | Developer security dashboard; pre-commit hooks enforced; SAST on every PR with CRITICAL gate |
| 4. CI/CD Security | 22 / 32 | 2.75 | L3 | SAST, SCA, container scan on all PRs; OIDC adopted; runners ephemeral; signing not yet implemented |
| 5. Testing and Validation | 13 / 20 | 2.6 | L3 | DAST on staging; IaC scanning; API security testing in test suite; pen test annually |
| 6. Infrastructure Security | 19 / 24 | 3.2 | L4 | CIS benchmark enforced; all infra as code; drift detection active; quarterly access reviews |
| 7. Operations and Monitoring | 16 / 24 | 2.7 | L3 | SIEM deployed; alerting for key patterns; IR playbook exists; MTTD tracked (avg 4.2 hours) |
| 8. Governance and Compliance | 16 / 20 | 3.2 | L4 | SOC 2 Type II; automated evidence collection; risk exceptions tracked |
| **Overall** | **135 / 184** | **2.9** | **L3** | |

**Determined by overall average (2.9) mapping to L3; no domain below L3.**

**Interpretation:** A well-rounded program with genuine strengths. The absence of artifact signing (Domain 4: practice 4.5) is the standout gap at this maturity level — signing is now expected for Level 4 pipeline security. Priority investments: implement Cosign artifact signing and SBOM generation (Domain 4 gap closing); invest in reducing MTTD to < 1 hour (Domain 7 improvement for Level 4 readiness).

---

### Profile C: Enterprise Financial Services (Level 4 — Quantitatively Managed)

A 2,000-engineer financial services firm, publicly traded, AWS + Azure, regulated under PCI-DSS v4.0 and SOC 2. Dedicated security platform team (8 engineers), 40+ security champions, automated compliance evidence pipeline.

| Domain | Total | Average | Level | Key Evidence |
|--------|-------|---------|-------|--------------|
| 1. Culture and Organization | 22 / 24 | 3.7 | L5 | Champions program mature; security OKRs enforced; regular blameless post-mortems; security town halls |
| 2. Security Requirements | 18 / 20 | 3.6 | L5 | Threat modeling on all significant changes; automated abuse case generation from threat models |
| 3. Secure Development | 18 / 20 | 3.6 | L5 | Self-serve security dashboard; pre-commit enforced org-wide; AI-assisted secure code review guidance |
| 4. CI/CD Security | 30 / 32 | 3.75 | L5 | All controls in place; Cosign signing; SBOM with fleet query capability; OIDC 100%; zero long-lived credentials |
| 5. Testing and Validation | 18 / 20 | 3.6 | L5 | DAST on all staging deploys; API security testing; pen test + red team annually; security regression suite |
| 6. Infrastructure Security | 22 / 24 | 3.7 | L5 | Full IaC; drift detected and auto-remediated in non-production; CIS benchmark 95%+ pass rate |
| 7. Operations and Monitoring | 20 / 24 | 3.3 | L4 | SIEM fully deployed; MTTD < 45 minutes; IR playbook tested annually; runtime threat detection deployed |
| 8. Governance and Compliance | 18 / 20 | 3.6 | L5 | PCI-DSS + SOC 2; automated evidence; compliance dashboard; exception SLA < 15 days |
| **Overall** | **166 / 184** | **3.6** | **L4/5** | |

**Determined by Domain 7 (Operations and Monitoring) at L4; all other domains at L5.**

**Interpretation:** An industry-leading program. The remaining gap is in the operations domain — specifically, reducing MTTD further (currently 45 minutes, target < 15 minutes for L5 Pipeline anomaly detection) and moving toward continuous threat hunting (currently monthly, L5 target is continuous). Priority investment: advanced behavioral analytics in SIEM to enable continuous automated threat hunting in CI/CD audit logs.

---

## Next Steps

After completing this scorecard:

1. **Record the date.** Re-run this assessment in 6 months to measure progress.
2. **Map gaps to roadmap items.** Use the [Implementation Guide](implementation.md) to build a prioritized roadmap.
3. **Identify quick wins.** Practices scoring 1 in domains scoring below average are typically the easiest to improve first.
4. **Share results with leadership.** Use the domain radar chart to communicate the program posture in executive briefings.
5. **Cross-reference with framework selection.** Use the [Framework Selection Guide](../../techstream-docs/docs/framework-selection-guide.md) to identify which Techstream frameworks address your lowest-scoring domains.

---

## Related Documents

- [Maturity Framework](framework.md) — Full five-level model with domain-by-domain capability descriptions
- [Implementation Guide](implementation.md) — Full assessment methodology, evidence collection guidance, and reporting templates
- [DevSecOps Methodology](../../devsecops-methodology/docs/implementation.md) — 90-day transformation playbook
