# DevSecOps Maturity Model — Implementation Guide

## Table of Contents

1. [How to Conduct a Maturity Assessment](#how-to-conduct-a-maturity-assessment)
2. [Assessment Questionnaire](#assessment-questionnaire)
3. [Scoring Methodology](#scoring-methodology)
4. [Example Maturity Assessment Report Format](#example-maturity-assessment-report-format)
5. [Building a Roadmap from Assessment Results](#building-a-roadmap-from-assessment-results)
6. [Prioritization Framework](#prioritization-framework)
7. [Organizational Change Management](#organizational-change-management)

---

## How to Conduct a Maturity Assessment

### Step 1: Define Scope and Objectives (Week 1)

Before beginning any assessment activity, establish clear boundaries:

**Define organizational scope**: Is this a whole-organization assessment, a business unit assessment, or a specific product area assessment? The answer affects which stakeholders you engage, how you aggregate scores, and how you use results.

**Define assessment objectives**: Are you measuring baseline maturity for the first time? Tracking progress against a previous assessment? Preparing evidence for a compliance audit? The objective shapes how deeply you investigate each domain and how you communicate results.

**Identify assessment team**: A typical assessment team includes:
- Assessment lead (security architect or senior DevSecOps practitioner)
- Domain subject matter experts (1-2 per domain)
- Organizational sponsor (CISO or VP Engineering) who can mandate stakeholder participation

**Establish timeline**: Allow 4-6 weeks for a thorough first assessment. Subsequent assessments (annual cadence) can typically be completed in 2-3 weeks.

### Step 2: Stakeholder Identification and Scheduling (Week 1-2)

Map assessment participants to domains:

| Domain | Key Stakeholders to Interview |
|--------|------------------------------|
| Culture & Organization | CISO, VP Engineering, HR (training), Engineering Manager sample |
| Security Requirements | Security Architect, Product Manager, Senior Developer |
| Secure Development | Lead Developers, AppSec Engineers, DevOps Engineers |
| CI/CD Security | Platform Engineering Lead, Build/Release Engineers |
| Testing & Validation | QA Lead, AppSec/Penetration Tester, Red Team Lead |
| Infrastructure Security | Cloud Architect, SRE Lead, Platform Security Engineer |
| Operations & Monitoring | SOC Manager/Lead, SIEM Engineer, IR Lead |
| Governance & Compliance | Compliance Officer, Risk Manager, Legal (privacy) |

Schedule 60-90 minute structured interviews for each domain. Provide participants with the interview topics in advance but not the specific questions — this ensures they prepare genuinely rather than rehearsing answers.

### Step 3: Evidence Collection Planning (Week 2)

Create an evidence request list covering:

**Tool output evidence**:
- SAST scan results from last 90 days (finding counts, severity distribution, remediation rates)
- DAST scan results from last 6 months
- CSPM/cloud security posture reports
- Vulnerability management dashboard exports
- Pipeline configuration samples

**Process documentation evidence**:
- Incident response plan and runbooks
- Threat model templates and examples
- Secure coding standards
- Security training curriculum and completion records
- Risk register
- Exception/waiver log

**Metrics evidence**:
- Security KPI dashboard screenshots
- MTTD/MTTR reports (last 12 months)
- Vulnerability SLA compliance reports
- Security training completion reports
- Compliance audit findings (last 2 years)

### Step 4: Conduct Interviews (Week 2-3)

Follow the structured questionnaire in the next section. For each interview:

1. Open with context-setting: explain the model, the scoring methodology, and how results will be used
2. Emphasize that the assessment measures organizational capability, not individual performance — scores are not reflections on the people being interviewed
3. Follow the questionnaire but be prepared to probe for evidence: "Can you show me an example of that?" or "Where would I find evidence of that practice?"
4. Document responses in real time with direct quotes where possible
5. Note gaps between claimed practice and available evidence

### Step 5: Evidence Review (Week 3-4)

Review all collected evidence artifacts against the criteria for each domain and level. For each criterion, record:
- Whether evidence exists
- Quality of evidence (direct/objective vs. indirect/asserted)
- Any discrepancies between interview claims and evidence

### Step 6: Scoring and Calibration (Week 4)

Score each domain using the methodology in the Architecture document. If the assessment team has multiple members, conduct a calibration session:

1. Each assessor independently scores each domain
2. Compare scores and identify divergences greater than 0.5
3. For divergent scores, discuss the specific criteria causing disagreement
4. Arrive at consensus scores with documented rationale

### Step 7: Report Drafting and Review (Week 4-5)

Draft the assessment report following the format described below. Share a draft with:
- Organizational sponsor for factual review
- Key domain stakeholders to validate findings before final publication
- Not for score negotiation — factual corrections only

### Step 8: Results Presentation and Roadmap Initiation (Week 5-6)

Present results to leadership using the report format. Immediately initiate roadmap development using the gap analysis to identify top priorities. See the Roadmap Building section below.

---

## Assessment Questionnaire

The following questionnaire covers all eight domains with 4-5 questions per domain (39 questions total). Each question is scored 1-5 by the assessor based on interview responses, corroborated by evidence. Scores are then mapped to domain maturity levels.

### Domain 1: Culture & Organization (7 questions)

**Q1.01 — Security Responsibility Model**
*How is security responsibility distributed between the security team and engineering teams? Who is responsible when a vulnerability is found in production code?*

| Score | Criteria |
|-------|---------|
| 1 | Security team owns all security; engineering teams defer to security for all security decisions |
| 2 | Engineering teams have some security responsibilities but rely heavily on security team for guidance |
| 3 | Shared responsibility model documented; "you build it, you secure it" principle stated and mostly followed |
| 4 | Security ownership embedded in engineering team OKRs; security metrics tracked per team |
| 5 | Engineering teams are fully accountable for security outcomes; security team operates as consultant and enabler |

**Q1.02 — Security Champions Program**
*Do you have a security champions program? How are champions selected, supported, and measured?*

| Score | Criteria |
|-------|---------|
| 1 | No security champions program |
| 2 | Informal champions nominated in 1-2 teams; no dedicated time or training budget |
| 3 | Formal program with champions in all engineering teams; dedicated time allocation (10-20%); community of practice |
| 4 | Champions are senior engineers with measurable impact; program effectiveness tracked via metrics |
| 5 | Champions program is industry-recognized; champions present at external conferences; program replicated by peers |

**Q1.03 — Security Training**
*What security training do engineers receive? How is effectiveness measured?*

| Score | Criteria |
|-------|---------|
| 1 | Annual compliance training only; no role-specific security content |
| 2 | Security awareness training with completion tracking; some role-based modules |
| 3 | Role-specific training (developer secure coding, DevOps infra security, PM threat modeling); effectiveness tested |
| 4 | Training tied to vulnerability findings; developer security skills tracked; training ROI measured |
| 5 | Internal security research and training development; training program published externally |

**Q1.04 — Security Engagement in Development**
*At what stage does security get involved in new features or systems? How does that engagement happen?*

| Score | Criteria |
|-------|---------|
| 1 | Security engaged only at end of project or after incidents |
| 2 | Security consulted at architecture review for high-priority projects |
| 3 | Security involved at sprint planning; threat modeling at design phase mandatory |
| 4 | Security embedded in sprint teams; continuous security consultation; proactive risk identification |
| 5 | Security co-leads architecture and design decisions; anticipates future risks |

**Q1.05 — Security Culture Indicators**
*How do engineers talk about security? Is it seen as engineering quality or as an external requirement?*

| Score | Criteria |
|-------|---------|
| 1 | Security perceived as compliance overhead; developers work around security requirements |
| 2 | Security acknowledged as important but separate from core engineering quality |
| 3 | Security is part of code quality; included in PR review checklist; part of definition of done |
| 4 | Security metrics displayed alongside deployment frequency; engineering pride in security posture |
| 5 | Security innovation is a source of competitive pride; engineers volunteer for security projects |

**Q1.06 — Security in Hiring and Onboarding**
*How is security evaluated in engineering hiring? What security onboarding do new engineers receive?*

| Score | Criteria |
|-------|---------|
| 1 | Security not evaluated in hiring; no security-specific onboarding |
| 2 | Security mentioned in job descriptions; basic security onboarding module |
| 3 | Security competency assessed in interviews; structured security onboarding with tool access and standards |
| 4 | Security skills weighted in leveling criteria; onboarding includes hands-on security lab |
| 5 | Security expertise a competitive differentiator in talent acquisition; security reputation attracts engineers |

**Q1.07 — Executive Security Engagement**
*How frequently does security report to executive leadership? What is the quality of those conversations?*

| Score | Criteria |
|-------|---------|
| 1 | Security reports to leadership only after incidents |
| 2 | Quarterly security report to leadership; primarily focused on incidents and compliance |
| 3 | Monthly security dashboard; security KPIs in business review; CISO has direct board access |
| 4 | Security metrics in business operating cadence; executive security risk conversations data-driven |
| 5 | Board security committee; security strategy integrated into business strategy; external recognition |

---

### Domain 2: Security Requirements (4 questions)

**Q2.01 — Threat Modeling Practice**
*Do you conduct threat modeling? For what projects? What methodology do you use? Who participates?*

| Score | Criteria |
|-------|---------|
| 1 | Threat modeling not practiced or done ad hoc by individual security experts only |
| 2 | Threat modeling done for critical projects by security architects; no standard methodology |
| 3 | Threat modeling mandatory for significant features; standard methodology (STRIDE/PASTA); developer participation |
| 4 | Threat models maintained continuously; risk-scored; integrated with vulnerability management |
| 5 | AI-assisted threat modeling; threat intelligence automatically updates threat models |

**Q2.02 — Security Requirements Process**
*How are security requirements defined for new features? Where do they come from? How are they tracked?*

| Score | Criteria |
|-------|---------|
| 1 | No formal security requirements process; security requirements ad hoc or absent |
| 2 | Security requirements checklist used for critical projects; requirements documented |
| 3 | Security user stories in backlog; security acceptance criteria in definition of done; traceability to test cases |
| 4 | Risk-scored requirements; requirements prioritization informed by threat model findings |
| 5 | Automated requirements generation from system architecture analysis |

**Q2.03 — Abuse Case Definition**
*Do you define abuse cases or misuse cases for features? How are they used in testing?*

| Score | Criteria |
|-------|---------|
| 1 | Abuse cases not defined |
| 2 | Abuse cases defined for highest-risk features informally |
| 3 | Abuse cases defined systematically during design; linked to security test cases |
| 4 | Abuse cases used to drive automated security test generation |
| 5 | Adversarial modeling drives product design decisions; abuse cases shared with industry |

**Q2.04 — Privacy by Design**
*How are privacy requirements identified and integrated into design? Who is responsible?*

| Score | Criteria |
|-------|---------|
| 1 | Privacy requirements identified only when legally required or after incident |
| 2 | Privacy checklist used for data-handling features |
| 3 | Privacy impact assessment mandatory for data-processing features; DPO involved at design |
| 4 | Privacy risk quantified; privacy engineering built into platform capabilities |
| 5 | Privacy-by-design maturity shared publicly; regulatory engagement on privacy standards |

---

### Domain 3: Secure Development (5 questions)

**Q3.01 — SAST Deployment and Enforcement**
*Is SAST in your pipelines? Is it enforced (break-build)? What tools? What coverage?*

| Score | Criteria |
|-------|---------|
| 1 | No SAST in pipelines |
| 2 | SAST deployed in some pipelines; results reported but not enforced |
| 3 | SAST required in all pipelines; break-build on high/critical; false positive rate managed |
| 4 | SAST tuned with custom rules; vulnerability density tracked per team; remediation SLA enforced |
| 5 | Predictive vulnerability modeling; ML-augmented SAST; custom rules open-sourced |

**Q3.02 — Dependency Security Management**
*How do you manage the security of open-source dependencies? What happens when a CVE is published for a dependency you use?*

| Score | Criteria |
|-------|---------|
| 1 | Dependencies not tracked; CVE response ad hoc or absent |
| 2 | Dependency scanning in place; process for reviewing critical CVEs |
| 3 | SCA enforced in pipelines with policy; SLA for vulnerability remediation by severity |
| 4 | Dependency health portfolio tracked; automated PR creation for upgrades; SBOM maintained |
| 5 | SBOM published; contribution to dependency security ecosystem; novel SCA tooling |

**Q3.03 — Secure Coding Standards**
*Do you have secure coding standards? How are they maintained and enforced?*

| Score | Criteria |
|-------|---------|
| 1 | No secure coding standards or outdated/ignored documentation |
| 2 | Secure coding standards documented; developers aware but not systematically trained |
| 3 | Standards maintained, versioned, and trained; referenced in code review process |
| 4 | Standards enforced via automated linting and SAST rules; effectiveness tracked |
| 5 | Standards published externally; contribution to industry secure coding resources |

**Q3.04 — Security-Focused Code Review**
*How does security feature in code reviews? Are reviewers trained to identify security issues?*

| Score | Criteria |
|-------|---------|
| 1 | Code review does not systematically address security |
| 2 | Security mentioned in code review guidelines; some reviewers security-aware |
| 3 | Security review checklist in PR process; security-aware reviewers required for sensitive changes |
| 4 | Security review effectiveness tracked; security findings from review tracked and fed back to training |
| 5 | AI-augmented security code review; security review methodology published |

**Q3.05 — Pre-Commit Security Tooling**
*What security tooling do developers have in their local development environment?*

| Score | Criteria |
|-------|---------|
| 1 | No developer-facing security tooling |
| 2 | IDE security plugins available but not standardized |
| 3 | IDE security plugins deployed as standard; pre-commit hooks for secrets scanning |
| 4 | Developer security tooling integrated into feedback loop metrics |
| 5 | Custom developer security tooling built and published |

---

### Domain 4: CI/CD Security (5 questions)

**Q4.01 — Secrets Management**
*How are secrets (API keys, credentials, certificates) managed? Are there any known secrets in code repositories?*

| Score | Criteria |
|-------|---------|
| 1 | Secrets in code repositories or configuration files; no vault |
| 2 | Vault adopted for some applications; secrets scanning runs but not all remediations complete |
| 3 | Vault for all environments; no hardcoded secrets; pre-commit and pipeline scanning enforced |
| 4 | Secret rotation automated; access to secrets audited and reviewed; secrets health metrics tracked |
| 5 | Zero-trust secrets management; dynamic secrets for all credentials; research contribution |

**Q4.02 — Pipeline Hardening and Access Control**
*How are CI/CD pipelines protected? What are the access controls on pipeline definitions?*

| Score | Criteria |
|-------|---------|
| 1 | Pipelines not treated as security-sensitive; broad access permissions |
| 2 | Pipeline access reviewed; some hardening applied |
| 3 | Pipeline definitions as code with review requirements; least-privilege service accounts; separation of duties |
| 4 | Pipeline security metrics tracked; anomaly detection on pipeline behavior |
| 5 | SLSA Level 3+ compliance; pipeline integrity attestation; supply chain security research |

**Q4.03 — Container and Artifact Security**
*How are container images scanned? What happens when a critical vulnerability is found in a base image?*

| Score | Criteria |
|-------|---------|
| 1 | Container images not scanned |
| 2 | Container scanning runs; results reviewed periodically |
| 3 | Container scanning enforced with break-build; base image policy; image signing |
| 4 | Runtime container security monitoring; admission control enforcement; image provenance tracked |
| 5 | Binary authorization in all environments; custom container security tooling |

**Q4.04 — IaC Security Scanning**
*Is infrastructure-as-code scanned for security issues before deployment? What tools?*

| Score | Criteria |
|-------|---------|
| 1 | IaC not scanned |
| 2 | IaC scanning runs periodically or in some pipelines |
| 3 | IaC scanning enforced in all infrastructure pipelines with policy thresholds |
| 4 | Custom IaC security rules; IaC security debt tracked; drift detection active |
| 5 | Novel IaC security research; custom policy frameworks published |

**Q4.05 — Software Supply Chain Security**
*How do you verify the integrity and provenance of artifacts and dependencies used in your build pipelines? Do you generate and maintain SBOMs?*

| Score | Criteria |
|-------|---------|
| 1 | No supply chain security controls; third-party dependencies fetched directly from public registries without verification |
| 2 | Dependency scanning (SCA) in place; some dependency pinning; no SBOM generation |
| 3 | All dependencies pinned to exact versions with hash verification; SBOM generated for production artifacts; artifact signing implemented; private registry mirror in use |
| 4 | SBOM fleet management platform deployed (Dependency-Track equivalent); CVE-to-fleet query capability; SLSA provenance generated; signing enforced at admission |
| 5 | SLSA Level 3+ compliance; published SBOMs for externally distributed software; VEX publishing process; supply chain security research contribution |

---

### Domain 5: Testing & Validation (5 questions)

**Q5.01 — Dynamic Application Security Testing (DAST)**
*Where and how frequently is DAST run? Is it automated?*

| Score | Criteria |
|-------|---------|
| 1 | No DAST |
| 2 | DAST run periodically; manual process |
| 3 | DAST automated in staging pipeline; runs on every release candidate |
| 4 | Continuous DAST in production (synthetic/canary approach); DAST findings tracked as security KPI |
| 5 | Novel DAST techniques for cloud-native apps; contribution to DAST tooling open source |

**Q5.02 — Penetration Testing Program**
*How often is penetration testing conducted? How are findings managed and tracked?*

| Score | Criteria |
|-------|---------|
| 1 | Penetration testing not conducted or done ad hoc |
| 2 | Annual penetration test; findings documented; remediation tracked informally |
| 3 | Semi-annual penetration testing; formal finding management; remediation SLAs; regression testing |
| 4 | Quarterly red team exercises; findings vs. self-assessment gap tracked; threat-intel-driven scope |
| 5 | Continuous adversarial simulation team; findings shared with community; novel attack research |

**Q5.03 — Security Regression Testing**
*Do you have automated security regression tests? How are they maintained?*

| Score | Criteria |
|-------|---------|
| 1 | No security regression tests |
| 2 | Security regression tests exist for some previously exploited vulnerabilities |
| 3 | Security regression suite in CI covering all historically significant findings; maintained with each release |
| 4 | Security regression suite tied to threat model; coverage metrics tracked |
| 5 | AI-generated security regression tests; novel test generation research |

**Q5.04 — API Security Testing**
*How are APIs tested for security issues? What tools?*

| Score | Criteria |
|-------|---------|
| 1 | APIs not security tested beyond general penetration test |
| 2 | API security testing included in annual penetration test |
| 3 | Automated API security testing (OWASP API Top 10 coverage) in CI/CD pipeline |
| 4 | Continuous API security monitoring; API inventory complete and maintained |
| 5 | API security research; novel API testing methodology published |

**Q5.05 — Fuzz Testing and IAST**
*Is fuzz testing used for any components? Is Interactive Application Security Testing (IAST) deployed for instrumented runtime testing?*

| Score | Criteria |
|-------|---------|
| 1 | No fuzz testing or IAST |
| 2 | Fuzz testing used ad hoc for high-value components by security team |
| 3 | Continuous fuzzing (OSS-Fuzz / libFuzzer / AFL++) integrated for parsing and input-handling components; IAST deployed in QA environment for at least one language stack |
| 4 | Fuzzing corpus maintained and growing; IAST findings tracked alongside SAST; language runtime instrumentation in staging |
| 5 | Internal fuzzing research; vulnerability discovery shared with upstream; novel fuzzing infrastructure |

---

### Domain 6: Infrastructure Security (4 questions)

**Q6.01 — Cloud Security Posture Management**
*How is cloud misconfiguration detected and managed? What CSPM tools are in use?*

| Score | Criteria |
|-------|---------|
| 1 | No CSPM; cloud configuration reviewed manually or not at all |
| 2 | CSPM deployed; findings reviewed periodically |
| 3 | CSPM with active alert monitoring; compliance score tracked; critical misconfigurations SLA-managed |
| 4 | Compliance score KPI in executive dashboard; automated remediation for common findings; drift detection |
| 5 | Self-healing infrastructure; AI-assisted anomaly detection; CSPM research published |

**Q6.02 — Kubernetes / Container Platform Security**
*How is Kubernetes cluster security managed? Are Pod Security Standards enforced?*

| Score | Criteria |
|-------|---------|
| 1 | No Kubernetes security controls; default configurations |
| 2 | Basic pod security; network policies in some namespaces |
| 3 | Pod Security Standards enforced; network policies comprehensive; CIS K8s Benchmark met |
| 4 | Admission control with Kyverno/OPA; runtime security monitoring (Falco/equivalent); workload identity |
| 5 | Service mesh with mTLS everywhere; zero-trust Kubernetes; novel K8s security research |

**Q6.03 — IAM and Access Control**
*How is cloud IAM managed? Is least privilege enforced? How are access reviews conducted?*

| Score | Criteria |
|-------|---------|
| 1 | IAM not systematically managed; over-permissive roles common |
| 2 | IAM review conducted periodically; some least-privilege enforcement |
| 3 | IAM least privilege enforced at provisioning; quarterly access reviews; no standing administrative access |
| 4 | Just-in-time access for privileged operations; access analytics tracked; automated anomaly detection |
| 5 | AI-assisted access review; novel least-privilege research; workload identity everywhere |

**Q6.04 — Infrastructure-as-Code Security Practices**
*Is all infrastructure defined as code? How is IaC change managed from a security perspective?*

| Score | Criteria |
|-------|---------|
| 1 | Infrastructure managed manually; limited IaC adoption |
| 2 | IaC adopted for most infrastructure; change process informal |
| 3 | 100% IaC with security review required; scanned before apply; drift detection |
| 4 | IaC security debt tracked; automated remediation of drift; compliance policy as code |
| 5 | Policy as code research; IaC security tooling contributions; novel drift detection approaches |

---

### Domain 7: Operations & Monitoring (4 questions)

**Q7.01 — Security Logging and SIEM**
*What security events are logged? Is there a centralized SIEM? What is the alert false positive rate?*

| Score | Criteria |
|-------|---------|
| 1 | Minimal logging; no centralized SIEM or SIEM not actively monitored |
| 2 | Centralized logging; SIEM with basic alert rules; alert triage process |
| 3 | Security logging standards enforced; SIEM tuned (<20% false positive rate); 24/7 monitoring |
| 4 | ML anomaly detection; threat intelligence integrated; MTTD tracked with SLA |
| 5 | Threat hunting operations; autonomous detection for Tier 1 incidents; threat intelligence produced |

**Q7.02 — Incident Response Capability**
*When was the IR plan last tested? How long does it take to contain a critical incident?*

| Score | Criteria |
|-------|---------|
| 1 | IR undocumented; response improvised |
| 2 | IR plan documented; contact lists maintained; basic runbooks |
| 3 | IR runbooks tested semi-annually via tabletop; MTTR tracked; communication chains tested |
| 4 | SOAR automation for common playbooks; MTTR KPI with SLA; purple team exercises |
| 5 | Autonomous IR for Tier 1-2; IR research published; industry collaboration on IR standards |

**Q7.03 — Threat Intelligence Consumption**
*What threat intelligence sources do you consume? How is TI operationalized into detection rules?*

| Score | Criteria |
|-------|---------|
| 1 | No formal TI consumption |
| 2 | Public threat feeds consumed; manual review by security team |
| 3 | TI feeds automatically integrated into SIEM rules; ISAC membership; TI review cadence |
| 4 | TI operationalized into automated detection; TI coverage tracked by MITRE ATT&CK mapping |
| 5 | TI produced and shared with community; TI research; novel TI integration approaches |

**Q7.04 — Security Observability**
*Can you answer "what happened" for a security incident within 1 hour? What tooling enables this?*

| Score | Criteria |
|-------|---------|
| 1 | Cannot reconstruct incident timeline from logs |
| 2 | Incident timeline reconstructable from logs with significant manual effort |
| 3 | Security observability tooling enables rapid timeline reconstruction; log retention policy enforced |
| 4 | Automated incident timeline generation; forensic tooling deployed; evidence preservation automated |
| 5 | Real-time attack path visualization; novel forensic tooling; DFIR research |

---

### Domain 8: Governance & Compliance (5 questions)

**Q8.01 — Risk Management**
*How is security risk managed? Is there a risk register? How are risk decisions made?*

| Score | Criteria |
|-------|---------|
| 1 | No formal risk management; risks not documented |
| 2 | Risk register exists for major risks; informal review |
| 3 | Risk register with owners; regular review cycle; formal risk acceptance process |
| 4 | Quantitative risk model (FAIR or equivalent); risk metrics in executive dashboard; risk-driven investment |
| 5 | Automated risk quantification; risk model published; contribution to risk management standards |

**Q8.02 — Policy Management**
*How are security policies maintained? How frequently reviewed? How is compliance tracked?*

| Score | Criteria |
|-------|---------|
| 1 | Security policies outdated or informal; compliance not tracked |
| 2 | Core policies documented and reviewed annually |
| 3 | Policy review cycle enforced; exception process; compliance tracking per policy |
| 4 | Automated policy compliance monitoring; policy effectiveness metrics; exception aging tracked |
| 5 | AI-assisted policy generation; policy-as-code; policy research published |

**Q8.03 — Compliance Control Management**
*Which compliance frameworks apply? How are controls mapped and ownership assigned?*

| Score | Criteria |
|-------|---------|
| 1 | Compliance frameworks identified; controls not systematically mapped |
| 2 | Controls mapped to frameworks; owners identified |
| 3 | Continuous compliance monitoring; gap tracking; automated evidence collection for some controls |
| 4 | Real-time compliance dashboard; automated evidence collection for majority of controls; always audit-ready |
| 5 | Regulatory engagement; predictive compliance; compliance research and publication |

**Q8.04 — Third-Party Risk Management**
*How is third-party security risk assessed? What happens when a critical vendor has a security incident?*

| Score | Criteria |
|-------|---------|
| 1 | Third-party risk not systematically assessed |
| 2 | Security questionnaires for critical vendors; review process |
| 3 | Tiered third-party assessment program; continuous monitoring for critical vendors |
| 4 | Automated questionnaire and evidence collection; real-time vendor risk scoring |
| 5 | Industry collaboration on third-party risk standards; novel vendor risk methodology |

**Q8.05 — Security Metrics and Reporting**
*What security metrics are reported to leadership? How frequently? In what format?*

| Score | Criteria |
|-------|---------|
| 1 | Security reports only after incidents |
| 2 | Quarterly security reports; incident-focused |
| 3 | Monthly security dashboard; KPIs tracked; trend analysis |
| 4 | Real-time executive security dashboard; risk-adjusted metrics; board security report |
| 5 | Published security metrics methodology; industry benchmark contribution |

---

## Scoring Methodology

### Step 1: Score Each Question

For each of the 37 questions, assign a score from 1-5 based on the rubric criteria, supported by evidence. Record the evidence basis for each score.

### Step 2: Calculate Domain Scores

Average the question scores within each domain, then apply the threshold anchoring described in the Architecture document to arrive at the final domain score.

### Step 3: Apply Domain Weights

Multiply each domain score by its weight (see Architecture document) and sum for the overall score.

### Step 4: Apply Floor Rules

Check that no domain falls below the minimum required for the claimed overall level.

---

## Example Maturity Assessment Report Format

```
DEVSECOPS MATURITY ASSESSMENT REPORT
Organization: [Name]
Assessment Date: [Date]
Assessment Team: [Names]
Assessment Scope: [Scope Description]

EXECUTIVE SUMMARY
-----------------
Overall Maturity Score: 2.7 (Transitioning Level 2 → 3)

The organization has established foundational DevSecOps practices and is
progressing toward consistent, organization-wide security integration.
Core tooling (SAST, CSPM, SIEM) is in place and basic processes are
documented. Key gaps exist in CI/CD security hardening, automated testing,
and quantitative risk management.

Top 3 Strengths:
1. Infrastructure Security (3.0): CSPM deployed with active monitoring;
   CIS benchmark compliance improving
2. Secure Development (2.8): SAST deployed with enforced thresholds in
   most pipelines; secure coding standards maintained
3. Governance & Compliance (2.8): Compliance control mapping complete;
   exception process operational

Top 3 Gaps:
1. Testing & Validation (2.0): DAST not automated; penetration testing
   annual only; no security regression suite
2. Culture & Organization (2.2): Security champions program informal;
   security training not role-specific
3. CI/CD Security (2.3): Secrets management incomplete; IaC scanning
   not in all infra pipelines

DOMAIN SCORES
-------------
Domain                  | Score | Weight | Weighted
------------------------|-------|--------|--------
Culture & Organization  | 2.2   | 10%    | 0.22
Security Requirements   | 2.6   | 12%    | 0.31
Secure Development      | 2.8   | 15%    | 0.42
CI/CD Security          | 2.3   | 15%    | 0.35
Testing & Validation    | 2.0   | 12%    | 0.24
Infrastructure Security | 3.0   | 14%    | 0.42
Operations & Monitoring | 2.6   | 12%    | 0.31
Governance & Compliance | 2.8   | 10%    | 0.28
------------------------|-------|--------|--------
OVERALL                 | 2.55  | 100%   | 2.55

DOMAIN FINDINGS (Summary — full detail in appendix)
----------------------------------------------------
[One paragraph per domain covering key findings, evidence reviewed,
and specific gaps identified]

RECOMMENDED ROADMAP (High Level)
---------------------------------
0-6 months (Quick Wins):
- Automate DAST in staging pipeline
- Complete secrets migration to vault for all applications
- Formalize security champions program with dedicated time allocation

6-12 months (Foundation Building):
- Implement security regression testing suite
- Deploy IaC scanning in all infrastructure pipelines
- Conduct first red team exercise

12-18 months (Level 3 Completion):
- Achieve consistent SAST enforcement across all teams
- Implement threat modeling for all significant features
- Deploy SOAR for incident response automation

EVIDENCE INVENTORY
------------------
[Table listing all evidence artifacts reviewed, with source and date]

ASSESSMENT METHODOLOGY NOTE
----------------------------
[Description of assessment approach, interviews conducted, evidence
reviewed, any limitations or scope exclusions]
```

---

## Building a Roadmap from Assessment Results

### Step 1: Gap Analysis

For each domain, list the specific criteria from the next level that are not currently met. Group these into:
- **Capability gaps**: Missing practices or processes
- **Tooling gaps**: Missing or underutilized tooling
- **Organizational gaps**: Missing roles, responsibilities, or skills

### Step 2: Quick Win Identification

Identify improvements that can be achieved within 90 days with low organizational friction. Quick wins are typically:
- Tool deployments with existing vendor relationships
- Process formalization of practices already happening informally
- Training programs
- Policy updates

Quick wins matter disproportionately for organizational change management — they demonstrate momentum and build confidence in the maturity improvement program.

### Step 3: Dependency Mapping

Some improvements are prerequisites for others. Map these dependencies:
- SAST enforcement requires tuning (reducing false positives) before break-build thresholds make sense
- SOAR automation requires documented runbooks as input
- Quantitative risk management requires a risk register as foundation

### Step 4: Effort and Impact Estimation

For each improvement initiative, estimate:
- **Effort**: Engineering weeks, elapsed time, organizational difficulty
- **Impact**: Expected score improvement, risk reduction, compliance benefit

### Step 5: Sequence and Timeline

Sequence improvements based on:
1. Dependencies (prerequisites must come first)
2. Quick wins (front-load to demonstrate momentum)
3. Risk reduction priority (highest-risk gaps first)
4. Organizational readiness (choose improvements where the organization is ready to adopt)

---

## Prioritization Framework

Use the following scoring matrix to prioritize improvements:

| Factor | Weight | Scoring |
|--------|--------|---------|
| Risk reduction impact | 30% | 1-5 (5 = highest risk reduction) |
| Implementation ease | 20% | 1-5 (5 = easiest to implement) |
| Compliance benefit | 20% | 1-5 (5 = strongest compliance improvement) |
| Organizational readiness | 15% | 1-5 (5 = high readiness) |
| Score improvement | 15% | 1-5 (5 = largest maturity score gain) |

**Priority score = Σ (Factor score × Weight)**

Initiatives with priority scores above 3.5 are Tier 1 priorities. Scores between 2.5 and 3.5 are Tier 2. Below 2.5 are Tier 3 (deferred).

---

## Organizational Change Management for Maturity Advancement

Maturity advancement is fundamentally a change management challenge. Technical gaps are usually easier to close than organizational and cultural ones.

### Change Management Principles

**Sponsor visibility**: The CISO or VP Engineering must visibly champion the maturity program. When security requirements create short-term friction (SAST break-builds failing releases, for example), engineers need to see that leadership views this as acceptable and expected friction on the path to maturity.

**Engineering partnership**: Present maturity improvements as making engineers' lives better, not harder. SAST break-builds catch vulnerabilities before they become production incidents — that protects engineers from on-call pain. Threat modeling prevents having to re-architect systems after they're built.

**Celebrate progress**: Recognize teams that achieve maturity milestones. Publish domain scores transparently (within the organization) to create healthy competition.

**Incremental rollout**: Do not attempt to jump from Level 1 to Level 3 across all domains simultaneously. Choose 2-3 domains for focused improvement each quarter.

**Address resistance directly**: The most common sources of resistance are fear of blame (if scores are low), fear of slowdown (security gates), and tool fatigue (too many new tools). Address each directly with clear communication and realistic expectations.

---

## Domain 9: Automation Capability Assessment

The eight core assessment domains evaluate security practice maturity. This supplementary domain evaluates the maturity of the DevSecOps tooling stack itself — an organization can score Level 3 on process practices while operating immature, fragile automation that limits its ability to sustain those practices at scale.

### Assessment Questions — Automation Capability

**Q9.1 — Scan result coverage and completeness**
> What percentage of repositories in the organization have automated SAST, SCA, and secrets scanning configured and actively running?

| Level | Description | Evidence |
|---|---|---|
| 1 | < 25% of repositories covered | Manual review of pipeline configurations |
| 2 | 25–74% covered; gaps tracked in backlog | Coverage dashboard or inventory |
| 3 | 75–94% covered; coverage monitored automatically | Automated coverage report; gaps have owners and deadlines |
| 4 | ≥ 95% covered; new repos auto-enrolled | Enrollment automation; exception list reviewed quarterly |
| 5 | 100% coverage enforced; repo creation fails if pipeline not configured | Policy-as-code gate on repository provisioning |

**Q9.2 — False positive rate and tuning maturity**
> What is the current false positive rate for SAST findings, and what is the process for tuning the tooling?

| Level | Description |
|---|---|
| 1 | False positive rate unknown; no measurement |
| 2 | FP rate estimated informally; ad-hoc tuning when engineers complain |
| 3 | FP rate measured per tool quarterly; documented tuning process exists |
| 4 | FP rate tracked monthly by tool and by team; tuning SLAs defined (resolve high-FP rules within 30 days) |
| 5 | FP rate < 15% for all tools; automated anomaly detection alerts when a rule's FP rate exceeds threshold |

**Q9.3 — Mean time to detection (MTTD) for new vulnerabilities**
> How quickly does the organization detect that a newly disclosed CVE affects production services?

| Level | Description |
|---|---|
| 1 | Days to weeks; reactive (discovered via external notification or incident) |
| 2 | < 5 business days; periodic manual SCA scans or Dependabot alerts |
| 3 | < 24 hours; continuous SCA with daily scan runs and automated notifications |
| 4 | < 4 hours; event-driven scanning triggered by new CVE publication (webhook from NVD/GHSA) |
| 5 | < 1 hour; SBOM fleet query executed automatically on CVE publication; affected services notified before manual review begins |

**Q9.4 — Security finding triage automation**
> What percentage of security findings are automatically triaged (classified, prioritized, and routed) without requiring manual triage for each finding?

| Level | Description |
|---|---|
| 1 | 0%; all findings require manual triage from a shared queue |
| 2 | < 25%; duplicate suppression via tool configuration; severity-based routing |
| 3 | 25–59%; VEX documents suppress known-non-exploitable findings; auto-close for fixed-version upgrades |
| 4 | 60–84%; AI-assisted triage with human review for High/Critical; auto-close for Medium and below when VEX present |
| 5 | ≥ 85% auto-triaged with full audit trail; human triage required only for Critical findings and novel vulnerability patterns |

**Q9.5 — Tooling stack observability**
> Does the organization have visibility into the performance and reliability of its security tooling pipeline?

| Level | Description |
|---|---|
| 1 | No monitoring; tool failures are discovered when someone notices missing scan results |
| 2 | Basic alerting on pipeline failures; scan completion tracked manually |
| 3 | Dashboard shows scan success rate, scan duration, and coverage per tool; alert on failure |
| 4 | SLAs defined for scan tools (e.g., SAST must complete in < 5 minutes for 95% of builds); SLA violations trigger PagerDuty |
| 5 | Full observability: coverage, latency, FP rate, finding age, escape rate — all monitored with automated trend analysis |

**Q9.6 — Tooling update and CVE response for security tools**
> How quickly are the security tools themselves (Semgrep, Trivy, Checkov, etc.) updated when they have known vulnerabilities or significant rule improvements?

| Level | Description |
|---|---|
| 1 | No update process; tools may be years out of date |
| 2 | Manual updates on an ad-hoc basis; no tracking of tool versions |
| 3 | Dependabot or Renovate manages tool version updates; updates reviewed weekly |
| 4 | Tool updates tested in staging pipeline before production rollout; CVE patches applied within 7 days |
| 5 | Fully automated tool update pipeline with behavioral tests validating that update does not increase FP rate or change findings on known-vulnerable test fixtures |

### Automation Capability Score

The Automation Capability domain is weighted at **10%** of the composite TDMM score. It is intentionally lower-weighted than process and people domains because automation capability is a means to an end — high automation with poor process produces unreliable, misleading security signals.

| Score Range | Interpretation |
|---|---|
| 1.0–1.9 | Automation is a blocker: practices cannot be sustained at scale without improvement |
| 2.0–2.9 | Automation supports basic DevSecOps; scaling to the full organization will expose gaps |
| 3.0–3.9 | Automation is adequate for current scale; invest in coverage and observability |
| 4.0–5.0 | Automation is a differentiator; focus on fine-tuning and emerging threat integration |

**Measure enablement, not gatekeeping**: Track metrics that demonstrate security enabling velocity (finding vulnerabilities before production, preventing incidents) rather than only metrics that emphasize blockage (failed gates, rejected deployments).
