# Contributing to the Techstream DevSecOps Maturity Model

Thank you for your interest in contributing. This repository defines the Techstream DevSecOps Maturity Model (TDMM) — a five-level, eight-domain maturity framework for assessing and improving DevSecOps programs. Contributions that improve assessment criteria, domain coverage, scoring methodology, and alignment with recognized frameworks (OWASP SAMM, BSIMM, NIST CSF) are welcome.

---

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [What We Welcome](#what-we-welcome)
- [What We Do Not Accept](#what-we-do-not-accept)
- [How to Contribute](#how-to-contribute)
- [Documentation Standards](#documentation-standards)
- [Domain and Level Stability Policy](#domain-and-level-stability-policy)
- [Review Process](#review-process)
- [License](#license)

---

## Code of Conduct

All contributors are expected to engage professionally and constructively. Contributions that are dismissive, personal, or unprofessional will not be reviewed.

---

## What We Welcome

- **Domain criteria updates** — as DevSecOps practices evolve (e.g., supply chain security becoming a standard domain, AI/ML security emerging as a new concern), updates to domain criteria at each maturity level are valuable.
- **Assessment questionnaire improvements** — additions, clarifications, or corrections to the assessment questionnaire that make it more accurate or easier to use in practice.
- **Scoring methodology refinements** — improvements to the scoring rubrics that make them more objective and reproducible.
- **Alignment with updated external frameworks** — as OWASP SAMM, BSIMM, NIST CSF, and NIST SSDF are updated, corresponding updates to the TDMM's mapping are important.
- **Transition guidance** — practical guidance on how organizations progress from one maturity level to the next in a specific domain.
- **Evidence catalog improvements** — additions to the evidence catalog that make it more useful for audit and compliance use cases.
- **New domain proposals** — if an emerging area of DevSecOps is not covered by the current eight domains, a well-reasoned proposal for a new domain (submitted as an issue first, before a PR) is welcome.

---

## What We Do Not Accept

- **Arbitrary changes to maturity level definitions** — the five-level structure and domain definitions are stable. Changes to level characteristics must be well-justified and grounded in observable industry practice.
- **Contributions that inflate maturity criteria** — the model must be calibrated against observable, achievable industry practice. Criteria that only the most advanced organizations in the world could meet should not be placed at Level 3.
- Vendor promotional content.
- Major structural changes without prior issue discussion.

---

## Domain and Level Stability Policy

The TDMM's eight domains and five-level structure are considered stable. Changes to these foundational elements require:

1. An issue opened for community discussion, with a minimum 30-day comment period.
2. Consensus from the core team before any pull request is accepted.
3. Simultaneous updates to all affected documents (framework.md, architecture.md, implementation.md, roadmap.md) to maintain internal consistency.

Assessment questionnaire content and scoring rubric details are less stable and can be updated through the normal pull request process.

---

## How to Contribute

### Reporting Issues

Use GitHub Issues to report: assessment criteria that are unclear or inconsistent, scoring rubric ambiguities, external framework mapping errors, or gaps in the evidence catalog.

### Submitting Pull Requests

1. Fork and branch from `main`.
2. For domain or level changes, open an issue first and wait for core team input before writing a PR.
3. Ensure any changes to framework.md are reflected consistently in architecture.md and implementation.md.
4. Open a pull request with a clear description, rationale, and references to any industry frameworks or data supporting the change.

---

## Documentation Standards

- Technical tone for practitioners conducting assessments (security architects, DevSecOps leads, compliance officers).
- Tables for maturity level characteristics — maintain consistent structure across all domain tables.
- Numbered lists for assessment questions and evidence items.
- Mermaid diagrams for maturity progression flows and domain relationship maps.

---

## Review Process

Pull requests are reviewed with particular attention to calibration against observable industry practice. Changes to maturity criteria require evidence that the criteria reflect achievable standards for organizations at that level. Initial responses within 5 business days.

---

## License

By contributing, you agree your contributions will be licensed under the [Apache License 2.0](LICENSE).
