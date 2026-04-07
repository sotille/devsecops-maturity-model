# Introduction to the Techstream DevSecOps Maturity Model

## Table of Contents

1. [Purpose of Maturity Models in DevSecOps](#purpose-of-maturity-models-in-devsecops)
2. [Reference Frameworks and Inspirations](#reference-frameworks-and-inspirations)
3. [Why Organizations Need Structured Maturity Assessment](#why-organizations-need-structured-maturity-assessment)
4. [How This Model Differs From and Complements Existing Frameworks](#how-this-model-differs-from-and-complements-existing-frameworks)
5. [Target Audience](#target-audience)
6. [How to Read and Use This Document](#how-to-read-and-use-this-document)
7. [Quick-Start Assessment Guide](#quick-start-assessment-guide)
8. [Common Assessment FAQ](#common-assessment-faq)

---

## Purpose of Maturity Models in DevSecOps

DevSecOps represents the integration of security practices into every phase of the software development lifecycle — from design and coding through testing, deployment, and operations. The discipline emerged from the recognition that traditional security models, bolted on at the end of development cycles, were insufficient for organizations moving at the pace demanded by agile and DevOps methodologies.

However, "DevSecOps" is not a binary state. Organizations do not simply achieve DevSecOps and stop — they progress through increasingly sophisticated levels of security capability. A maturity model provides the language, structure, and measurement framework to describe and track that progression systematically.

Maturity models serve several critical purposes in this context:

**Diagnosis**: They provide a structured method for assessing where an organization currently stands, with enough granularity to identify specific gaps rather than producing a vague overall impression.

**Direction**: By defining what higher maturity looks like, they give organizations a clear target state to aim for, removing ambiguity from improvement planning.

**Communication**: Maturity levels create a shared vocabulary that enables productive conversations between security teams, engineering organizations, executive leadership, and boards. Saying "we are at Level 2 in CI/CD Security and targeting Level 3 within 18 months" conveys far more than generic statements about improving security posture.

**Measurement**: They provide a framework for demonstrating progress over time, converting security investment into trackable outcomes rather than activity metrics.

**Prioritization**: With limited budgets and engineering capacity, maturity models help organizations identify the highest-leverage improvements and sequence them rationally rather than pursuing the most recently discovered gap.

In DevSecOps specifically, maturity models address a challenge that pure compliance frameworks do not: they measure _capability_ rather than _configuration_. A system can be configured to pass a compliance check while remaining fundamentally insecure because the people and processes around it lack the maturity to maintain and respond to it. Maturity models capture this organizational dimension.

---

## Reference Frameworks and Inspirations

The Techstream DevSecOps Maturity Model is informed by decades of research and practical experience codified in several influential frameworks. Understanding these foundations helps practitioners contextualize the TDMM and appreciate the choices made in its design.

### CMMI (Capability Maturity Model Integration)

Originally developed at Carnegie Mellon University's Software Engineering Institute, CMMI is the archetype of five-level maturity models. Its structure — Initial, Managed, Defined, Quantitatively Managed, Optimizing — provides the foundational level taxonomy adopted (with customization) by the TDMM. CMMI demonstrated that process maturity follows predictable, measurable stages and that organizations can be assessed reliably against those stages. The TDMM borrows this level structure while replacing CMMI's process area focus with security-specific domain content.

### OWASP Software Assurance Maturity Model (SAMM)

OWASP SAMM is the most widely adopted application security maturity model in the industry. It organizes software security into five business functions (Governance, Design, Implementation, Verification, Operations), each containing three security practices, each with two streams assessed at three maturity levels. SAMM's depth in application security practices — particularly threat modeling, security testing, and secure build — directly informs the TDMM's Security Requirements, Secure Development, and Testing & Validation domains. However, SAMM predates the widespread adoption of cloud-native architectures and modern CI/CD pipelines, leaving gaps that the TDMM explicitly addresses.

### BSIMM (Building Security In Maturity Model)

Unlike prescriptive frameworks, BSIMM is an observational model — it describes what organizations with mature software security programs actually do, based on annual surveys of hundreds of participating enterprises. BSIMM's data-driven foundation gives it exceptional empirical credibility and makes it an excellent benchmark tool. The TDMM draws on BSIMM's activity catalog and observed prevalence rates to validate that its domain criteria reflect real-world practice rather than aspirational theory. BSIMM's twelve practice areas and 122 observed activities serve as a reference for the completeness of TDMM's coverage.

### NIST Cybersecurity Framework (CSF)

The NIST CSF's five core functions — Identify, Protect, Detect, Respond, Recover — provide an organizing principle for security operations that the TDMM incorporates into its Operations & Monitoring and Governance & Compliance domains. The CSF's tiered implementation model (Partial, Risk Informed, Repeatable, Adaptive) also informs how the TDMM characterizes organizational behavior at each level.

### CIS DevSecOps Guide and NIST SSDF

The CIS DevSecOps Guide and NIST's Secure Software Development Framework (SSDF, SP 800-218) provide prescriptive control catalogs that the TDMM maps to its domain criteria, particularly for CI/CD Security and Secure Development. These references ensure that the TDMM's domain criteria align with recognized industry standards and regulatory expectations.

---

## Why Organizations Need Structured Maturity Assessment

Despite the proliferation of security tooling and the universal acknowledgment that DevSecOps is essential, most organizations lack a systematic method for assessing the effectiveness of their security program. The consequences are predictable:

**Investment Misalignment**: Without a clear picture of where the organization stands, security investments are often driven by vendor presentations, recent incidents, or compliance mandates rather than systematic gap analysis. Organizations routinely over-invest in tooling while under-investing in the process and cultural changes that would make that tooling effective.

**False Confidence from Compliance**: Compliance certifications (SOC 2, ISO 27001, PCI-DSS) confirm that certain controls were in place at the point of audit — they do not assess whether the security program is improving, whether teams are using tools effectively, or whether the organization is resilient against threats that haven't yet been incorporated into regulatory requirements. Maturity assessment fills this gap.

**Inability to Track Progress**: Engineering and security teams work hard on security improvements, but without a measurement framework, it is nearly impossible to demonstrate progress to leadership in concrete terms. This erodes confidence in the security program and makes budget justification difficult.

**Repeating Failures**: Organizations that have experienced security incidents frequently find that the underlying cause was not a missing tool but a missing capability — lack of threat modeling practices, immature incident response procedures, or insufficient security awareness. Maturity assessment identifies these capability gaps before they become incidents.

**Peer Benchmarking Vacuum**: Industry surveys provide aggregate statistics ("X% of organizations have adopted SAST"), but without a structured framework, it is impossible to know how your organization compares to peers at a meaningful level of granularity.

Structured maturity assessment addresses all of these problems by providing a systematic, repeatable, and evidence-based method for understanding security capability — not just security configuration.

---

## How This Model Differs From and Complements Existing Frameworks

The TDMM occupies a deliberate position in the landscape of security frameworks. Understanding where it overlaps and where it diverges from existing models helps practitioners use it most effectively.

### Differences from OWASP SAMM

OWASP SAMM is primarily an **application security** model. Its strength is in characterizing the maturity of software development security practices — threat modeling, code review, security testing. The TDMM extends this scope in two critical directions: it explicitly covers **infrastructure security** and **CI/CD pipeline security** with the depth required for cloud-native environments, and it treats **DevSecOps culture and organizational structure** as a first-class domain rather than a subcomponent of governance.

The TDMM also adopts a flatter level structure (5 levels vs SAMM's stream-based 3-level approach per practice) to enable cleaner aggregation into an overall maturity score.

### Differences from BSIMM

BSIMM is **observational and descriptive** — it tells you what mature organizations do. The TDMM is **prescriptive and actionable** — it tells you what to do and in what sequence. These are complementary lenses: BSIMM is excellent for benchmarking ("are our practices consistent with what mature organizations do?"), while the TDMM is better suited for roadmapping ("what should we do next?").

### Differences from CMMI

CMMI is **process-general**: it can be applied to any organizational process capability. The TDMM is **security-specific**: its domain criteria, assessment questions, and level characteristics are tailored to DevSecOps. CMMI's rigor and mathematical foundation inspired the TDMM's scoring model, but practitioners should not attempt to apply CMMI assessment methodology directly to DevSecOps maturity measurement.

### How These Frameworks Work Together

A mature security program uses all of these frameworks in concert. A recommended combination:

- Use **OWASP SAMM** for detailed application security practice assessment and roadmapping
- Use **BSIMM** annually for benchmarking against peer organizations
- Use the **TDMM** for overall program maturity tracking, board reporting, and cross-domain investment prioritization
- Use **NIST CSF** for communicating with executive leadership and regulators
- Use **NIST SSDF** for supply chain and software development compliance requirements

---

## Target Audience

This document and the broader TDMM framework are designed for the following roles:

**CISOs and VP-level Security Leaders** use the model for strategic planning cycles, board presentations, security program investment justification, and regulatory reporting. They engage primarily with the Architecture, Implementation, and Roadmap documents.

**Security Architects** use the model for detailed domain-level gap analysis, toolchain selection and roadmapping, and program design. They engage with the full Framework document and the technical sections of the Implementation guide.

**DevSecOps Leads and Platform Security Engineers** conduct the actual assessments, gather tooling evidence, facilitate stakeholder interviews, and develop the detailed roadmap. They engage with the Implementation guide and questionnaire most intensively.

**Engineering Managers and Tech Leads** participate in assessments as subject matter experts for their teams and use the model to understand what security expectations apply at each stage of the development lifecycle.

**Compliance Officers and Auditors** use the model as evidence of a structured, improving security program — particularly relevant for SOC 2 Type II and ISO 27001 audits where the maturity and effectiveness of the ISMS are evaluated.

---

## How to Read and Use This Document

This introduction serves as the conceptual foundation for the entire TDMM framework. Readers are encouraged to approach the documentation in the following sequence:

1. **This document (Introduction)**: Establish conceptual grounding — why maturity models exist, how this one was constructed, and what it is designed to accomplish.

2. **Architecture (docs/architecture.md)**: Understand the structural mechanics of the model — the eight domains, five levels, scoring methodology, and assessment approach. This is the "operating manual" for the model.

3. **Framework (docs/framework.md)**: Study the detailed characteristics of each level across each domain. This is the substantive content of the model — the definitive reference for what each maturity level means.

4. **Implementation (docs/implementation.md)**: Learn how to conduct a maturity assessment using the structured questionnaire and scoring methodology. This is the practitioner's guide.

5. **Best Practices (docs/best-practices.md)**: Review guidance on running effective assessments, interpreting results, and communicating them to stakeholders.

6. **Roadmap (docs/roadmap.md)**: Use the transition guides and timeline templates to build a concrete improvement plan.

For organizations conducting their first assessment, we recommend allocating 4-6 weeks for a thorough assessment process — including stakeholder interviews, tooling evidence collection, and scoring — before moving to roadmap development. The quality of the assessment directly determines the quality of the resulting roadmap, and shortcuts in the assessment phase routinely produce misdirected investment.

For organizations using the TDMM as an ongoing measurement tool, annual full assessments complemented by quarterly domain-level check-ins are recommended. See docs/best-practices.md for detailed guidance on assessment cadence.

---

## Quick-Start Assessment Guide

For practitioners who need to produce a rapid maturity estimate before committing to a full assessment, this section provides a structured self-assessment process that can be completed in 2–4 hours. The quick-start produces an approximate domain-level score (accurate to ±0.5 level) sufficient for initial gap identification and investment prioritization.

### Step 1: Assemble Your Assessment Team (30 minutes)

Identify the right people to answer assessment questions across each domain. A quick-start assessment works best with 2–3 individuals who span security, engineering, and platform perspectives. A single individual conducting a self-assessment will have blind spots; at minimum, pair a security team member with a senior engineer or DevOps lead.

**Recommended participants**:
- Security architect or DevSecOps lead (primary assessor)
- Senior platform or DevOps engineer (engineering perspective)
- One engineering team lead from the primary product team (developer perspective)

### Step 2: Level-Setting Review (20 minutes)

Before beginning scoring, all participants should read the Five Maturity Levels summary from `docs/architecture.md`. Agree on a shared understanding of what Level 2 vs. Level 3 means — the most common source of scoring inconsistency is different mental models of the level boundaries.

A useful calibration exercise: before assessing your own organization, apply the five-level descriptions to an organization you know well that is clearly at one level. If you can agree on that calibration case, your assessments of your own organization will be more consistent.

### Step 3: Domain-by-Domain Quick Scoring (60–90 minutes)

For each of the eight domains, answer the following diagnostic questions. The highest level at which you can answer "Yes" to all questions is your approximate domain score.

**Domain 1: Culture & Organization**

| Level | Gate Question |
|---|---|
| Level 2 | Is there at least one person in the engineering organization who has dedicated security responsibility and is consulted on security decisions? |
| Level 3 | Does every engineering team have a designated security champion who receives regular security training and actively participates in security activities? |
| Level 4 | Are security KPIs (e.g., vulnerability backlog, time-to-remediate) tracked at the team level and reviewed by engineering leadership? |
| Level 5 | Does the organization contribute to industry security standards, open source security projects, or publish original security research? |

**Domain 2: Security Requirements**

| Level | Gate Question |
|---|---|
| Level 2 | Are security requirements documented for business-critical features before development begins? |
| Level 3 | Is STRIDE or equivalent threat modeling performed for all significant architectural changes, and are identified threats tracked to resolution? |
| Level 4 | Are threat models maintained as living documents, updated when the system architecture or threat landscape changes? |
| Level 5 | Is threat modeling partially automated (e.g., ML-assisted threat identification) or integrated into design tools? |

**Domain 3: Secure Development**

| Level | Gate Question |
|---|---|
| Level 2 | Is SAST tooling deployed and running on at least some code repositories? |
| Level 3 | Does SAST run on every pull request with break-build enforcement for Critical findings, across all production code repositories? |
| Level 4 | Is vulnerability density (findings per KLOC or per PR) tracked per team and used to drive investment decisions? |
| Level 5 | Is security fix suggestion or automated remediation assistance deployed (e.g., AI-assisted fix proposals for SAST findings)? |

**Domain 4: CI/CD Security**

| Level | Gate Question |
|---|---|
| Level 2 | Is secret scanning deployed in at least some CI/CD pipelines? |
| Level 3 | Are pipeline credentials managed through a secrets management solution (no hardcoded secrets), and is artifact signing implemented for production artifacts? |
| Level 4 | Are SBOM and provenance attestations generated for all production artifacts, and is supply chain integrity verified at deployment? |
| Level 5 | Is the build system itself assessed against SLSA Level 3+ requirements, with provenance attestations verifiable by external consumers? |

**Domain 5: Testing & Validation**

| Level | Gate Question |
|---|---|
| Level 2 | Is DAST scanning performed at least quarterly against production or staging environments? |
| Level 3 | Is DAST integrated into the staging environment pipeline and run on every deployment before production promotion? |
| Level 4 | Is continuous DAST running against production with active monitoring and alerting on new findings? |
| Level 5 | Are adversarial simulation exercises (red team) conducted quarterly with findings directly feeding tool and process improvements? |

**Domain 6: Infrastructure Security**

| Level | Gate Question |
|---|---|
| Level 2 | Is IaC scanning deployed and running in at least some CI/CD pipelines? |
| Level 3 | Is IaC scanning a mandatory break-build gate in all production infrastructure pipelines, and are Kubernetes Pod Security Standards enforced? |
| Level 4 | Is continuous infrastructure drift detection deployed and alerting on unauthorized changes within minutes? |
| Level 5 | Is automated misconfiguration remediation deployed for a defined category of low-risk findings, executing without human intervention? |

**Domain 7: Operations & Monitoring**

| Level | Gate Question |
|---|---|
| Level 2 | Are security event logs (cloud audit logs, application logs) centrally collected and searchable? |
| Level 3 | Is a SIEM deployed with tuned detection rules for the top threat scenarios applicable to this environment? |
| Level 4 | Are MTTD and MTTR tracked as KPIs and reviewed monthly? Is threat intelligence actively consumed and operationalized? |
| Level 5 | Is threat hunting conducted proactively (not just reactive alert response), and does the organization share threat intelligence with peer organizations? |

**Domain 8: Governance & Compliance**

| Level | Gate Question |
|---|---|
| Level 2 | Are core security policies documented and accessible to all relevant staff? |
| Level 3 | Is a risk register maintained, compliance controls mapped to technical controls, and an exception process defined and enforced? |
| Level 4 | Is quantitative risk modeling (e.g., FAIR) used to inform security investment decisions, and is compliance posture continuously monitored? |
| Level 5 | Is security policy generation or review partially automated based on risk data, and is the organization's compliance posture predictively modeled? |

### Step 4: Calculate and Interpret Your Score (20 minutes)

Assign a numeric score to each domain based on the highest gate question answered "Yes" for all questions at that level. Use the weighting table from `docs/architecture.md` to calculate a weighted overall score.

```
Quick Scoring Example:
  Culture & Org:           L2 → 2.0 × 10% = 0.20
  Security Requirements:   L2 → 2.0 × 12% = 0.24
  Secure Development:      L3 → 3.0 × 15% = 0.45
  CI/CD Security:          L2 → 2.5 × 15% = 0.38
  Testing & Validation:    L2 → 2.0 × 12% = 0.24
  Infrastructure Security: L3 → 3.0 × 14% = 0.42
  Ops & Monitoring:        L2 → 2.0 × 12% = 0.24
  Governance & Compliance: L2 → 2.0 × 10% = 0.20
                                            ------
  Overall Score:                             2.37
```

**Interpreting the quick-start score**:
- The score is accurate to approximately ±0.5 maturity level
- Domain scores below 2.0 identify the highest-priority investment areas
- Any domain scoring ≥1.0 below the organization's average is a candidate for focused short-term investment

### Step 5: Prioritize Improvement Targets (20 minutes)

From your domain scores, identify:

1. **The lowest-scoring domain**: This is typically the most impactful area for near-term investment, as foundational gaps in lower domains limit the effectiveness of controls in higher domains.
2. **The domain most misaligned with organizational risk**: If your organization runs public APIs at scale, Testing & Validation maturity is more consequential than for an internal-only application.
3. **The domain with the highest achievable improvement**: Sometimes a domain scoring at Level 2 is one concrete initiative away from Level 3, making it a high-ROI improvement target.

Bring your domain scores and improvement priorities to the full TDMM assessment (using `docs/implementation.md`) to develop a detailed improvement roadmap with evidence collection.

---

## Common Assessment FAQ

**Q: Should we conduct the assessment internally or use an external assessor?**

Both approaches are valid. Internal assessments are faster and cheaper, and the team's existing context is an advantage. External assessments provide independence and a benchmark perspective from other organizations the assessor has worked with. For a first assessment, internal is often more practical. For assessments used in board reporting or customer trust contexts, external validation adds credibility. Many organizations do an internal assessment to calibrate expectations before commissioning an external validation.

**Q: How long does a full TDMM assessment take?**

A thorough full assessment — including stakeholder interviews, tooling evidence collection, and scoring — typically requires 4–6 weeks of elapsed time for a medium-sized organization (50–500 engineers). The effort from the security team is typically 2–4 person-weeks. Larger organizations may take 8–12 weeks for enterprise-wide coverage. The quick-start guide above produces a ±0.5 accuracy estimate in 2–4 hours.

**Q: How often should we reassess?**

Annual full assessments are the standard recommendation. Quarterly domain-level check-ins (using the gate questions above for the 2–3 domains being actively improved) provide more frequent progress tracking without the overhead of a full assessment. Annual reassessments produce score deltas that demonstrate program progress, which are valuable for board reporting and budget justification.

**Q: How do we use the maturity score in stakeholder reporting?**

Present the domain profile (radar chart) alongside the overall score to give leadership a complete picture. Context matters: a score of 2.5 at an organization that was at 1.5 twelve months ago is an excellent story. A score of 2.5 at an organization that has been investing in DevSecOps for three years and expected to be at 3.5 requires explanation. Always present scores with a trend line (historical context) and a forward projection (where will we be in 12 months and what will it take to get there).

**Q: What if different teams in our organization are at very different maturity levels?**

This is common — and it is the right situation to surface. Score each major team or product area separately and present the distribution alongside the organizational average. The distribution reveals whether inconsistency is the primary risk (a 2.8 average could be five teams at 2.8 or three teams at 1.5 and two teams at 4.0). Inconsistency-driven programs have a different remediation strategy than uniformly-low programs.

**Q: Can we use the TDMM to compare ourselves to industry peers?**

The TDMM provides a consistent scoring methodology that enables comparisons if other organizations use the same model. For cross-organizational benchmarking, BSIMM (Building Security In Maturity Model) provides the most robust industry benchmark data due to its large participant base. Use TDMM for internal roadmapping and progress tracking; use BSIMM for peer benchmarking. The two frameworks are complementary rather than competitive.
