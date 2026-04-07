# Domain Remediation Playbooks: Advancing Between Maturity Levels

This document provides actionable remediation guidance for each of the eight DevSecOps maturity domains. For each domain, it specifies exactly what actions to take to advance from one level to the next. Use the [Assessment Scorecard](assessment-scorecard.md) to determine your current level in each domain, then apply the corresponding playbook below.

Each advancement section answers: *What specifically must change — in tooling, process, culture, and measurement — to demonstrate the next level of capability?*

---

## Domains Covered

1. [Culture & Organization](#domain-1-culture--organization)
2. [Security Requirements](#domain-2-security-requirements)
3. [Secure Development](#domain-3-secure-development)
4. [CI/CD Security](#domain-4-cicd-security)
5. [Testing & Validation](#domain-5-testing--validation)
6. [Infrastructure Security](#domain-6-infrastructure-security)
7. [Operations & Monitoring](#domain-7-operations--monitoring)
8. [Governance & Compliance](#domain-8-governance--compliance)

---

## Domain 1: Culture & Organization

### Level 1 → Level 2

**Target:** Establish a security champion network and formalize basic security education.

**Required Actions:**

| Action | Owner | Effort | Evidence |
|--------|-------|--------|----------|
| Identify at least one security champion per engineering team (minimum 20% time) | CISO / Engineering VPs | 1–2 weeks to nominate | Champion roster with team mapping |
| Launch annual security awareness training with completion tracking | Security Team | 2–4 weeks to deploy | Training platform with completion rates |
| Create a security consultation mechanism (office hours, Slack channel, ticket queue) | Security Team | 1 week | Documented consultation process and SLAs |
| Establish security onboarding module for new engineers | Security + Engineering Enablement | 3–4 weeks | Onboarding curriculum, completion records |
| Report security metrics to leadership monthly (even if immature) | Security Lead | Ongoing | Monthly security report template |

**Key Behavioral Milestone:** At least one engineering team can describe what their security champion does and has used the consultation mechanism at least once.

---

### Level 2 → Level 3

**Target:** Security champions are empowered, trained, and integrated into the development process. Security culture extends beyond the security team.

**Required Actions:**

| Action | Owner | Effort | Evidence |
|--------|-------|--------|----------|
| Formal security champion program: dedicated time (≥20%), training budget, community of practice | Security + HR | 4–6 weeks to formalize | Champion program charter, training records |
| Champions conduct security design reviews for features in their team — not just security team reviews | Security Champions | Ongoing | Design review records showing champion involvement |
| Champions perform first-pass triage of SAST/SCA findings before escalation | Security Champions | Process change | Triage records, finding lifecycle tracking |
| Role-specific security training for developers (OWASP Top 10), QA (security testing), and ops (infrastructure hardening) | Security + Learning & Dev | 4–8 weeks | Training completion by role |
| Security KPIs visible in engineering team dashboards (not just security team) | Platform + Security | 2–3 weeks | Dashboard screenshots |

**Key Behavioral Milestone:** Engineering teams proactively ask security champions for guidance rather than waiting for security team reviews.

---

### Level 3 → Level 4

**Target:** Security is measurably embedded across all engineering teams. Security metrics drive engineering decisions.

**Required Actions:**

| Action | Owner | Effort | Evidence |
|--------|-------|--------|----------|
| All engineering teams have active, trained security champions meeting defined engagement standards | Security Lead | Ongoing | Quarterly champion effectiveness reviews |
| Security champions contribute to threat models — they do not just review them | Security Champions | Process change | Threat model authorship records |
| Security metrics included in engineering team OKRs or equivalent (MTTD, MTTR, vulnerability density) | Engineering VPs + Security | Planning cycle | OKR documentation |
| Security data used to identify systemic training needs (vulnerability patterns drive curriculum updates) | Security + L&D | Ongoing | Training content updates tied to finding patterns |
| Gamification or recognition for security champion contributions | Engineering Culture | 2–4 weeks | Recognition program documentation |

---

### Level 4 → Level 5

**Target:** Security culture is self-sustaining and continuously improving. Engineering teams drive security innovation.

**Required Actions:**

| Action | Owner | Effort | Evidence |
|--------|-------|--------|----------|
| Engineering teams identify and propose security improvements without security team prompting | Engineering Teams | Cultural | Innovation log showing engineer-driven improvements |
| Security champions mentor other engineers — informal security knowledge sharing is routine | Security Champions | Cultural | Internal security talks, brown bags, documentation contributions |
| Security lessons from incidents are systematically incorporated into training within 30 days | Security + L&D | Process | Post-incident training update records |
| Security team transitions from reviewer/controller role to advisor/enabler role | CISO + Engineering | Cultural | Security team workload analysis showing shift |

---

## Domain 2: Security Requirements

### Level 1 → Level 2

**Target:** Security requirements are documented for new systems and significant features.

**Required Actions:**

| Action | Owner | Effort | Evidence |
|--------|-------|--------|----------|
| Create a security requirements template (functional + non-functional security requirements) | Security Architect | 1–2 weeks | Template in use for new projects |
| Mandate threat modeling for all new systems with > [X] users or > [Y] data sensitivity | Security Architect | Process change | Threat model records for qualifying projects |
| Include security acceptance criteria in the definition of done for affected teams | Security + Engineering | 1 sprint | Updated definition of done in team documentation |
| Identify a security architect or senior engineer for design review consultation | Security Lead | 1 week | Named role, contact information, SLA |
| Define abuse cases for all authentication, authorization, and payment features | Security + Product | Per-feature | Abuse case documentation in user stories |

---

### Level 2 → Level 3

**Target:** Threat modeling is universal, integrated into the design phase for all significant changes.

**Required Actions:**

| Action | Owner | Effort | Evidence |
|--------|-------|--------|----------|
| Threat modeling is required for all new services, major features, and integrations — not just high-risk ones | Security + Engineering | Process change | Threat model coverage metric |
| Engineers (not just security team) can lead threat modeling sessions using a defined methodology (STRIDE, PASTA, or equivalent) | Security | Training program | Engineer-led threat model records |
| Security requirements are tracked to completion — open security requirements block release | Product + Security | Process change | Security requirement closure rate metric |
| Privacy impact assessments (PIAs) integrated with threat modeling for features handling personal data | Privacy / DPO + Security | Process change | PIA records for personal data features |
| Security requirements coverage metric: % of features with documented security requirements > 80% | Security | Ongoing | Dashboard metric |

---

### Level 3 → Level 4

**Target:** Security requirements are quantified and their effectiveness measured.

**Required Actions:**

| Action | Owner | Effort | Evidence |
|--------|-------|--------|----------|
| Threat model effectiveness measured: % of production vulnerabilities that should have been caught by threat modeling | Security | Ongoing | Threat model quality metric |
| Feedback loop: production vulnerabilities trigger review and update of the threat model that should have caught them | Security | Process | Threat model revision records |
| Security requirements coverage approaches 100% for all non-trivial changes | Security | Ongoing | Coverage metric > 95% |
| Threat modeling integrated with design documents in the project management system | Platform + Security | 2–4 weeks | Automated linking between design docs and threat models |

---

## Domain 3: Secure Development

### Level 1 → Level 2

**Target:** Automated SAST and dependency scanning operational in all pipelines with findings visible to developers.

**Required Actions:**

| Action | Owner | Effort | Evidence |
|--------|-------|--------|----------|
| Deploy SAST tool in all production-bound CI pipelines (Semgrep, CodeQL, Checkmarx) | Platform / DevOps | 2–4 weeks | Pipeline configuration with SAST step |
| Deploy dependency vulnerability scanning (Dependabot, Renovate, OWASP Dependency-Check, Grype) | Platform / DevOps | 1–2 weeks | SCA findings visible in developer PRs |
| Establish finding remediation SLAs: Critical: 7 days, High: 30 days, Medium: 90 days | Security + Engineering | Policy change | SLA policy document |
| Deploy secrets detection (TruffleHog, Gitleaks) as a pre-commit hook and in CI | Platform + Security | 1–2 weeks | Secrets detection in all repos |
| Establish a secure coding standard and make it accessible (intranet, IDE plugin) | Security | 2–4 weeks | Secure coding standard document, adoption evidence |

---

### Level 2 → Level 3

**Target:** Security gates enforce quality — high-severity findings block promotion to production.

**Required Actions:**

| Action | Owner | Effort | Evidence |
|--------|-------|--------|----------|
| SAST: Critical and High findings block the build (not just report) | Platform + Security | 1–2 weeks | Build gate configuration, pass/fail evidence |
| SCA: Critical vulnerabilities block promotion to staging and production | Platform + Security | 1–2 weeks | Promotion gate configuration |
| Secrets detection: any committed secret blocks the PR | Platform + Security | 1 week | Pre-commit and CI gate configuration |
| SAST ruleset tuned to reduce false positives to < 20% (review per-repo baselines) | Security | 4–8 weeks | False positive rate metric |
| SAST findings tracked to closure — no backlog older than policy SLA | Security + Engineering | Ongoing | Finding age distribution report |
| Vulnerability density metric tracked per team and per service | Security | Ongoing | Dashboard metric |

---

### Level 3 → Level 4

**Target:** Security tooling generates measurable data that drives quality improvement decisions.

**Required Actions:**

| Action | Owner | Effort | Evidence |
|--------|-------|--------|----------|
| SAST findings per 1000 lines of code trending downward quarter-over-quarter | Security + Engineering | Ongoing | Trend analysis report |
| False positive rate below 10% (active ruleset tuning and custom rules per language) | Security | Ongoing | FP rate metric |
| Security findings feeding into developer IDEs (Semgrep LSP, SonarLint) for shift-left feedback | Platform | 2–4 weeks | IDE plugin deployment evidence |
| SBOM generated for every build and stored with the artifact | Platform | 1–2 weeks | SBOM presence in registry, Cosign attestation |
| Dependency update automation (Dependabot/Renovate) with auto-merge for patch-level security fixes | Platform | 1–2 weeks | Automated PR closure rate for security patches |

---

## Domain 4: CI/CD Security

### Level 1 → Level 2

**Target:** Eliminate secrets in code; basic pipeline access controls.

**Required Actions:**

| Action | Owner | Effort | Evidence |
|--------|-------|--------|----------|
| Remove all secrets from repositories and environment files — migrate to a secrets manager | Platform + Security | 2–6 weeks (repo-by-repo) | Secrets scan shows zero hardcoded secrets |
| Implement branch protection: require PR reviews before merge to main | Platform / Engineering Leads | 1 week | Branch protection configuration |
| CI/CD service accounts use scoped credentials — not admin credentials | Platform | 2–4 weeks | IAM policy review for CI service accounts |
| All CI runs produce logs that are retained for 90+ days | Platform | 1 week | Log retention configuration |
| Pipeline configurations are version-controlled and not modifiable outside of code review | Platform | Process | Pipeline-as-code in protected branch |

---

### Level 2 → Level 3

**Target:** OIDC-based keyless authentication; signed artifacts; comprehensive pipeline security.

**Required Actions:**

| Action | Owner | Effort | Evidence |
|--------|-------|--------|----------|
| Migrate CI cloud authentication to OIDC federation (no long-lived cloud credentials in CI) | Platform | 2–4 weeks | Zero long-lived cloud credentials in CI |
| Implement artifact signing with Cosign/Sigstore for all production-bound artifacts | Platform | 2–4 weeks | Cosign signature present on all images |
| Generate and attach SLSA provenance attestations for all builds | Platform | 1–2 weeks | SLSA provenance attestation in registry |
| Enforce artifact signature verification in deployment admission (Kyverno, OPA) | Platform + Security | 2–4 weeks | Admission policy configuration |
| All GitHub Actions/pipeline actions pinned to full SHA digests | Platform | 1–2 weeks | Actionlint or Semgrep rule enforcing pinning |
| CODEOWNERS configured for pipeline configuration files | Platform | 1 day | CODEOWNERS file in repositories |

---

### Level 3 → Level 4

**Target:** Pipeline security is measured, optimized, and continuously validated.

**Required Actions:**

| Action | Owner | Effort | Evidence |
|--------|-------|--------|----------|
| Pipeline security control effectiveness metrics collected (gate pass/fail rates, secret detection hit rate) | Platform + Security | 2 weeks | Security metrics dashboard |
| SLSA Level 3 compliance achieved: hermetic builds, non-falsifiable provenance | Platform | 4–8 weeks | SLSA Level 3 attestation |
| Automated pipeline security tests (test that gates fail when they should) | Platform + Security | 2–4 weeks | Security test suite with passing evidence |
| Regular pipeline security reviews: quarterly audit of all pipeline permissions and configurations | Security | Ongoing | Quarterly audit records |

---

## Domain 5: Testing & Validation

### Level 1 → Level 2

**Target:** Regular vulnerability scanning; initial DAST deployment.

**Required Actions:**

| Action | Owner | Effort | Evidence |
|--------|-------|--------|----------|
| Annual internal penetration test (not just external) with tracked remediation | Security | Annual | Pentest reports, remediation tracking |
| DAST tool deployed in staging environment (OWASP ZAP, Burp Suite, Nuclei) | Security + Platform | 2–4 weeks | DAST scan results, pipeline configuration |
| Container image scanning before promotion to staging | Platform + Security | 1–2 weeks | Image scan results in pipeline |
| Security regression test: every fixed security vulnerability has a test to prevent recurrence | Security + Engineering | Process | Security regression test suite |
| Infrastructure scanning (Checkov, tfsec, Prowler) for IaC security issues | Platform + Security | 1–2 weeks | IaC scan results |

---

### Level 2 → Level 3

**Target:** Security testing is automated, continuous, and integrated into the delivery pipeline.

**Required Actions:**

| Action | Owner | Effort | Evidence |
|--------|-------|--------|----------|
| DAST runs automatically against every staging deployment | Platform + Security | 2–4 weeks | Automated DAST in pipeline configuration |
| DAST findings classified and acted upon with the same SLAs as SAST findings | Security | Process change | DAST finding lifecycle records |
| API security testing (OWASP API Top 10) integrated into the test suite | Security + Engineering | 4–6 weeks | API security test results |
| Container and Kubernetes workload runtime security scanning (Trivy, Falco) | Platform + Security | 2–4 weeks | Runtime scan evidence |
| Security test coverage metric tracked: % of OWASP Top 10 controls tested | Security | Ongoing | Coverage dashboard |

---

### Level 3 → Level 4

**Target:** Security testing effectiveness measured; feedback loop to security requirements.

**Required Actions:**

| Action | Owner | Effort | Evidence |
|--------|-------|--------|----------|
| Pentest finding recurrence rate tracked (measure whether fixed issues reappear) | Security | Ongoing | Recurrence metric |
| Continuous attack simulation (BAS — Breach and Attack Simulation) for production environment | Security | Large effort | BAS tool deployment and results |
| Adversarial simulation exercises (purple team exercises) at least annually | Security | Annual | Exercise records, findings, remediation |
| Security testing findings feeding back into threat model updates | Security | Process | Cross-reference records |

---

## Domain 6: Infrastructure Security

### Level 1 → Level 2

**Target:** IaC for infrastructure; basic cloud security controls enabled.

**Required Actions:**

| Action | Owner | Effort | Evidence |
|--------|-------|--------|----------|
| All new infrastructure defined as code (Terraform, CloudFormation, Pulumi) | Platform | Process change | IaC coverage metric for new deployments |
| IaC security scanning (Checkov, tfsec) integrated into CI with critical findings blocking deployment | Platform + Security | 1–2 weeks | IaC scan gate in pipeline |
| Cloud security baselines enabled: GuardDuty (AWS), Defender for Cloud (Azure), SCC (GCP) | Cloud / Platform | 1–2 weeks | Service enablement evidence |
| CIS Benchmark baseline defined and measured for primary cloud provider | Security | 2–4 weeks | CIS Benchmark scan results |
| No default VPCs in use; all workloads in custom VPCs with defined network segmentation | Platform | 2–6 weeks | Network architecture documentation |
| Encryption at rest enabled for all data stores | Platform | 2–4 weeks | Encryption configuration evidence |

---

### Level 2 → Level 3

**Target:** IaC is the exclusive deployment mechanism; cloud security posture continuously monitored.

**Required Actions:**

| Action | Owner | Effort | Evidence |
|--------|-------|--------|----------|
| Existing infrastructure remediated to IaC (not just new infrastructure) | Platform | Large effort | 100% IaC coverage for production |
| Drift detection: manual infrastructure changes detected and auto-reverted or flagged | Platform + Security | 2–4 weeks | Drift detection alerts, auto-remediation evidence |
| CSPM tool deployed (Prowler, Wiz, Orca, Lacework) with continuous scanning | Security + Platform | 2–4 weeks | CSPM findings dashboard |
| CIS Benchmark compliance score > 80% for primary cloud provider | Platform + Security | 4–8 weeks | Benchmark scan results |
| Secrets Manager used for all credentials — zero credentials in environment variables or parameter files | Platform | 2–6 weeks | Secrets scan, Secrets Manager inventory |
| Kubernetes Pod Security Standards enforced (Restricted profile for production workloads) | Platform + Security | 2–4 weeks | PSA policy configuration, audit logs |

---

### Level 3 → Level 4

**Target:** Infrastructure security measured against targets; automated remediation for common findings.

**Required Actions:**

| Action | Owner | Effort | Evidence |
|--------|-------|--------|----------|
| CSPM findings remediation SLAs defined and tracked | Security | Process | SLA compliance metric |
| Automated remediation for defined low-risk findings (e.g., S3 public access, security group misconfiguration) | Platform + Security | 4–8 weeks | Auto-remediation playbooks, execution logs |
| CIS Benchmark compliance score > 95% | Platform + Security | Ongoing | Benchmark scan trend |
| Vulnerability management for infrastructure: OS patching within 30 days for Critical/High CVEs | Platform | Process | Patch SLA compliance metric |
| Infrastructure security metrics published to engineering team dashboards | Platform + Security | 2 weeks | Dashboard evidence |

---

## Domain 7: Operations & Monitoring

### Level 1 → Level 2

**Target:** Centralized logging; basic alerting; documented incident response process.

**Required Actions:**

| Action | Owner | Effort | Evidence |
|--------|-------|--------|----------|
| Central log aggregation for all production services (application logs, cloud audit logs, access logs) | Platform | 2–4 weeks | Log pipeline configuration, log volume evidence |
| SIEM or equivalent (AWS Security Hub, Splunk, Elastic SIEM) deployed with basic alerting | Security + Platform | 4–6 weeks | SIEM deployment, initial alert rules |
| Incident response plan documented: roles, escalation path, communication plan | Security | 2–4 weeks | IR plan document |
| Incident response tabletop exercise conducted with all key stakeholders | Security | Annual | Exercise records |
| On-call rotation established for security incidents (not just infrastructure incidents) | Security + Engineering | Process | On-call schedule and runbooks |
| Mean Time to Detect (MTTD) baseline established | Security | Ongoing | MTTD metric |

---

### Level 2 → Level 3

**Target:** Threat detection is automated; incident response is practiced and measured.

**Required Actions:**

| Action | Owner | Effort | Evidence |
|--------|-------|--------|----------|
| Detection rules tuned: false positive rate < 30% (team can respond to all alerts) | Security | 4–8 weeks | Alert volume and FP rate metric |
| MTTD for Critical security events < 1 hour | Security | Ongoing | MTTD metric |
| MTTR for Critical security incidents < 4 hours | Security | Ongoing | MTTR metric |
| Incident response playbooks for top 5 incident types (see [cloud-security-devsecops: incident-response-playbooks.md](../../cloud-security-devsecops/docs/incident-response-playbooks.md)) | Security | 2–4 weeks | Playbook documentation |
| Post-incident reviews mandatory for all P1/P2 incidents | Security | Process | Post-mortem database |
| Threat hunting exercises conducted quarterly | Security | Ongoing | Hunt records with findings |

---

### Level 3 → Level 4

**Target:** Security operations are metrics-driven; detection capability continuously improving.

**Required Actions:**

| Action | Owner | Effort | Evidence |
|--------|-------|--------|----------|
| MTTD for Critical events < 15 minutes | Security | Ongoing | MTTD trend |
| MTTR for Critical incidents < 1 hour | Security | Ongoing | MTTR trend |
| Detection coverage mapped to MITRE ATT&CK — coverage gaps documented and addressed | Security | 4–8 weeks | ATT&CK coverage heatmap |
| SOAR (Security Orchestration, Automation, Response) for automated containment of defined incident types | Security + Platform | Large effort | SOAR playbook deployment |
| Alert fatigue metric tracked (% of alerts requiring human review vs. auto-resolved) | Security | Ongoing | Alert disposition metric |

---

## Domain 8: Governance & Compliance

### Level 1 → Level 2

**Target:** Formal security policies; risk register; basic compliance evidence collection.

**Required Actions:**

| Action | Owner | Effort | Evidence |
|--------|-------|--------|----------|
| Security policies reviewed and updated: ISSP, Acceptable Use, Access Control, Incident Response | CISO + Legal | 4–8 weeks | Policy documents with revision dates |
| Risk register established: top 10 organizational security risks identified, scored, and owned | CISO | 2–4 weeks | Risk register |
| Exception management process defined: how to request, approve, and track exceptions to security requirements | CISO + Legal | 2–4 weeks | Exception management process document |
| Compliance framework selected (SOC 2, ISO 27001, etc.) and gap assessment completed | CISO + Legal | 4–6 weeks | Gap assessment report |
| Security KPI reporting cadence established: monthly security metrics to CISO; quarterly to board | CISO | Process | Reporting calendar, sample reports |

---

### Level 2 → Level 3

**Target:** Compliance evidence is continuously collected; policy exceptions are formally governed.

**Required Actions:**

| Action | Owner | Effort | Evidence |
|--------|-------|--------|----------|
| Automated compliance evidence collection for selected framework (Drata, Vanta, or custom tooling) | Security + Platform | 4–8 weeks | Evidence collection coverage metric |
| Policy-as-Code deployed for key controls (OPA, Kyverno, Checkov) | Platform + Security | 4–8 weeks | Policy deployment evidence |
| First compliance audit passed (SOC 2 Type I or equivalent) | CISO | Program milestone | Audit report |
| Exception inventory: all active exceptions in a tracked register with expiry dates and compensating controls | CISO + Security | 2–4 weeks | Exception register |
| Vendor security assessment process: all critical third-party vendors assessed annually | Security + Procurement | 4–6 weeks | Vendor assessment records |

---

### Level 3 → Level 4

**Target:** Compliance is continuous; risk management is quantitative.

**Required Actions:**

| Action | Owner | Effort | Evidence |
|--------|-------|--------|----------|
| SOC 2 Type II or equivalent continuous compliance achieved | CISO | Annual program | Audit reports |
| Compliance coverage metric: % of required controls fully automated > 80% | Security | Ongoing | Automation coverage dashboard |
| Risk quantification: top risks expressed in financial terms (FAIR methodology or equivalent) | CISO + Risk | 4–8 weeks | Quantified risk assessments |
| Compliance drift detection: automated alerts when control status changes | Security + Platform | 2–4 weeks | Drift alert configuration |
| Board-level security reporting: quarterly security risk briefing to board or equivalent | CISO | Ongoing | Board presentation records |

---

### Level 4 → Level 5

**Target:** Governance drives organizational strategy; continuous improvement is systematic.

**Required Actions:**

| Action | Owner | Effort | Evidence |
|--------|-------|--------|----------|
| Security metrics inform product and engineering investment decisions (not just security team decisions) | CISO + Product / Engineering VPs | Cultural | Investment decision records linking to security data |
| Threat intelligence integrated into risk register: emerging threats assessed and risk register updated quarterly | Security | Ongoing | Risk register update records with TI sourcing |
| External peer benchmarking: security program compared against industry benchmarks annually | CISO | Annual | Benchmark study report |
| Security program contributes to industry standards development (public comments, working groups, open source) | CISO + Security Architects | Cultural | Contribution records |

---

## Advancement Measurement Checklist

Use this checklist to validate that a level transition is complete before declaring the advancement:

```
[ ] All "Required Actions" for the target level are complete
[ ] Evidence documented for each action (not self-asserted — verifiable by an auditor)
[ ] Key Behavioral Milestones observed (not just tooling deployed)
[ ] KPI baselines established for the new level
[ ] Assessment Scorecard re-scored to confirm new level assignment
[ ] Transition documented in the organization's DevSecOps program record
```

*A common failure mode is declaring level advancement based on tool deployment without verifying behavioral adoption. A SAST tool in a pipeline that no one triages does not advance you from Level 1 to Level 2 in Secure Development. Evidence of developer engagement with findings is required.*

---

*See also:*
- *[framework.md](framework.md) — Full 5-level, 8-domain framework*
- *[assessment-scorecard.md](assessment-scorecard.md) — Workshop scorecard for current-state assessment*
- *[metrics-kpis.md](metrics-kpis.md) — KPI definitions and measurement guidance*
- *[devsecops-methodology: security-champion-program.md](../../devsecops-methodology/docs/security-champion-program.md) — Security champion program implementation*
