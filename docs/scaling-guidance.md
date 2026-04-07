# DevSecOps Scaling Guidance: Small Teams to Enterprise

The DevSecOps Maturity Model applies across organization sizes, but the implementation path, tool choices, and governance structures differ significantly between a 5-person startup and a 5,000-person enterprise. This guide describes how to apply the maturity model appropriately given organizational scale, and which adaptations are required at each size.

---

## Scaling Dimensions

DevSecOps programs scale along four primary dimensions. Challenges and solutions differ for each.

| Dimension | Small Team Challenge | Enterprise Challenge |
|-----------|--------------------|--------------------|
| **People** | One person owns security and engineering; no dedicated security team | Multiple security teams with competing priorities; coordination overhead |
| **Repositories** | 1–20 repositories; easy to apply controls manually | 500–5,000+ repositories; manual policy application impossible |
| **Toolchain** | Any tool works at this scale; cost sensitivity | Tool standardization across hundreds of teams; platform teams required |
| **Governance** | Informal; the team knows the rules | Formal; policies must be documented, enforced, and audited |

---

## Small Team Profile (1–30 Engineers)

### Characteristics
- Engineering and security roles overlap; dedicated security personnel unlikely
- Limited budget for commercial security tools
- Fast iteration; heavyweight processes have immediate negative impact on velocity
- 1–20 repositories; single CI/CD platform

### Maturity Level Targets

Small teams should target **Maturity Level 2 (Managed)** as the primary goal. Level 3 requires metrics infrastructure and organizational structures that are premature at this scale. A well-implemented Level 2 provides strong security posture without organizational overhead.

| Domain | Small Team L2 Target | How to Implement |
|--------|---------------------|-----------------|
| Pipeline security | SAST + SCA on every PR; secrets scanning | Use open source only: Semgrep, Trivy, Gitleaks. Adopt the [Secure Pipeline Templates](../../secure-pipeline-templates/README.md) directly — no customization needed |
| Dependency management | Weekly SCA reports; CVE response within 7 days for Critical | Dependabot or Renovate for automated PRs; weekly triage slot |
| Secrets management | No hardcoded secrets; cloud KMS or Vault OSS | Cloud-native KMS (AWS Secrets Manager, GCP Secret Manager); $0–$5/month at startup scale |
| Branch protection | Protected main; required reviewer | Platform settings; 30 minutes to configure |
| Artifact signing | Sign releases only (not every PR build) | Cosign keyless on release workflow only; reduces cost |
| Incident response | Documented runbook; shared oncall | Simple Notion/Confluence runbook; PagerDuty Starter ($0) |

### Small Team Anti-Patterns

| Anti-Pattern | Why It Happens | What to Do Instead |
|-------------|---------------|-------------------|
| No pipeline security because "we're too small to be attacked" | Underestimation of startup targeting | Attackers target small teams to access corporate customers via supply chain; implement pipeline basics in week 1 |
| Using a single long-lived AWS access key for CI/CD | Fastest path to "working" | Takes 30 minutes to configure OIDC; do this before shipping anything significant |
| Not scanning because "it's all our own code" | False sense of control | 70–90% of modern application code is dependencies, not original code |
| Putting security on the backlog until Series A/B | Misaligned incentives | Security debt at Series B is disproportionately expensive to fix; enterprise customers will audit you |

### Recommended Minimal Toolset (< $200/month)

| Tool | Use | Cost |
|------|-----|------|
| Semgrep (Community) | SAST | $0 |
| Trivy | SCA + container scanning + SBOM | $0 |
| Gitleaks | Secrets detection | $0 |
| Cosign | Artifact signing | $0 |
| Dependabot | Dependency update PRs | $0 (GitHub) |
| AWS Secrets Manager / GCP Secret Manager | Secrets storage | ~$5/month |
| Dependency-Track | Vulnerability tracking | $0 (self-hosted) or ~$30/month (hosting) |

---

## Growth Stage Profile (30–150 Engineers)

### Characteristics
- First dedicated security engineer or small security team (1–3 people)
- Multiple engineering teams; security cannot review every PR
- 20–200 repositories; manual policy inconsistency becomes visible
- First compliance requirements appearing (SOC 2, customer security questionnaires)

### Maturity Level Targets

Growth stage teams should target **Maturity Level 3 (Defined)** with a clear roadmap to Level 4. Level 3 requires:
- Formal security metrics tracked and published
- Security processes documented and consistently followed
- Security champions in each engineering team
- First compliance automation (for SOC 2 or ISO 27001)

### Platform Engineering as Enabler

At 30–150 engineers, a "paved road" approach becomes necessary. One or two engineers cannot review every repository. Instead, build platform-level defaults that apply security controls automatically.

**GitHub organization-level default workflows:**

```yaml
# .github/workflows/security-defaults.yml
# Placed in the .github repository at the org level
# Applies to all repositories in the organization automatically (GitHub starter workflows)

name: Security Defaults
on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  sast:
    uses: your-org/.github/.github/workflows/reusable-sast.yml@main
    secrets: inherit

  sca:
    uses: your-org/.github/.github/workflows/reusable-sca.yml@main
    secrets: inherit
```

**Reusable workflow library pattern:**

Maintain a centralized repository of reusable CI/CD workflows. Each engineering team references the shared workflow rather than copying it. Updates to the shared workflow propagate to all teams.

```yaml
# In each team's pipeline — 3 lines vs 200 lines
jobs:
  security-scan:
    uses: your-org/pipeline-library/.github/workflows/security-scan.yml@v2.1.0
    with:
      image-name: ${{ vars.IMAGE_NAME }}
      severity-threshold: CRITICAL,HIGH
    secrets: inherit
```

### First Compliance Program

Growth stage is typically when SOC 2 or ISO 27001 first appears on the agenda. The [Compliance Automation Framework](../../compliance-automation-framework/docs/introduction.md) provides the architecture for automating evidence collection from this point forward.

**Priority controls for first audit:**
1. Access control logs (who has access to what; quarterly reviews)
2. Change management evidence (PR merge logs; deployment records)
3. Vulnerability management records (scan results; remediation timelines)
4. Incident response records (incident log; post-mortems)

All four can be automated from CI/CD pipeline outputs and cloud audit logs. Do not collect evidence manually if you are starting a compliance program at this scale.

---

## Mid-Market Profile (150–500 Engineers)

### Characteristics
- Dedicated security team (4–15 people)
- Platform engineering team exists or is forming
- Multiple business units or product lines with different risk profiles
- Active compliance program (SOC 2 Type II, ISO 27001, possibly PCI-DSS)
- Security tooling budget: $200,000–$800,000/year

### Maturity Level Targets

Mid-market organizations should target **Maturity Level 3 (Defined)** across all domains, with specific domains reaching **Level 4 (Quantitatively Managed)**.

**Domains to prioritize for Level 4:**
- Vulnerability management (MTTD and MTTR metrics driving SLA enforcement)
- Pipeline security coverage (100% coverage measurable and enforced)
- Compliance automation (continuous compliance dashboards replacing periodic assessments)

### Multi-Team Governance

At 150–500 engineers, security governance requires structure that does not create a bottleneck.

**Security steering committee:** Monthly meeting with security team lead + engineering team leads. Reviews metrics, approves exceptions, sets priorities. Not a review board for individual PRs.

**Risk-tiered control enforcement:**

Different teams have different risk profiles. A team building a public-facing payment API needs stricter controls than a team building an internal analytics dashboard. Define tiers:

| Tier | Risk Profile | Control Stringency | Example Teams |
|------|-------------|-------------------|--------------|
| **Tier 1: Critical** | Handles PII, financial data, auth systems | Full control suite; no exceptions without security approval | Payments, identity, customer data API |
| **Tier 2: Standard** | General application services | Standard controls; exceptions with team lead approval | Product features, internal APIs |
| **Tier 3: Internal** | Internal tools, low-sensitivity data | Baseline controls only | Developer tooling, internal dashboards |

```yaml
# Pipeline variable — teams declare their tier in their repository config
# Platform team validates tier assignment via review process
security:
  tier: "1"
  exceptions: []
  last_reviewed: "2026-01-15"
  reviewed_by: "security-team"
```

---

## Enterprise Profile (500+ Engineers)

### Characteristics
- Dedicated security organization (20–100+ security engineers)
- Platform engineering as a discipline
- Multiple compliance frameworks simultaneously (SOC 2, ISO 27001, PCI-DSS, FedRAMP, HIPAA)
- Thousands of repositories; automation is non-optional
- Security tooling budget: $1M–$10M+/year

### Maturity Level Targets

Enterprise organizations should target **Maturity Level 4 (Quantitatively Managed)** as the operating baseline, with strategic investments in Level 5 (Optimizing) capabilities in high-priority domains.

### Repository-Scale Policy Enforcement

At 500+ repositories, human review of security policy compliance is impossible. Policy-as-Code enforcement at the platform level becomes the primary control.

**GitHub organization rulesets (enterprise):**

```yaml
# Enterprise ruleset — applies to all repositories in the organization
# Cannot be overridden at the repository level
ruleset:
  name: enterprise-security-baseline
  enforcement: active
  conditions:
    repository_name:
      include: ["*"]
  rules:
    - type: required_status_checks
      parameters:
        strict_required_status_checks_policy: true
        required_status_checks:
          - context: "SAST / Semgrep"
          - context: "SCA / Trivy Filesystem"
          - context: "Secrets Detection / Gitleaks"
    - type: pull_request
      parameters:
        required_approving_review_count: 1
        dismiss_stale_reviews_on_push: true
        require_code_owner_review: true
    - type: required_deployments
      parameters:
        required_deployment_environments: ["staging"]
```

**Policy compliance dashboard:**

Track repository-level compliance against the enterprise baseline. Alert security leads when repositories fall out of compliance.

```python
# compliance-dashboard-collector.py
# Queries GitHub API for policy compliance across all org repositories

import requests

GITHUB_ORG = "your-org"
REQUIRED_WORKFLOWS = ["sast", "sca", "secrets-scan"]

headers = {"Authorization": f"Bearer {GITHUB_TOKEN}"}
repos = requests.get(
    f"https://api.github.com/orgs/{GITHUB_ORG}/repos?per_page=100",
    headers=headers
).json()

compliance_report = {"compliant": [], "non_compliant": []}

for repo in repos:
    workflows = requests.get(
        f"https://api.github.com/repos/{repo['full_name']}/actions/workflows",
        headers=headers
    ).json().get("workflows", [])

    workflow_names = [w["name"].lower() for w in workflows]
    has_required = all(
        any(req in name for name in workflow_names)
        for req in REQUIRED_WORKFLOWS
    )

    if has_required:
        compliance_report["compliant"].append(repo["full_name"])
    else:
        compliance_report["non_compliant"].append({
            "repo": repo["full_name"],
            "missing": [r for r in REQUIRED_WORKFLOWS
                        if not any(r in n for n in workflow_names)]
        })

print(f"Compliant: {len(compliance_report['compliant'])}/{len(repos)}")
for nc in compliance_report["non_compliant"]:
    print(f"  NON-COMPLIANT: {nc['repo']} — missing: {nc['missing']}")
```

### Enterprise Security Champions at Scale

The [Security Champions Program](../../devsecops-methodology/docs/security-champion-program.md) requires different structure at enterprise scale.

| Aspect | Startup/Small | Enterprise |
|--------|--------------|-----------|
| Champion selection | Volunteer | Nominated by engineering lead; approved by security org |
| Training | Self-directed | Structured curriculum; vendor-delivered certifications (CSSLP, GWEB) |
| Time allocation | 5–10% of time | 15–20% formally allocated; reflected in performance objectives |
| Coordination | Slack channel | Monthly champions guild; quarterly summit; dedicated champion Slack workspace |
| Recognition | Informal | Formal career path component; visible in performance review |
| Metrics | None | Champion activity tracked: findings reported, training completed, PRs reviewed |

---

## Scaling the Maturity Assessment

The [Assessment Scorecard](assessment-scorecard.md) is designed for a single organizational unit. At enterprise scale, running a single org-wide assessment produces a meaningless average. Use a federated assessment model instead.

**Federated assessment model:**

1. Each product team or business unit runs an independent maturity assessment
2. Results are aggregated to identify the spread across the organization
3. The security program targets raising the minimum (not the average)
4. High-maturity teams serve as implementation case studies for lower-maturity teams

```
Assessment distribution (enterprise example):
  L1: 5 teams  → Immediate remediation priority
  L2: 18 teams → Active improvement program
  L3: 25 teams → Maintaining and extending
  L4: 8 teams  → Sharing practices organization-wide
  L5: 2 teams  → Industry-leading; contributing to open standards

Program target: Bring all L1 teams to L2 within 6 months
               Bring all L2 teams to L3 within 12 months
```

---

## Scaling DevSecOps Tooling Architecture

As organizations grow, the CI/CD tooling architecture must evolve from individual pipeline configurations to a managed platform.

| Scale | Architecture | Management Model |
|-------|-------------|-----------------|
| **1–30 engineers** | Individual pipeline configs per repo | Each team manages own pipeline |
| **30–150 engineers** | Reusable workflow library; shared action marketplace | Central library maintained by platform team; teams reference shared workflows |
| **150–500 engineers** | Internal developer platform; golden path templates | Platform engineering team provides paved road; teams customize within guardrails |
| **500+ engineers** | Enterprise developer platform (Backstage, Cortex, or custom); policy-as-code enforcement at platform level | Platform team maintains; security team provides policy; engineering teams consume |

---

## Cross-References

| Topic | Document |
|-------|---------|
| Full maturity level definitions | [Framework](framework.md) |
| Assessment scorecard | [Assessment Scorecard](assessment-scorecard.md) |
| Metrics and KPIs | [Metrics and KPIs](metrics-kpis.md) |
| Remediation playbooks by level | [Remediation Playbooks](remediation-playbooks.md) |
| Security champions program design | [Security Champions Program](../../devsecops-methodology/docs/security-champion-program.md) |
| Tool budget by org size | [Security Tool Budget Framework](../../devsecops-methodology/docs/security-tool-budget-framework.md) |
