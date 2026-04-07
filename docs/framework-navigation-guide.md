# Assessment-to-Framework Navigation Guide

The DevSecOps Maturity Model produces a quantitative assessment of your organization's current security capability across eight domains and five levels. That assessment is only valuable if it drives concrete action. This guide translates assessment scores into specific implementation guidance — pointing to the exact documents, sections, and practices in the Techstream framework ecosystem that address each gap.

Use this guide immediately after completing an assessment to convert your scorecard into a prioritized reading and implementation list.

---

## How to Use This Guide

1. Complete the [Assessment Scorecard](assessment-scorecard.md) for all eight domains
2. For each domain where you scored below your target level, find that domain in this guide
3. Read the "What this score means" interpretation
4. Follow the recommended actions and linked documents in priority order
5. Use the [Remediation Playbooks](remediation-playbooks.md) for step-by-step advancement guidance within each domain

---

## Domain 1: Culture and Organization

### Score Interpretation

| Your Score | Meaning | Next Focus |
|------------|---------|-----------|
| L1 (Initial) | Security is reactive; developers do not consider security their responsibility; no security champions | Establish shared responsibility model and minimal security awareness |
| L2 (Managed) | Some security awareness; ad hoc security champions; security training exists but inconsistent | Formalize security champion program; standardize training |
| L3 (Defined) | Security champions active in all teams; training curriculum defined; security included in planning | Scale champion program; integrate security into performance goals |
| L4 (Quantitative) | Security culture measured via metrics; champion effectiveness tracked; executive visibility | Advance to developer-led security with metrics driving improvement |
| L5 (Optimizing) | Developers proactively identify and fix security issues; security team focuses on enabling, not policing | Continuous improvement; blameless postmortems; industry contribution |

### L1 → L2 Action Set

**Read first:**
- [DevSecOps Framework: Introduction](../../devsecops-framework/docs/introduction.md) — The "why" of DevSecOps; foundational vocabulary for all team members
- [DevSecOps Methodology: Introduction](../../devsecops-methodology/docs/introduction.md) — Why transformations fail and the principles behind successful programs
- [DevSecOps Methodology: Resistance Management](../../devsecops-methodology/docs/resistance-management.md) — How to address team resistance to security adoption

**Key actions:**
- Identify one security champion per team (even informally)
- Run a 2-hour DevSecOps foundations workshop using the DevSecOps Framework introduction as the curriculum
- Define a shared incident postmortem template to begin the blameless culture

### L2 → L3 Action Set

**Read first:**
- [DevSecOps Methodology: Security Champion Program](../../devsecops-methodology/docs/security-champion-program.md) — Full program design including roles, incentives, training, and success metrics
- [DevSecOps Framework: Developer Experience](../../devsecops-framework/docs/developer-experience.md) — How to reduce friction so developers adopt security willingly

**Key actions:**
- Formalize the security champion role with documented responsibilities and time allocation
- Create a security champion community of practice with regular meetings
- Integrate security discussion into sprint retrospectives

### L3 → L4 Action Set

**Read first:**
- [DevSecOps Maturity Model: Metrics and KPIs](metrics-kpis.md) — Culture metrics including champion engagement rate, training completion, developer acknowledgment time
- [DevSecOps Framework: Roadmap](../../devsecops-framework/docs/roadmap.md) — Quarterly milestone targets for culture metrics

**Key actions:**
- Establish security OKRs that include all engineering teams, not just the security team
- Track and publish security champion program effectiveness metrics quarterly

---

## Domain 2: Security Requirements

### Score Interpretation

| Your Score | Meaning | Next Focus |
|------------|---------|-----------|
| L1 | Security requirements are absent from sprint planning; no threat modeling | Begin lightweight threat modeling practice |
| L2 | Security requirements defined for some high-risk features; informal threat modeling | Standardize threat modeling methodology |
| L3 | Threat modeling required for all significant features; security user stories in backlogs | Integrate security requirements into definition of done |
| L4 | Threat model coverage measured; abuse cases tracked; security requirements as code | Automate requirements validation |
| L5 | Continuous threat model refresh; requirements linked to controls; automated abuse scenario testing | AI-assisted threat model analysis |

### L1 → L2 Action Set

**Read first:**
- [DevSecOps Framework: Framework — Security Requirements Phase](../../devsecops-framework/docs/framework.md) — The Plan phase security activities including threat modeling basics
- [DevSecOps Framework: API Security](../../devsecops-framework/docs/api-security.md) — API threat modeling checklist (applicable pattern for any service)

**Key actions:**
- Adopt the STRIDE methodology for threat modeling (1-page format to start)
- Require a threat model for all new services and significant feature additions
- Create a library of security user stories for common patterns (authentication, authorization, input handling)

### L2 → L3 Action Set

**Read first:**
- [DevSecOps Framework: Implementation — Phase 1](../../devsecops-framework/docs/implementation.md) — Prerequisites assessment and security requirements integration
- [DevSecOps Methodology: Framework](../../devsecops-methodology/docs/framework.md) — How to embed security requirements into Agile ceremonies

---

## Domain 3: Secure Development

### Score Interpretation

| Your Score | Meaning | Next Focus |
|------------|---------|-----------|
| L1 | No secure coding standards; no SAST; security found in penetration tests only | Deploy basic SAST |
| L2 | Some SAST in place; inconsistent standards across teams | Standardize SAST toolchain; establish secure coding standards |
| L3 | SAST integrated in CI with mandatory gates; secure coding standards documented and trained | Tune SAST rulesets; add IDE integration |
| L4 | SAST tuned to low false positive rate; developer IDE integration; metrics on finding resolution time | Differential scanning; advanced SAST rules for custom business logic |
| L5 | Developers catch security issues before commit; SAST continuously improved with new attack pattern data | Semantic code analysis; AI-assisted secure code suggestions |

### L1 → L2 Action Set

**Read first:**
- [Secure Pipeline Templates: Introduction](../../secure-pipeline-templates/docs/introduction.md) — Threat model and rationale for each security stage
- [Secure Pipeline Templates: Framework — Stage 3 SAST](../../secure-pipeline-templates/docs/framework.md) — Semgrep configuration, severity mapping, failure criteria

**Implement first:**
- Deploy `secure-pipeline-templates` GitHub Actions template (or equivalent) — this gives you SAST, SCA, and secrets scanning in a single workflow file

### L2 → L3 Action Set

**Read first:**
- [DevSecOps Framework: Developer Experience](../../devsecops-framework/docs/developer-experience.md) — Reducing false positives; making findings actionable; IDE integration
- [DevSecOps Framework: Best Practices — Code Security](../../devsecops-framework/docs/best-practices.md) — Practices 8-13 covering secure coding standards, code review, input validation

**Implement:**
- Configure SAST gate in CI to fail builds on CRITICAL and HIGH severity findings
- Add Semgrep or SonarLint to IDE setup guide for developers
- Define secure coding standards document (input validation, output encoding, parameterized queries, error handling)

### L3 → L4 Action Set

**Read first:**
- [DevSecOps Framework: Developer Experience — Reduce False Positives](../../devsecops-framework/docs/developer-experience.md) — Measuring and reducing false positive rate; tuning SAST rulesets

**Key metric:** Measure false positive rate monthly. Target: < 20% FP rate.

---

## Domain 4: CI/CD Security

### Score Interpretation

| Your Score | Meaning | Next Focus |
|------------|---------|-----------|
| L1 | CI exists but has no security controls; admin credentials shared; no secrets management | Remove shared credentials; add basic secrets management |
| L2 | Basic secrets management; some pipeline security controls; security scans run | Eliminate long-lived credentials; add branch protection |
| L3 | OIDC federation for all credentials; ephemeral runners; security gates block high-severity findings | Artifact signing; SBOM generation; supply chain controls |
| L4 | Full SLSA L2+ compliance; signed artifacts; verified on deploy; supply chain controls complete | SLSA L3; hermetic builds; full pipeline audit coverage |
| L5 | SLSA L3 or L4; automated verification at every promotion; pipeline anomaly detection | SLSA L4; reproducible builds; zero-trust pipeline controls |

### L1 → L2 Action Set

**Read first:**
- [Secure CI/CD Reference Architecture: Threat Model](../../secure-ci-cd-reference-architecture/docs/threat-model.md) — Understanding the pipeline threat landscape before implementing controls
- [Secure Pipeline Templates: Architecture](../../secure-pipeline-templates/docs/architecture.md) — Security gate placement and approval architecture

**Implement first:**
- Deploy the `secure-pipeline-templates` baseline workflow for your CI platform
- Enable branch protection on main/default branch with required PR reviews and status checks
- Enable native secrets management in your CI platform (GitHub Secrets, GitLab CI Variables)

### L2 → L3 Action Set

**Read first:**
- [Secure CI/CD: OIDC Federation Guide](../../secure-ci-cd-reference-architecture/docs/oidc-federation-guide.md) — Step-by-step elimination of long-lived credentials using OIDC
- [Secure Pipeline Templates: Hardening Checklist](../../secure-pipeline-templates/docs/hardening-checklist.md) — Full security review against all pipeline controls

**Key actions:**
- Migrate all cloud credentials to OIDC federation (no more IAM keys in CI secrets)
- Enable ephemeral runners (or document equivalent controls for self-hosted runners)
- Set SAST and SCA gates to block on CRITICAL severity findings

### L3 → L4 Action Set

**Read first:**
- [Software Supply Chain: SLSA Level Advancement Guide](../../software-supply-chain-security-framework/docs/slsa-level-advancement.md) — Step-by-step SLSA L1 through L4 implementation
- [Software Supply Chain: SBOM Guide](../../software-supply-chain-security-framework/docs/sbom-guide.md) — Generating and integrating SBOM into the CI pipeline

**Key actions:**
- Add Cosign keyless signing to all container image builds
- Generate SBOM (CycloneDX format) as a pipeline artifact
- Deploy Kyverno or OPA Gatekeeper to enforce signature verification at admission time

### L4 → L5 Action Set

**Read first:**
- [Software Supply Chain: SLSA Level Advancement — Level 3](../../software-supply-chain-security-framework/docs/slsa-level-advancement.md) — Hardened ephemeral build environment requirements
- [Secure CI/CD: Pipeline Forensics Playbook](../../secure-ci-cd-reference-architecture/docs/pipeline-forensics-playbook.md) — Post-incident pipeline investigation

---

## Domain 5: Testing and Validation

### Score Interpretation

| Your Score | Meaning | Next Focus |
|------------|---------|-----------|
| L1 | No security testing; vulnerabilities found by customers or in incidents | Deploy DAST; add basic SCA |
| L2 | DAST runs periodically (not in CI); manual security testing | Integrate DAST into CI; add API security testing |
| L3 | DAST in CI with gate on high-severity findings; API security testing; annual penetration test | Authenticated DAST; IAST in staging; penetration testing scoped to high-risk areas |
| L4 | Full DAST coverage including authenticated flows; semi-annual pen tests; defined vulnerability SLAs | Continuous security testing; bug bounty or VDP program |
| L5 | Continuous automated security testing; red team exercises; chaos security engineering | Self-healing systems; automated exploit validation |

### L1 → L2 Action Set

**Read first:**
- [Secure Pipeline Templates: Framework — Stage 10 DAST](../../secure-pipeline-templates/docs/framework.md) — OWASP ZAP baseline, full, and API scan modes
- [DevSecOps Framework: API Security](../../devsecops-framework/docs/api-security.md) — API-specific DAST configuration and testing

**Implement:**
- Add OWASP ZAP baseline scan to staging environment (weekly automated run to start)
- Configure Trivy for SCA (filesystem and container image scanning) in CI

### L2 → L3 Action Set

**Read first:**
- [Secure Pipeline Templates: Framework — DAST Configuration](../../secure-pipeline-templates/docs/framework.md) — Authenticated scanning, rate limiting, state mutation considerations
- [DevSecOps Framework: Implementation — Phase 2](../../devsecops-framework/docs/implementation.md) — DAST integration as a Phase 2 milestone

---

## Domain 6: Infrastructure Security

### Score Interpretation

| Your Score | Meaning | Next Focus |
|------------|---------|-----------|
| L1 | Infrastructure deployed manually; no IaC scanning; cloud misconfigurations undetected | Add IaC scanning to any Terraform/CloudFormation in use |
| L2 | IaC in use; basic IaC scanning (Checkov); some hardening applied | Complete CIS Benchmark compliance; add CSPM |
| L3 | IaC scanning in CI with mandatory gates; CSPM continuous monitoring; Kubernetes hardening complete | Network micro-segmentation; admission control policies |
| L4 | Full drift detection; OPA/Kyverno policies enforced; continuous compliance reporting | Zero trust network architecture; eBPF-based monitoring |
| L5 | Infrastructure security as code; automated remediation of drift; behavioral security baseline | Self-healing security posture |

### L1 → L2 Action Set

**Read first:**
- [Cloud Security: Introduction](../../cloud-security-devsecops/docs/introduction.md) — Cloud-specific threat model and shared responsibility
- [Secure Pipeline Templates: IaC Security Pipeline](../../secure-pipeline-templates/templates/iac-security-pipeline.yml) — Production-ready IaC scanning pipeline for Terraform, Helm, CloudFormation

### L2 → L3 Action Set

**Read first:**
- [Cloud Security: Framework](../../cloud-security-devsecops/docs/framework.md) — Full cloud controls catalog for AWS/Azure/GCP
- [Cloud Security: Multi-Cloud Reference](../../cloud-security-devsecops/docs/multi-cloud-reference.md) — Side-by-side service comparison and hardening guidance
- [Compliance Automation: Architecture](../../compliance-automation-framework/docs/architecture.md) — Deploying CSPM with continuous monitoring

### L3 → L4 Action Set

**Read first:**
- [Cloud Security: Zero Trust Architecture](../../cloud-security-devsecops/docs/zero-trust-architecture.md) — Network micro-segmentation and workload identity implementation
- [Cloud Security: eBPF Security](../../cloud-security-devsecops/docs/ebpf-security.md) — eBPF-based infrastructure monitoring

---

## Domain 7: Operations and Monitoring

### Score Interpretation

| Your Score | Meaning | Next Focus |
|------------|---------|-----------|
| L1 | No centralized logging; incidents discovered by customers | Deploy centralized logging; define on-call process |
| L2 | Centralized logging; basic alerting; informal incident response | Define IR process; add SIEM alerting on critical events |
| L3 | SIEM with correlated alerts; documented IR playbooks; defined MTTD and MTTR targets | Runtime threat detection (Falco); behavioral baselines |
| L4 | Runtime behavioral monitoring operational; MTTD < 15 minutes; automated containment for P1 | Threat intelligence integration; behavioral anomaly detection |
| L5 | AI-assisted threat detection; proactive threat hunting; automated response for known attack patterns | Autonomous security response |

### L1 → L2 Action Set

**Read first:**
- [DevSecOps Framework: Framework — Operate and Monitor phases](../../devsecops-framework/docs/framework.md) — Security activities and monitoring requirements per phase
- [Compliance Automation: Evidence Collection](../../compliance-automation-framework/docs/evidence-collection-automation.md) — Log retention, immutability, and audit requirements

### L2 → L3 Action Set

**Read first:**
- [DevSecOps Framework: Runtime Threat Detection](../../devsecops-framework/docs/runtime-threat-detection.md) — Falco deployment, rule development, and alert triage
- [Cloud Security: Incident Response Playbooks](../../cloud-security-devsecops/docs/incident-response-playbooks.md) — Playbooks for common cloud and container incidents

### L3 → L4 Action Set

**Read first:**
- [DevSecOps Framework: Runtime Threat Detection — eBPF and Tetragon](../../devsecops-framework/docs/runtime-threat-detection.md) — Advanced eBPF-based process and network monitoring
- [Cloud Security: Zero Trust — Visibility Pillar](../../cloud-security-devsecops/docs/zero-trust-architecture.md) — Behavioral baselines and anomaly detection signals

---

## Domain 8: Governance and Compliance

### Score Interpretation

| Your Score | Meaning | Next Focus |
|------------|---------|-----------|
| L1 | No formal security policy; compliance is reactive (audit-driven) | Define security policy; map to one compliance framework |
| L2 | Security policies documented; some compliance evidence collected manually | Automate evidence collection; map controls to frameworks |
| L3 | Continuous compliance monitoring; automated evidence collection; audit-ready posture | Policy as Code enforcement; multi-framework mapping |
| L4 | Full Policy as Code for all environments; continuous compliance dashboard; exception management automated | Advanced controls automation; geographic compliance |
| L5 | Real-time compliance posture; automated audit package generation; continuous risk quantification | Predictive compliance; autonomous control adjustment |

### L1 → L2 Action Set

**Read first:**
- [Compliance Automation: Introduction](../../compliance-automation-framework/docs/introduction.md) — Why manual compliance fails at scale; the automation imperative
- [Compliance Automation: Regulatory Controls Matrix](../../compliance-automation-framework/docs/regulatory-controls-matrix.md) — Map your applicable frameworks to Techstream controls

### L2 → L3 Action Set

**Read first:**
- [Compliance Automation: Architecture](../../compliance-automation-framework/docs/architecture.md) — Four-layer compliance system design
- [Compliance Automation: Evidence Collection Automation](../../compliance-automation-framework/docs/evidence-collection-automation.md) — Deploying automated evidence pipelines

### L3 → L4 Action Set

**Read first:**
- [Compliance Automation: Framework](../../compliance-automation-framework/docs/framework.md) — OPA and Kyverno Policy as Code patterns
- [Compliance Automation: Exception Management](../../compliance-automation-framework/docs/exception-management.md) — Automated exception lifecycle, approval routing, and expiry

---

## Prioritizing Remediation Across Domains

When multiple domains score below target, use this prioritization framework:

### Priority 1: Prerequisites for Everything Else

These domains create the foundation that all others depend on. Score them first regardless of organizational focus:

| Domain | Why It's Foundational |
|--------|-----------------------|
| **Domain 3: Secure Development** (L1→L2) | Deploying the secure pipeline template is the single highest-leverage action — it addresses gaps in domains 3, 4, and 5 simultaneously |
| **Domain 4: CI/CD Security** (L1→L2) | Pipeline controls protect all code in the organization; a compromised pipeline undermines all other controls |

### Priority 2: Address Your Highest-Profile Risk

| If Your Profile Is... | Focus Next On |
|-----------------------|--------------|
| Pre-audit (SOC 2 in < 6 months) | Domain 8: Governance → Compliance Automation Framework |
| Recent supply chain incident | Domain 4: CI/CD → Supply Chain Framework → SLSA L2 |
| Kubernetes platform team | Domain 6: Infrastructure → Cloud Security Framework |
| Regulated industry (healthcare, finance) | Domain 8 + Domain 2 (security requirements with regulatory mapping) |
| Rapid growth (hiring fast) | Domain 1: Culture + Security Champion Program |

### Priority 3: Sequence for Maximum Coverage

After addressing Priority 1 and 2:

```
D3 Secure Dev (L2) → D4 CI/CD (L2) → D5 Testing (L2) [pipeline template deployment]
         ↓
D6 Infrastructure (L2) → D8 Governance (L2) [cloud controls + evidence]
         ↓
D4 CI/CD (L3) → Supply Chain (SLSA L2) → D6 Infrastructure (L3)
         ↓
D7 Monitoring (L3) → Runtime Detection [Falco deployment]
         ↓
D8 Governance (L3) → Policy as Code [OPA/Kyverno enforcement]
```

---

## Tracking Progress

After using this guide to define your implementation plan, track advancement using:

- **[Assessment Scorecard](assessment-scorecard.md)** — Re-run quarterly; compare against previous scores
- **[Metrics and KPIs](metrics-kpis.md)** — Domain-specific metrics to confirm improvement is real, not just tooling deployed
- **[Remediation Playbooks](remediation-playbooks.md)** — Step-by-step advancement guides with evidence requirements and owner assignments
- **[Scaling Guidance](scaling-guidance.md)** — Organization-size-specific sequencing for startup, scale-up, and enterprise

---

## Related Documents

- [Assessment Scorecard](assessment-scorecard.md) — Workshop scorecard to produce the scores this guide interprets
- [Remediation Playbooks](remediation-playbooks.md) — Detailed advancement steps with effort estimates and owner assignments
- [Metrics and KPIs](metrics-kpis.md) — Measurable outcomes for each domain and level
- [Techstream Docs: Framework Selection Guide](../../techstream-docs/docs/framework-selection-guide.md) — Alternate starting point by organizational driver
- [Techstream Docs: Integration Scenarios](../../techstream-docs/docs/integration-scenarios.md) — End-to-end implementation walkthroughs for six organizational contexts
