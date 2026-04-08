<p align="center">
  <a href="https://techstream.app">
    <img src="https://techstream.app/images/techstream-icon.svg" width="72" height="72" alt="TechStream" />
  </a>
</p>

# DevSecOps Maturity Model

A structured, five-level maturity framework for assessing, benchmarking, and advancing DevSecOps practices across software engineering organizations. This model provides CISOs, security architects, and DevSecOps leads with a rigorous, evidence-based methodology for evaluating security integration across the full software development lifecycle.

---

## Description

The Techstream DevSecOps Maturity Model (TDMM) defines a comprehensive assessment framework spanning eight security domains and five maturity levels. It draws inspiration from industry-proven models including CMMI, OWASP SAMM, and BSIMM, while extending them to address the unique demands of modern cloud-native, microservices, and continuous delivery environments.

Organizations use this model to:

- Establish a baseline of current DevSecOps capability
- Identify gaps and prioritize security investments
- Build structured roadmaps for security program advancement
- Benchmark their posture against industry peers
- Demonstrate progress to boards, regulators, and auditors

---

## Purpose

Traditional security assessments produce point-in-time snapshots that quickly become stale. DevSecOps maturity assessment, by contrast, evaluates the _processes_, _culture_, _tooling_, and _metrics_ that produce security outcomes continuously. This model shifts the focus from compliance checklists to organizational capability, giving security and engineering leaders a durable foundation for continuous improvement.

The TDMM is designed to:

1. Provide a common language between security, engineering, and business leadership
2. Make security capability measurable and trackable over time
3. Connect security investment decisions to quantifiable risk reduction
4. Support regulatory and compliance reporting by demonstrating program maturity
5. Enable peer benchmarking within and across industry verticals

---

## Audience

| Role | How They Use This Model |
|------|------------------------|
| **Chief Information Security Officer (CISO)** | Strategic planning, board reporting, investment prioritization |
| **Security Architects** | Domain-level gap analysis, toolchain roadmapping |
| **DevSecOps Leads** | Team-level assessments, pipeline security reviews |
| **Platform / SRE Leads** | Infrastructure security, operations maturity scoring |
| **Compliance Officers** | Evidence of program maturity for auditors and regulators |
| **Engineering Managers** | Understanding security expectations at each development stage |
| **Risk Officers** | Quantitative risk posture and exposure assessment |

---

## Table of Contents

- [Introduction](docs/introduction.md) - Purpose of maturity models, reference frameworks, and how to use this document
- [Architecture](docs/architecture.md) - Model structure, domain matrix, scoring methodology, and assessment approach
- [Framework](docs/framework.md) - Full five-level, eight-domain maturity framework with detailed characteristics
- [Implementation](docs/implementation.md) - Assessment methodology, questionnaire, scoring, and roadmap building
- [Remediation Playbooks](docs/remediation-playbooks.md) - Actionable advancement guidance for each domain: exact steps, owners, effort estimates, and evidence requirements to advance between levels
- [Best Practices](docs/best-practices.md) - Running effective assessments, avoiding common pitfalls, communicating results
- [Roadmap](docs/roadmap.md) - Level transition guides, investment requirements, and transformation timelines
- [Assessment Scorecard](docs/assessment-scorecard.md) - Standalone workshop scorecard: 45 scored practice statements across all 8 domains, radar chart template, and interpretation guide
- [Metrics Gaming Prevention](docs/metrics-gaming-prevention.md) - Identifying and preventing metrics gaming across all domains: gaming patterns, structural controls, anomaly detection, and metrics design principles that resist gaming

---

## How to Use This Model

### Step 1 - Read the Introduction and Architecture

Start with docs/introduction.md to understand the model foundation and relationship to CMMI, OWASP SAMM, and BSIMM. Then review docs/architecture.md to understand the eight-domain, five-level matrix and how scoring works.

### Step 2 - Conduct the Assessment

Use the questionnaire and methodology in docs/implementation.md to perform a structured assessment. Gather evidence from tooling, interviews, metrics dashboards, and pipeline configurations. Score each domain independently before calculating the aggregate.

### Step 3 - Interpret Results Against the Framework

Map your scores to the characteristics described in docs/framework.md. This will reveal not just where you are, but what specific practices define your current level and what is required to advance.

### Step 4 - Build a Roadmap

Use docs/roadmap.md to construct a realistic, time-bounded roadmap for maturity advancement. Reference the prioritization framework in docs/implementation.md to sequence investments based on risk reduction and organizational readiness.

### Step 5 - Track Progress Continuously

Review docs/best-practices.md for guidance on establishing assessment cadence, selecting leading and lagging indicators, and communicating progress to leadership.

---

## The Eight Domains

| # | Domain | Focus Area |
|---|--------|-----------|
| 1 | Culture & Organization | Shared responsibility, security champions, training |
| 2 | Security Requirements | Threat modeling, abuse cases, security user stories |
| 3 | Secure Development | Secure coding standards, SAST, peer review |
| 4 | CI/CD Security | Pipeline hardening, secrets management, supply chain |
| 5 | Testing & Validation | DAST, IAST, penetration testing, red teaming |
| 6 | Infrastructure Security | IaC scanning, cloud configuration, hardening |
| 7 | Operations & Monitoring | SIEM, anomaly detection, incident response |
| 8 | Governance & Compliance | Policy management, audit evidence, risk governance |

---

## The Five Maturity Levels

| Level | Name | Summary |
|-------|------|---------|
| 1 | Initial (Ad Hoc) | Security is reactive and unstructured |
| 2 | Managed (Repeatable) | Basic practices formalized in some teams |
| 3 | Defined (Standardized) | Security integrated consistently across the SDLC |
| 4 | Quantitatively Managed (Measured) | Security driven by metrics and risk quantification |
| 5 | Optimizing (Continuous Improvement) | Industry-leading, self-improving security program |

---

## Learning Resources

The Techstream Book Series and hands-on lab companion extend the concepts in this framework with structured learning, maturity assessment exercises, and roadmap-building guidance.

- **[Book 1: DevSecOps — Foundations & Transformation](https://www.techstream.app/learn)** — The primary book volume aligned with this framework. Part II covers TDMM in depth: the 8 domains, 5 maturity levels, 2-hour quick-start assessment, and board-level reporting.
- **[Hands-On Labs (techstream-learn/book-1-foundations/)](https://www.techstream.app/learn)** — Practical exercises including running a TDMM self-assessment, building a transformation roadmap from assessment results, and designing a security champion program.
- **[Book 5: AI and Agentic Systems Security (Ch 18 — AI Security Maturity)](https://www.techstream.app/learn)** — Chapter 18 extends the TDMM maturity model to AI and agentic system security, defining a five-level AI Security Maturity scale. Use alongside the [ai-devsecops-framework maturity model](../ai-devsecops-framework/docs/maturity-model.md) for AI-specific assessments.
- **[Book Series Overview (VOLUMES.md)](../techstream-books/VOLUMES.md)** — Index of all five Techstream volumes covering DevSecOps foundations, CI/CD security, cloud security, release governance, and AI and agentic systems security.
- **[Techstream Platform](https://www.techstream.app)** — The central portal for all Techstream frameworks, documentation, and learning resources.

---

## Contributing

Contributions are welcome from security practitioners, architects, and researchers. To contribute:

1. Fork this repository and create a feature branch
2. Document the rationale for any changes to the maturity model structure, level definitions, or domain criteria
3. Ensure all contributions include evidence-based references (industry research, standards, or production experience)
4. Submit a pull request with a clear description of the change and its impact on the model

All additions are reviewed by the core Techstream security team before merging.

---

## License

Copyright 2024 Techstream

Licensed under the Apache License, Version 2.0. See LICENSE for the full license text.

---

*Techstream DevSecOps Maturity Model - Enabling measurable, continuous security advancement.*
