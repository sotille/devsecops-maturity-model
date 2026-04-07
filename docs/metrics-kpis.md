# DevSecOps Metrics and KPI Reference Guide

This guide defines the metrics and key performance indicators (KPIs) used to measure DevSecOps program effectiveness across all eight domains of the [DevSecOps Maturity Model](framework.md). It includes metric definitions, collection methods, recommended thresholds by maturity level, and example dashboard queries for common observability platforms.

---

## Measurement Philosophy

Effective DevSecOps measurement follows three principles:

1. **Instrument what you can change.** Metrics should reflect outcomes that teams can directly influence — not just environmental conditions. Tracking "number of CVEs in the wild" is noise; tracking "mean time from CVE disclosure to remediation in your pipeline" is actionable.

2. **Lead indicators over lag indicators.** Lag indicators (production breach count, audit findings) measure past failures. Lead indicators (scan coverage %, secrets detection rate, SBOM completeness) measure current control health. Prioritize lead indicators in operational dashboards; use lag indicators for executive reporting.

3. **Baseline before benchmarking.** Establish a 60-day baseline for each metric before setting improvement targets. Setting targets against undefined baselines produces gaming behavior, not improvement.

---

## Core Metric Domains

### Domain 1: Pipeline Security Coverage

These metrics measure the completeness of security controls across the software delivery pipeline.

| Metric | Definition | Collection Point | Target (Maturity L3+) |
|--------|-----------|------------------|----------------------|
| **SAST scan coverage** | % of repositories with SAST running on every PR | CI/CD platform API | 100% |
| **SCA scan coverage** | % of repositories with dependency scanning on every PR | CI/CD platform API | 100% |
| **Container image scan coverage** | % of container images scanned before deployment | Registry / deployment gate | 100% |
| **IaC scan coverage** | % of IaC repositories with policy enforcement (OPA/Checkov) | CI/CD platform API | 100% |
| **Secrets detection coverage** | % of repositories with pre-commit or CI-level secrets scanning | Source control API | 100% |
| **SBOM generation coverage** | % of released artifacts with an attached, validated SBOM | Artifact registry / SBOM store | ≥ 95% |
| **Artifact signing coverage** | % of released artifacts with a valid cryptographic signature | Registry / Sigstore Rekor | ≥ 95% |

**Collection approach:**

Query your CI/CD platform API to enumerate active repositories and their pipeline configurations. Cross-reference against a central repository inventory. Gaps indicate repositories operating outside the secure pipeline standard.

```python
# Example: GitHub Actions — repositories without SAST workflow
import requests

headers = {"Authorization": f"Bearer {GITHUB_TOKEN}"}
repos = requests.get("https://api.github.com/orgs/{org}/repos?per_page=100", headers=headers).json()
repos_without_sast = [
    r["full_name"] for r in repos
    if not any(
        "sast" in wf["name"].lower()
        for wf in requests.get(
            f"https://api.github.com/repos/{r['full_name']}/actions/workflows",
            headers=headers
        ).json().get("workflows", [])
    )
]
```

---

### Domain 2: Vulnerability Management Velocity

These metrics measure how quickly vulnerabilities are detected and resolved.

| Metric | Definition | Target (Maturity L3+) |
|--------|-----------|----------------------|
| **Mean Time to Detect (MTTD)** | Average time from vulnerability publication (NVD) to first detection in your pipeline | < 24 hours for Critical/High |
| **Mean Time to Remediate (MTTR)** | Average time from detection to verified fix deployed to production | Critical: < 7 days; High: < 30 days; Medium: < 90 days |
| **Vulnerability age distribution** | % of open findings older than SLA threshold by severity | 0% past-SLA for Critical; < 5% for High |
| **False positive rate** | % of scanner findings triaged as false positives | < 20% (higher rates indicate misconfigured scanners) |
| **Reopen rate** | % of closed findings that reopen within 30 days | < 5% |
| **Patch success rate** | % of remediation attempts that successfully eliminate the finding on rescan | ≥ 95% |

**Prometheus / Grafana example:**

If you export vulnerability findings to a time-series store (via Dependency-Track or DefectDojo exporters):

```promql
# Mean time to remediate Critical findings (hours) — 30-day window
avg(
  vulnerability_resolution_duration_hours{severity="critical"}
) by (team)

# % of Critical findings past SLA (7 days)
(
  count(vulnerability_age_days{severity="critical"} > 7)
  /
  count(vulnerability_age_days{severity="critical"})
) * 100
```

---

### Domain 3: Supply Chain Security

These metrics measure the integrity and traceability of your software supply chain.

| Metric | Definition | Target (Maturity L3+) |
|--------|-----------|----------------------|
| **SBOM completeness score** | % of SBOM components with complete metadata (name, version, PURL, license, supplier) | ≥ 90% |
| **Dependency freshness** | % of direct dependencies within N major versions of current release | ≥ 80% within 2 major versions |
| **License compliance rate** | % of dependencies with approved license classifications | 100% (all others blocked) |
| **Artifact provenance coverage** | % of production artifacts with verifiable build provenance attestation | ≥ 95% |
| **Third-party action/plugin audit coverage** | % of CI/CD third-party integrations pinned to a specific SHA | 100% |
| **Supply chain incident MTTR** | Mean time from supply chain incident detection to containment | < 4 hours for P1 |

---

### Domain 4: Secrets and Credential Hygiene

| Metric | Definition | Target (Maturity L3+) |
|--------|-----------|----------------------|
| **Secrets detected in commits** | Count of secrets detected per month in commit history | Trending to zero |
| **Secrets remediation rate** | % of detected secrets revoked within 24 hours | 100% |
| **Long-lived credential count** | Number of long-lived API keys or passwords in use (vs. OIDC/short-lived) | Trending to zero |
| **Credential rotation compliance** | % of credentials rotated within policy-defined intervals | 100% |
| **Vault dynamic secret adoption** | % of application credentials sourced from a secrets manager at runtime | ≥ 75% (L3); ≥ 95% (L4) |

---

### Domain 5: Compliance and Audit Posture

| Metric | Definition | Target (Maturity L3+) |
|--------|-----------|----------------------|
| **Policy compliance rate** | % of pipeline runs passing all mandatory policy gates | ≥ 99% |
| **Evidence collection automation** | % of compliance evidence collected automatically (vs. manually) | ≥ 80% |
| **Audit finding repeat rate** | % of audit findings that recur in the next assessment cycle | < 10% |
| **Control coverage** | % of required controls with automated monitoring | ≥ 85% |
| **Exception resolution time** | Average time from policy exception creation to resolution or formal acceptance | < 30 days |

**OPA policy compliance query (if using Styra DAS or rego output logging):**

```sql
-- Example: BigQuery query for policy violation trends
SELECT
  DATE(evaluation_timestamp) AS date,
  policy_name,
  COUNT(*) AS violations
FROM compliance_events
WHERE result = 'DENY'
  AND evaluation_timestamp > TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 30 DAY)
GROUP BY 1, 2
ORDER BY 1, 3 DESC
```

---

### Domain 6: DORA Security Integration

DORA metrics (from the DevOps Research and Assessment program) measure delivery performance. This domain tracks the intersection of DORA metrics with security controls, ensuring that security does not act as a delivery bottleneck.

| Metric | Definition | Target |
|--------|-----------|--------|
| **Deployment frequency** | Number of deployments per day per team | Elite: multiple per day |
| **Lead time for changes** | Time from commit to production | Elite: < 1 hour |
| **Change failure rate** | % of deployments causing production incidents | Elite: 0–5% |
| **MTTR (production incidents)** | Time to restore service after incident | Elite: < 1 hour |
| **Security gate failure rate** | % of pipeline runs blocked by security gates | Target: < 5% (gates should not be bottlenecks) |
| **Security-attributed deployment delay** | Average delay in minutes added by security scanning steps | Target: < 5 minutes for standard pipelines |

The security gate failure rate and security-attributed delay metrics are critical for identifying scanner misconfiguration, excessive false positives, or scans running on the critical path that should be parallelized.

---

### Domain 7: Threat Detection and Response

| Metric | Definition | Target (Maturity L3+) |
|--------|-----------|----------------------|
| **Pipeline anomaly detection coverage** | % of pipelines with behavioral anomaly alerting | ≥ 80% |
| **Alert signal-to-noise ratio** | % of security alerts that result in a confirmed investigation (vs. auto-closed as noise) | ≥ 30% |
| **MTTD (pipeline security events)** | Mean time from anomalous event to alert | < 15 minutes |
| **MTTR (pipeline security events)** | Mean time from alert to containment | < 2 hours for P2 |
| **Threat hunt cadence** | Frequency of proactive threat hunts in CI/CD audit logs | Monthly minimum (L3); Continuous (L4) |

---

### Domain 8: Developer Security Experience

These metrics measure security's impact on developer productivity and adoption.

| Metric | Definition | Target |
|--------|-----------|--------|
| **Developer security training completion** | % of engineers completing annual security training | 100% |
| **Security champion participation rate** | % of engineering teams with an active security champion | 100% |
| **Security finding acknowledgment time** | Average time for a developer to acknowledge a security finding in their PR | < 24 hours |
| **Tool-assisted fix rate** | % of SAST/SCA findings fixed using tool-provided remediation guidance | ≥ 60% |
| **Threat modeling adoption** | % of new features with a completed threat model before implementation | ≥ 80% |
| **Developer-reported friction score** | Self-reported score (1–5) of security tool friction in developer workflow | ≥ 4.0 / 5.0 |

---

## Dashboard Architecture

### Recommended Dashboard Layout

Structure security metrics dashboards in three tiers:

**Tier 1 — Executive Summary (weekly)**
- Program health score (composite of domain coverage rates)
- Open Critical/High findings count and trend
- SLA compliance rate
- Supply chain risk posture (SBOM coverage, artifact signing)
- DORA metrics with security impact overlay

**Tier 2 — Program Operations (daily)**
- Pipeline scan coverage by team and repository
- Vulnerability MTTR by severity and team
- Policy violation trends
- Credential hygiene status
- Incident/exception queue status

**Tier 3 — Engineering Dashboard (per-team, real-time)**
- Open findings in my repositories by severity
- My team's SLA compliance
- Scan pass/fail rate for my recent PRs
- Blocked deployments and reasons

---

## Grafana Dashboard JSON — Starter Template

The following panels are a starter configuration for a Grafana dashboard backed by a Prometheus exporter from Dependency-Track or DefectDojo. Adapt metric names to match your exporter's label schema.

```json
{
  "panels": [
    {
      "title": "Critical Vulnerabilities — Open Count",
      "type": "stat",
      "targets": [{
        "expr": "count(vulnerability_findings{severity='critical', status='open'})",
        "legendFormat": "Open Critical"
      }],
      "thresholds": {"steps": [
        {"color": "green", "value": 0},
        {"color": "yellow", "value": 1},
        {"color": "red", "value": 5}
      ]}
    },
    {
      "title": "SBOM Coverage %",
      "type": "gauge",
      "targets": [{
        "expr": "(sum(artifacts_with_sbom) / sum(total_artifacts)) * 100",
        "legendFormat": "SBOM Coverage"
      }],
      "thresholds": {"steps": [
        {"color": "red", "value": 0},
        {"color": "yellow", "value": 80},
        {"color": "green", "value": 95}
      ]}
    },
    {
      "title": "Vulnerability MTTR by Severity (days)",
      "type": "timeseries",
      "targets": [
        {"expr": "avg(vulnerability_mttr_days{severity='critical'})", "legendFormat": "Critical"},
        {"expr": "avg(vulnerability_mttr_days{severity='high'})", "legendFormat": "High"},
        {"expr": "avg(vulnerability_mttr_days{severity='medium'})", "legendFormat": "Medium"}
      ]
    },
    {
      "title": "Pipeline Security Gate Pass Rate %",
      "type": "timeseries",
      "targets": [{
        "expr": "(sum(pipeline_runs_passed) / sum(pipeline_runs_total)) * 100",
        "legendFormat": "Pass Rate"
      }]
    }
  ]
}
```

---

## Metric Collection Toolchain

| Tool | Metrics Provided | Integration |
|------|-----------------|-------------|
| **Dependency-Track** | Vulnerability counts, SBOM completeness, component age | REST API, Prometheus exporter |
| **DefectDojo** | Finding age, MTTR, false positive rates, team assignment | REST API, webhook |
| **GitHub Advanced Security** | SAST/SCA coverage, secret scanning detections | REST API, audit log streaming |
| **OPA / Styra DAS** | Policy compliance rate, violation trends | Decision log export |
| **Sigstore / Rekor** | Artifact signing coverage, transparency log entries | Rekor REST API |
| **HashiCorp Vault** | Credential rotation, secret lease expiry, dynamic secret adoption | Vault audit log, Prometheus metrics |
| **CI/CD platform (GA/GitLab)** | Pipeline pass rates, scan job duration, deployment frequency | REST API, webhook |

---

## Maturity-Aligned Targets Summary

| Metric Category | Level 1 | Level 2 | Level 3 | Level 4 |
|-----------------|---------|---------|---------|---------|
| SAST coverage | < 25% | 25–75% | > 75% | 100% |
| Critical MTTR | Unmeasured | < 60 days | < 14 days | < 7 days |
| SBOM coverage | 0% | < 50% | 50–90% | > 95% |
| Policy compliance rate | Unmeasured | < 80% | 80–95% | > 99% |
| Secrets remediation | Unmeasured | < 80% in 72h | 100% in 48h | 100% in 24h |
| Evidence automation | 0% | < 40% | 40–80% | > 80% |

---

## Industry Benchmark Ranges

The following benchmark ranges represent observed performance across engineering organizations segmented by size and regulatory posture. Benchmarks are derived from published DORA State of DevOps reports, Verizon DBIR data, Ponemon Institute research, and practitioner surveys. Use these ranges to contextualize your organization's metrics and set improvement targets.

> **Interpretation guidance:** Being below the median is not a risk on its own; it identifies an improvement opportunity. Being below the 25th percentile on Critical MTTR or Secrets Remediation in a regulated environment warrants immediate attention.

### DORA Delivery Metrics Benchmarks

| Metric | Low Performer (bottom 25%) | Industry Median | High Performer (top 25%) | Elite (top 10%) |
|--------|---------------------------|-----------------|--------------------------|------------------|
| Deployment Frequency | < 1/month | 1–4/month | 1–7/week | Multiple/day |
| Lead Time for Changes | > 1 month | 1 week – 1 month | 1 day – 1 week | < 1 hour |
| Change Failure Rate | > 15% | 10–15% | 5–10% | < 2% |
| Mean Time to Restore (MTTR) | > 1 week | 1 day – 1 week | < 1 day | < 1 hour |

*Source: DORA State of DevOps Report 2024/2025 — Software Delivery Performance clusters*

### Vulnerability Management Benchmarks

| Metric | Low Performer | Industry Median | High Performer | Elite |
|--------|---------------|-----------------|----------------|-------|
| Critical CVE MTTR | > 90 days | 30–60 days | 7–14 days | < 3 days |
| High CVE MTTR | > 180 days | 60–90 days | 14–30 days | < 7 days |
| SAST PR Coverage | < 30% | 50–75% | > 85% | 100% |
| Vulnerability Backlog Growth Rate | +20%/month | Flat | -5%/month | -15%/month |
| SLA Compliance Rate (Critical) | < 50% | 65–80% | > 90% | > 98% |

*Note: For PCI-DSS environments, Critical CVE MTTR > 30 days is a finding. For FedRAMP environments, Critical MTTR must be < 15 days.*

### Secrets Security Benchmarks

| Metric | Low Performer | Industry Median | High Performer | Elite |
|--------|---------------|-----------------|----------------|-------|
| Pre-commit Secrets Detection Coverage | 0% | 30–60% | > 80% | 100% |
| Exposed Secret Remediation (72h SLA) | < 40% | 60–75% | > 90% | 100% |
| Secrets in Version Control (current) | > 1% of repos | < 1% | 0 known | 0 with automated verification |
| Secrets Rotation Compliance | < 30% | 50–70% | > 85% | 100% automated |

### Supply Chain Security Benchmarks

| Metric | Low Performer | Industry Median | High Performer | Elite |
|--------|---------------|-----------------|----------------|-------|
| SBOM Generation Coverage | 0% | 20–50% | > 75% | 100% on every release |
| Artifact Signing Coverage | 0% | 15–40% | > 70% | 100% |
| SLSA Level Achieved | Level 0 | Level 1 | Level 2 | Level 3+ |
| Dependency Pinning Rate | < 30% | 50–70% | > 85% | 100% (digest-pinned) |
| License Compliance Automation | None | Manual scan | Automated in CI | Automated + policy enforcement |

*Source: OpenSSF Scorecards project aggregated data; SLSA community survey 2024*

### Policy Compliance Benchmarks

| Metric | Low Performer | Industry Median | High Performer | Elite |
|--------|---------------|-----------------|----------------|-------|
| Infrastructure Policy Compliance Rate | < 60% | 70–85% | > 90% | > 99% |
| Evidence Automation Rate (for audits) | 0–10% | 25–50% | > 70% | > 90% |
| Compliance Drift Detection Time | Unknown | Days–weeks | Hours | < 30 min |
| Policy-as-Code Coverage | 0% | 20–40% | > 60% | > 85% |

### Security Champion Program Benchmarks

| Metric | Low Performer | Industry Median | High Performer | Elite |
|--------|---------------|-----------------|----------------|-------|
| Security Champion Ratio (champions per dev) | None | 1:20–1:15 | 1:10 | 1:6 |
| Developer Security Training Completion | < 30% | 50–70% | > 85% | 100% + refreshers |
| Security Issues Found in Code Review (%) | < 5% | 10–20% | > 25% | > 35% |

### Benchmarks by Organization Profile

Organizations should calibrate targets based on their profile:

| Profile | Realistic 12-Month Target | Primary Focus |
|---------|--------------------------|---------------|
| **Early-stage startup** | DORA median; SAST on all PRs; secrets remediation SLA | Pipeline security foundation |
| **Growth-stage (100–500 engineers)** | DORA high performer; Critical CVE MTTR < 14 days; SBOM coverage > 50% | Vulnerability management velocity |
| **Enterprise non-regulated** | DORA high performer; SLSA Level 2; policy compliance > 90% | Automation and governance |
| **Enterprise regulated (FSI, healthcare, gov)** | DORA median acceptable; Critical CVE MTTR < 7 days; evidence automation > 70%; 100% secrets SLA | Compliance evidence and audit readiness |
| **Cloud-native / SaaS product** | DORA elite deployment frequency; SLSA Level 2–3; 100% SBOM; secrets rotation automated | Supply chain and deployment integrity |

---

## Integration with Maturity Assessment

These metrics directly map to the [Assessment Scorecard](assessment-scorecard.md) domains. When conducting a maturity assessment, use the 60-day metric history for the relevant domain to provide evidence for scored practices, rather than relying solely on participant recall.

Example mapping:

| Scorecard Practice | Supporting Metric | Benchmark Reference |
|--------------------|-------------------|--------------------|
| 3.3: SAST runs on every PR | SAST scan coverage % | High performer: > 85% |
| 4.1: Vulnerability SLAs are defined and tracked | Vulnerability MTTR by severity | Industry median: Critical < 30 days |
| 6.2: All released artifacts have an SBOM | SBOM generation coverage % | High performer: > 75% |
| 7.1: Pipeline anomalies trigger alerts | Pipeline anomaly detection coverage % | High performer: > 80% |

---

## Related Documents

- [Assessment Scorecard](assessment-scorecard.md) — 45-practice scorecard; use the 60-day metric history as evidence for scored practices
- [Remediation Playbooks](remediation-playbooks.md) — Level-by-level remediation steps for improving metrics that fall below target
- [DevSecOps Framework — Best Practices](../../devsecops-framework/docs/best-practices.md) — the practices that drive metric improvement
- [Release Orchestration Framework — Framework](../../release-orchestration-framework/docs/framework.md) — DORA metric instrumentation and deployment frequency measurement
- [Techstream Docs — Integration Scenarios](../../techstream-docs/docs/integration-scenarios.md) — scenario-based guidance on which metrics to prioritize by organizational profile

---

*Part of the Techstream DevSecOps Maturity Model. Licensed under Apache 2.0.*
