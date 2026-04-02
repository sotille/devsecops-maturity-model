# DevSecOps Maturity Model — Best Practices

## Table of Contents

1. [Best Practices for Running Maturity Assessments](#best-practices-for-running-maturity-assessments)
2. [Common Mistakes in Maturity Programs](#common-mistakes-in-maturity-programs)
3. [How to Avoid Gaming the Model](#how-to-avoid-gaming-the-model)
4. [Continuous Assessment Cadence](#continuous-assessment-cadence)
5. [Using Metrics to Track Progression](#using-metrics-to-track-progression)
6. [Communicating Results to Leadership](#communicating-results-to-leadership)
7. [Benchmarking Against Industry Peers](#benchmarking-against-industry-peers)

---

## Best Practices for Running Maturity Assessments

### 1. Separate Assessment from Audit

The most important cultural distinction in a successful maturity program is the difference between **assessment** (diagnostic, improvement-focused, psychologically safe) and **audit** (compliance-focused, pass/fail, accountability-focused). Maturity assessments produce better data and drive better outcomes when participants feel safe being honest about gaps.

Communicate explicitly that assessment scores do not reflect individual performance evaluations, that low scores in one area do not overshadow strong performance in another, and that the purpose of the assessment is to help the organization improve, not to create accountability for the past.

### 2. Use Multiple Evidence Types

Maturity assessments are most reliable when they triangulate across three evidence types:
- **Stated practice** (what stakeholders say they do in interviews)
- **Documented practice** (what processes, policies, and procedures describe)
- **Demonstrated practice** (what tool outputs, metrics, and artifacts show actually happens)

Discrepancies between these three types are the most valuable findings. An organization that has an incident response plan (documented) but cannot demonstrate it has been tested (demonstrated) is scored at a lower level than one where the plan is tested and refined regularly. Never accept stated practice without corroboration.

### 3. Score Evidence, Not Intent

Score the organization's current state, not its aspirations or plans. "We are planning to implement DAST by Q3" is not evidence of a DAST capability. Score based on what can be demonstrated today. This discipline is critical for maintaining the integrity of the model over time — if assessors routinely credit planned capabilities, scores become meaningless as predictors of actual security posture.

### 4. Engage Domain Experts, Not Just Security

The richest assessment data comes from the people doing the work, not from security team representatives describing what the engineering teams do. Wherever possible, interview the platform engineers about CI/CD security, the developers about secure coding practices, and the SRE team about security monitoring — not the security team speaking on their behalf.

### 5. Document Evidence Provenance

For every score, document what evidence was collected, from whom, and when. This serves two purposes: it makes the assessment defensible if scores are questioned, and it creates a clear picture of where evidence gaps exist (domains where scores are based primarily on interviews rather than documented or demonstrated practice are inherently more uncertain and should be noted as such).

### 6. Use a Consistent Assessment Team

When conducting assessments over time (annual cadence or more frequent), use a consistent core assessment team. This reduces score variation driven by assessor interpretation differences rather than actual capability changes, making trend data more reliable.

### 7. Validate Scores With Domain Stakeholders Before Finalizing

Before publishing final scores, share draft scores with the stakeholders interviewed for each domain. Ask them to review for factual accuracy — not to negotiate scores upward. This step frequently surfaces additional evidence (positive or negative) that was not presented during initial interviews, improves the quality of the final assessment, and builds stakeholder buy-in to the results.

### 8. Separate Assessment from Roadmap Development

The assessment should conclude with a clear, agreed-upon set of scores. The roadmap development discussion begins only after scores are finalized. When assessment and roadmap discussions are interleaved, participants begin advocating for higher scores in domains where they want investment rather than reporting accurate current state.

### 9. Calibrate Assessors

If the assessment team has multiple members, run a calibration exercise before the assessment begins. Review sample evidence from a previous assessment and independently score 2-3 domains, then compare. Discuss and align on interpretation of the scoring criteria before assessing live domains. This reduces inter-assessor variability that would otherwise make scores unreliable across teams or time periods.

### 10. Time-Box Evidence Review

Evidence review can expand to fill any available time. Set explicit time limits for evidence review per domain (suggested: 3-4 hours per domain for a first assessment, 2 hours for subsequent assessments). This forces prioritization of the most important evidence and prevents assessment fatigue from degrading quality in later domains.

---

## Common Mistakes in Maturity Programs

### Mistake 1: Treating Maturity Score as a Goal, Not a Measure

The goal of a maturity program is improved security outcomes. The maturity score is a measure of the capability that produces those outcomes. When organizations focus on hitting a specific score (driven by contractual requirements, board targets, or competitive benchmarking), they often achieve the score without achieving the underlying capability improvement that should drive it. Scores are lagging indicators of capability — they should be used to identify gaps, not to motivate gaming.

**Remedy**: Focus roadmap discussions on specific practices to implement, not on score targets. Define success as "we will implement threat modeling for all significant features" not as "we will achieve 3.0 in Security Requirements."

### Mistake 2: Over-Weighting Tooling Evidence

Tool deployment is easier to demonstrate than process maturity, and assessors often unconsciously give more weight to tool evidence because it is more concrete. An organization that deploys a SAST tool but has 80% false positive rates and no remediation process has lower actual maturity than one without the tool but with a disciplined manual code review process. Tooling is means, not ends.

**Remedy**: For every tool, assess whether its output is being acted upon. A deployed-but-ignored tool scores no higher than no tool at all.

### Mistake 3: Assessing the Security Team, Not the Engineering Organization

DevSecOps maturity is primarily a property of engineering organizations, not security teams. The security team can be highly capable and still serve an immature development organization. When assessors only interview security team members, they measure security team capability and miss the actual integration of security into development practice.

**Remedy**: Require interviews with engineering team leads, product managers, and individual developers as part of every domain assessment. If the security team is the only audience, the assessment is measuring the wrong thing.

### Mistake 4: Annual-Only Assessment

Annual assessments are insufficient to drive continuous improvement. They produce a momentary picture that is already outdated by the time it drives roadmap decisions. They also allow organizations to prepare for assessment periods rather than maintaining capabilities year-round — a form of gaming that annual cadence inadvertently encourages.

**Remedy**: Complement annual full assessments with quarterly domain-level check-ins and continuous metric monitoring. See the Continuous Assessment Cadence section.

### Mistake 5: Disconnecting Scores from Investments

A maturity score without a connected improvement roadmap and budget is decorative. Organizations that conduct maturity assessments but do not connect the results to specific investment decisions, engineering time allocation, and executive priorities will find that scores remain static year over year because nothing is actually changing.

**Remedy**: Assessment results must directly inform the annual security budget planning process. Each domain gap should map to a funded initiative with an owner, timeline, and success criteria.

### Mistake 6: Comparing Scores Across Domains Without Context

A Level 3 in Infrastructure Security and a Level 3 in Culture & Organization represent very different organizational efforts. Infrastructure security at Level 3 might be achievable with tooling investment; Culture at Level 3 requires sustained organizational change. Treating all domain scores as equivalent when allocating improvement effort will routinely result in tooling over-investment and culture/process under-investment.

**Remedy**: When discussing domain scores, always discuss the nature of the gap (tooling, process, or culture) separately from the size of the gap (score difference). Tooling gaps are generally faster and cheaper to close than culture gaps.

---

## How to Avoid Gaming the Model

Maturity models are vulnerable to gaming — particularly when scores have external consequences (compliance reporting, customer requirements, executive bonuses). These practices prevent gaming while maintaining a healthy, productive maturity program:

### Use Evidence Standards

Establish and publish the evidence standards for each score level. When stakeholders know that claiming a Level 3 in SAST requires being able to demonstrate that SAST is enforced (break-build) in all production-relevant pipelines — with pipeline configuration files as evidence — there is less opportunity to argue for a higher score based on intent or partial implementation.

### External Assessor Involvement

For high-stakes assessments (board reporting, major compliance requirements), engage an external assessor to validate internal scores. External assessors have no organizational incentive to inflate scores and bring benchmarking context from other organizations that internal assessors lack.

### Track Outcomes, Not Just Scores

If maturity scores improve while security outcomes worsen (more incidents, more open vulnerabilities, longer remediation times), the scores are wrong. Maintain a set of outcome metrics alongside maturity scores and treat significant divergence as a signal of gaming or scoring error.

### Anonymous Evidence Challenges

Create a mechanism for individual contributors to anonymously flag instances where stated practice diverges from actual practice. Engineers on the ground often know that the SAST scanner is deployed but that findings are routinely suppressed — information that doesn't reach assessors in structured interviews with managers.

### Score Reviews on Score Jumps

When a domain score improves by more than 0.5 between annual assessments without a clear explanation (specific funded initiative, known tooling deployment, documented process change), require a re-assessment of that domain with a different assessor to validate the improvement.

---

## Continuous Assessment Cadence

A mature maturity program does not rely solely on annual assessments. The recommended cadence:

### Annual: Full Assessment

Conduct a full eight-domain assessment using the complete questionnaire. Engage all stakeholder groups. Produce a formal assessment report with updated scores, findings, and roadmap recommendations. Use this to inform the upcoming budget cycle.

**Timing**: Align with budget planning cycle, typically Q3-Q4.

### Quarterly: Domain Check-In

Select 2-3 domains where active improvement initiatives are underway and conduct a lightweight check-in: review metrics updates, assess initiative completion status, update scores if criteria are demonstrably met. Use this to track progress on the roadmap and surface blockers.

**Output**: Updated domain scores for active improvement areas, roadmap status report, escalated blockers.

### Monthly: Metric Review

Review the security KPI dashboard for trend data across key metrics: MTTD, MTTR, vulnerability density, SAST gate pass rate, CSPM compliance score, training completion. This is not a formal assessment but a leading indicator review that warns of regression before it appears in formal assessment scores.

**Output**: Updated KPI trends, regression alerts, roadmap velocity metrics.

### Continuous: Tooling and Pipeline Monitoring

Deploy automated checks in pipelines and monitoring systems that continuously assess the operational state of security controls. SAST gate enforcement, secret scanning coverage, CSPM compliance scores, and certificate expiry status should be monitored continuously. These are lagging indicators of capability but leading indicators of operational failure.

---

## Using Metrics to Track Progression

Metrics should be selected based on their ability to serve as **leading indicators** of maturity advancement — they should change before the formal assessment score changes, providing early evidence that improvement initiatives are working (or not).

### Domain Metrics Map

| Domain | Leading Indicators | Lagging Indicators |
|--------|-------------------|--------------------|
| Culture & Org | Champion activity rate, developer-initiated security reports | Security NPS, training completion % |
| Security Requirements | Threat model coverage %, features with security acceptance criteria | Security requirements defect escape rate |
| Secure Development | SAST gate pass rate, pre-commit hook adoption %, dependency health score | Vulnerability density by team |
| CI/CD Security | Secrets scan finding rate, IaC scan pass rate, SBOM completeness | Supply chain incidents, pipeline security events |
| Testing & Validation | DAST scan frequency, security regression test coverage | Penetration test critical finding count |
| Infrastructure Security | CSPM compliance score, CIS benchmark pass rate | Misconfiguration-related incidents |
| Operations & Monitoring | Alert false positive rate, MTTD, playbook automation coverage | MTTR, incident severity distribution |
| Governance & Compliance | Exception count/age, risk register freshness, control owner response time | Audit findings, compliance gaps |

### Metric Selection Principles

**Prefer outcome metrics over activity metrics**: "Number of threat models completed" is an activity metric. "Percentage of significant features with current threat models" is an outcome metric. Both measure threat modeling, but the outcome metric tells you whether the practice is embedded or just occurring.

**Track trends, not snapshots**: A CSPM compliance score of 72% means nothing without context. A CSPM compliance score that has improved from 61% to 72% over six months while the number of monitored resources increased by 30% is a meaningful story.

**Disaggregate by team**: Organization-wide averages hide high-performing outliers and high-risk laggards. Track key metrics per team or application to identify where the real problems are.

**Avoid vanity metrics**: Lines of security code written, number of security issues filed, number of penetration testing hours — these metrics are easy to inflate and correlate poorly with actual security maturity.

---

## Communicating Results to Leadership

Effective communication of maturity assessment results requires translating security capability data into business-relevant language. Different audiences require different framings:

### Board-Level Communication

Boards respond best to:
- **Relative positioning**: "We are at Level 2.7, which places us in the top quartile of companies our size in this industry segment."
- **Trend direction**: "Our overall score has improved from 2.1 to 2.7 over the past 18 months, reflecting specific investments in [domains]."
- **Risk quantification**: "Our current security gaps create an estimated annual loss exposure of $X, which we are targeting to reduce to $Y through the roadmap investments of $Z."
- **Peer context**: "Three out of eight domains are below industry average for our sector; these are the focus of our current investment cycle."

Avoid: Technical detail, acronym-heavy security jargon, score-only reporting without context.

### Executive Leadership Communication

C-suite executives beyond the CISO want:
- **Investment ROI**: "The $X investment in SAST deployment has reduced vulnerability discovery costs by $Y annually by catching issues in development rather than production."
- **Business risk language**: "Our current Testing & Validation maturity creates risk of undetected API vulnerabilities in our customer-facing platform."
- **Competitive context**: "Our supply chain security practices are now at parity with major competitors following the CI/CD investments."
- **Decision items**: "Approving $X budget for the threat intelligence platform will enable us to advance Operations & Monitoring from Level 2 to Level 3 within 12 months."

### Engineering Leadership Communication

Engineering VPs and directors need:
- **Domain-level detail**: Specific scores and gap descriptions per domain
- **Team-level implications**: Which teams or applications represent the highest-risk gaps
- **Roadmap feasibility**: Realistic effort estimates for improvement initiatives
- **Engineering velocity impact**: Honest assessment of how security investments affect deployment frequency and lead time

### Broader Engineering Communication

When sharing results with engineering teams:
- Lead with team-level data, not overall scores
- Frame gaps as opportunities, not failures
- Celebrate specific improvements since the last assessment
- Be transparent about what is being invested in to close gaps

---

## Benchmarking Against Industry Peers

Benchmarking provides essential context for interpreting absolute maturity scores. A Level 2.5 is concerning in an industry where competitors average Level 3.5 and neutral in one where the average is 2.3.

### Benchmarking Sources

**BSIMM Annual Report**: The BSIMM (Building Security In Maturity Model) publishes annual data from over 100 participating organizations, covering software security practice adoption rates. While not using the same scoring model as the TDMM, BSIMM data provides valuable context for practice prevalence by industry vertical.

**Gartner Security and Risk Management Surveys**: Gartner publishes annual surveys of security spending, staffing, and capability across enterprise segments. Useful for benchmarking organizational structure and investment levels.

**CISO/Security Leadership Communities**: Peer communities (CISO Alliance, ISAC working groups, Cloud Security Alliance) provide informal benchmarking through practitioner discussion. Relationships built in these communities often yield frank, non-public benchmarking conversations.

**Security Vendors' Benchmark Reports**: Major security vendors (Snyk, Veracode, GitLab, Palo Alto) publish annual State of DevSecOps or similar reports drawing on their customer data. These are useful for tooling-specific benchmarking but often reflect the vendor's customer base rather than the full market.

### Interpreting Benchmark Data

Not all benchmark data is created equal. Apply these filters:
- **Industry alignment**: Security maturity expectations differ significantly between financial services, healthcare, government, and technology. Benchmark against your peer group.
- **Company size alignment**: A 5,000-person enterprise and a 50-person startup have different baseline security capabilities and different risk profiles.
- **Survey methodology**: Self-reported surveys are subject to the same gaming biases as internal assessments. Weight heavily surveyed-and-validated data over pure self-report.

### Using Benchmarks in Roadmapping

When benchmarking reveals that your organization is significantly below industry average in specific domains, treat this as a risk signal (peers have higher capability for reasons likely related to real threats in your shared industry environment) and a prioritization signal (industry-wide below-average domains are often the result of known, addressable capability gaps rather than uniquely difficult challenges).

Conversely, domains where you are above industry average represent potential competitive differentiators. Identify and protect these capabilities. Consider whether they represent opportunities for community contribution that enhances your employer brand and talent acquisition.
