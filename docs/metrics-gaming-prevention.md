# Preventing and Detecting Metrics Gaming

Maturity metrics and security KPIs are management tools — they work only if they measure real security capability rather than the appearance of it. When metrics are tied to team performance reviews, budget allocations, or public scorecards, teams face incentives to optimize for the metric rather than the underlying outcome. This guide identifies common gaming patterns in DevSecOps maturity programs and defines structural controls to prevent or detect them.

---

## Why Metrics Gaming Occurs

Gaming is a rational response to misaligned incentives. Teams optimize for what they are measured on, particularly when:

1. **Scores determine budget or headcount** — teams suppress findings to avoid appearing to have high vulnerability debt
2. **Maturity levels are used in external communications** — marketing pressure to claim high maturity levels inflates self-assessments
3. **Assessment is self-reported without evidence validation** — no external check on whether claimed practices actually operate
4. **There is no distinction between "implemented" and "effective"** — a tool installed but ignored scores the same as a tool actively used
5. **Speed of improvement is rewarded** — teams that claim rapid maturity gains receive recognition, incentivizing shortcuts

Understanding the incentive structure in your organization is the first step toward designing a measurement system that resists gaming.

---

## Common Gaming Patterns by Domain

### Scanning Coverage Gaming

**Pattern:** Teams deploy SAST/SCA tools in "report only" mode or with severity thresholds set to ignore everything, reporting tool deployment without enforcing findings.

**Indicators:**
- SAST scan runs in pipeline but never blocks a PR
- Zero SAST findings reported (statistically implausible for any active codebase)
- SCA reports show no vulnerabilities despite using dependencies with known CVEs
- Scan results are not visible to the security team

**Detection controls:**
```python
# Anomaly detection: zero-finding SAST is a red flag, not a green light
def detect_zero_finding_anomaly(sast_results: list[dict]) -> bool:
    """
    A healthy codebase with active SAST at LOW severity should have findings.
    Zero findings at any severity for a project > 10k lines of code is anomalous.
    """
    total_findings = sum(r.get("finding_count", 0) for r in sast_results)
    project_loc = sum(r.get("lines_of_code", 0) for r in sast_results)

    if project_loc > 10_000 and total_findings == 0:
        return True  # Potential gaming — investigate configuration

    return False
```

**Structural control:** Require security team review of scan *configuration*, not just scan *results*. A quarterly review of SAST rule sets and threshold settings detects tools running in ineffective configurations.

---

### Vulnerability SLA Gaming

**Pattern:** Vulnerabilities are "closed" by marking them as accepted risk, false positive, or out-of-scope without substantive review, to meet SLA compliance targets.

**Indicators:**
- False positive rate > 30% across all findings (industry baseline is typically 10-20% for well-tuned tools)
- Sharp spike in "accepted risk" designations near SLA deadline
- Accepted risk items never expire or get re-reviewed
- No correlation between accepted risks and actual business risk justification

**Detection controls:**
```sql
-- Detect gaming: spike in risk acceptances near SLA deadlines
SELECT
    DATE_TRUNC('week', accepted_at) AS week,
    COUNT(*) AS acceptances,
    AVG(COUNT(*)) OVER (ORDER BY DATE_TRUNC('week', accepted_at)
                        ROWS BETWEEN 12 PRECEDING AND 1 PRECEDING) AS baseline_avg
FROM vulnerability_dispositions
WHERE disposition = 'accepted_risk'
GROUP BY week
HAVING COUNT(*) > 2 * AVG(COUNT(*)) OVER (ORDER BY DATE_TRUNC('week', accepted_at)
                                           ROWS BETWEEN 12 PRECEDING AND 1 PRECEDING)
ORDER BY week;
```

**Structural control:**
- Sample 10-15% of accepted risk dispositions for independent security team review each quarter
- Require a second approver for accepted risk on HIGH and CRITICAL severity findings
- Set maximum "accepted risk" duration (e.g., 90 days), after which items must be re-reviewed or remediated
- Track false positive rate per team and investigate outliers

---

### Training Completion Gaming

**Pattern:** Security training completions are recorded without evidence of actual learning — training is opened and immediately closed, or a single completion is attributed to multiple employees.

**Indicators:**
- Training completion time is implausibly short (e.g., 2-hour course completed in 4 minutes)
- Completion rate is 100% across large teams (unusual without mandated time allocation)
- Post-training assessment scores are uniformly high but security incidents involving the trained topics continue at the same rate

**Detection controls:**
- Track and audit training completion duration — flag completions below 50% of estimated duration
- Require post-training knowledge assessments with random question ordering
- Measure the correlation between training completion and subsequent behavior changes (e.g., fewer SAST findings in trained developers' PRs)

**Structural control:** Complement completion metrics with outcome metrics: Are teams that have completed security training showing fewer vulnerability patterns in code review? Is the security champion program producing measurable security improvements in teams?

---

### Maturity Level Inflation

**Pattern:** In self-assessment-based maturity models, teams report higher maturity levels than the evidence supports by selecting favorable interpretations of criteria.

**Indicators:**
- Self-assessed scores are consistently 0.5-1.5 levels above assessor-validated scores
- Evidence submitted for high levels is thin or does not clearly demonstrate the claimed practice
- Score jumps of > 1 level between assessments without a corresponding improvement roadmap execution

**Detection controls:**
- Require evidence for every criterion scored above Level 2 — a brief description of "what we do" is not evidence
- Calibrate self-assessments against assessor-led assessments at least annually
- Track the self-to-validated score divergence over time; a persistent gap indicates systematic inflation
- Require teams to link specific artifacts (pipeline run IDs, tool screenshots, process documents) to score claims

**Structural control:** Separate the "current state" assessment from the "target" maturity level. Teams should report current state evidence accurately; improvement plans define target states. This removes the incentive to inflate current state to justify a target.

---

### Incident Rate Gaming

**Pattern:** Incident counts are reduced by reclassifying incidents (downgrading severity, closing as "informational") rather than improving detection or response capability.

**Indicators:**
- Incident count decreases significantly without corresponding capability improvements
- MTTD (mean time to detect) increases at the same time incident count decreases — fewer incidents detected, not fewer occurring
- High ratio of "informational" or "false positive" incident closures

**Detection controls:**
```python
# Detection: MTTD should decrease (improve) as incident count decreases
# If both MTTD and incident count decrease, detection capability likely degraded
def detect_incident_gaming(monthly_metrics: list[dict]) -> list[str]:
    warnings = []
    for i in range(1, len(monthly_metrics)):
        current = monthly_metrics[i]
        previous = monthly_metrics[i - 1]

        incident_delta = current["incident_count"] - previous["incident_count"]
        mttd_delta = current["mttd_hours"] - previous["mttd_hours"]

        # Incident count fell AND MTTD got worse — detection may have degraded
        if incident_delta < -0.2 * previous["incident_count"] and mttd_delta > 0:
            warnings.append(
                f"{current['month']}: Incident count fell {abs(incident_delta)} "
                f"but MTTD increased {mttd_delta:.1f}h — possible detection regression or gaming"
            )

    return warnings
```

---

## Structural Controls Against Gaming

### Evidence-Validated Scoring

The most effective control against gaming is requiring evidence for every score. Evidence must be:

1. **Machine-generated where possible** — pipeline run IDs, scan result exports, automated report screenshots are harder to fabricate than written descriptions
2. **Independently verifiable** — the security team or an assessor must be able to independently access the same source system and verify the claim
3. **Time-stamped and recent** — evidence must be from within the current assessment period, not historic one-time demonstrations
4. **Cross-referenced** — evidence for one domain should be consistent with evidence in related domains (e.g., "we enforce SAST at Level 4" should be consistent with "zero SAST findings" being implausible)

### Calibration Assessments

Annual calibration of self-assessments against independent assessor-led assessments provides a check against systematic inflation:

```
Year 1:  Full assessor-led baseline assessment
Year 2:  Self-assessment Q1 + Q3; assessor-validated Q4
Year 3:  Self-assessment quarterly; assessor-validated Q4
Year 3+: Self-assessment quarterly; assessor spot-check (2-3 domains) semi-annually
```

Calibration deltas (self-score vs. assessor score) should be tracked over time. A persistent inflation bias of > 0.3 in a domain indicates a measurement problem or gaming.

### Separate Measurement from Reward

The most direct control: do not tie maturity scores directly to team performance evaluations or budget allocations. Instead:

- Use maturity scores to allocate improvement support (higher score = fewer required improvement initiatives)
- Reward demonstrated improvements in outcome metrics (MTTR, vulnerability escape rate, incident rate) rather than score levels
- Recognize teams that report honest current states and execute credible improvement plans, not those that claim the highest scores

### Anomaly Detection in Metrics Pipelines

Automate detection of statistically unusual patterns:

```python
# metrics_monitor.py — example anomaly detection rules
ANOMALY_RULES = [
    {
        "name": "Zero SAST findings in active project",
        "check": lambda m: m["sast_finding_count"] == 0 and m["lines_of_code"] > 10_000,
        "severity": "HIGH",
        "message": "SAST tool may be misconfigured or bypassed",
    },
    {
        "name": "100% training completion rate",
        "check": lambda m: m["training_completion_pct"] == 100 and m["team_size"] > 20,
        "severity": "MEDIUM",
        "message": "Unusually high completion rate — verify completion quality",
    },
    {
        "name": "Vulnerability SLA compliance jump without remediation activity",
        "check": lambda m: (
            m["sla_compliance_pct"] > m.get("prev_sla_compliance_pct", 0) + 15
            and m["vulnerabilities_remediated"] < 5
        ),
        "severity": "HIGH",
        "message": "SLA compliance increased significantly without remediation — check dispositions",
    },
    {
        "name": "Incident count decrease with MTTD increase",
        "check": lambda m: (
            m["incident_count"] < m.get("prev_incident_count", 999) * 0.8
            and m["mttd_hours"] > m.get("prev_mttd_hours", 0)
        ),
        "severity": "MEDIUM",
        "message": "Fewer incidents AND slower detection — possible detection regression",
    },
]
```

---

## Metrics Design Principles That Resist Gaming

Apply these principles when defining new DevSecOps metrics:

### 1. Prefer Outcome Metrics Over Activity Metrics

| Activity Metric (gameable) | Outcome Metric (harder to game) |
|---------------------------|-------------------------------|
| Number of scans run | Vulnerability escape rate to production |
| Training completion % | SAST finding rate in new code over time |
| Number of security reviews conducted | Security defects found in code review vs. by scanners |
| Incident tickets created | MTTD for real threats (validated by red team) |

### 2. Use Lagging and Leading Indicators Together

A single metric is easy to game. Correlated pairs are harder to game simultaneously:

| Leading Indicator | Lagging Indicator | Gaming Signal |
|------------------|------------------|---------------|
| SAST coverage % | SAST finding count | Coverage up, findings drop → tool misconfigured |
| Training completion % | Post-training assessment pass rate | Completion up, assessment unchanged → gaming |
| Incident response tests run | MTTR in real incidents | Tests pass, MTTR doesn't improve → tests not representative |

### 3. Measure the Measurement System

Include measures of metric *quality* in the program:

- False positive rate trend per tool per team
- Evidence completeness score per domain assessment
- Calibration delta trend (self vs. assessor score) over time
- Time-to-disposition distribution for vulnerability findings (large spikes at SLA boundaries = gaming)

---

## Assessment Integrity Framework

Combine the above controls into an assessment integrity framework:

| Control | Frequency | Owner |
|---------|-----------|-------|
| Evidence sampling audit (10% sample of all Level 3+ claims) | Quarterly | Security Architecture |
| Automated anomaly detection on metrics pipeline | Continuous | Platform Security |
| Self-to-assessor calibration review | Annual | CISO / Assessment Lead |
| False positive disposition audit | Quarterly | AppSec |
| Training completion quality audit | Semi-annual | Security Enablement |
| Incident classification review | Quarterly | SOC / Incident Response |

---

## Related Techstream Resources

| Topic | Document |
|-------|---------|
| Metrics and KPI definitions | [Metrics and KPIs](metrics-kpis.md) |
| Assessment methodology | [Implementation Guide](implementation.md) |
| Assessment scorecard | [Assessment Scorecard](assessment-scorecard.md) |
| Scaling to multiple teams | [Scaling Guidance](scaling-guidance.md) |
| Building a maturity roadmap | [Roadmap](roadmap.md) |

*Part of the Techstream DevSecOps Maturity Model. Licensed under Apache 2.0.*
