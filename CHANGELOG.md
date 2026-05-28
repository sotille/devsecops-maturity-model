# Changelog

All notable changes to the DevSecOps Maturity Model are documented here.
Format: `[version] — [date] — [summary of changes]`

---

## [Unreleased]

- [2026-04-07] README.md: Added Book 5 cross-reference to Learning Resources — links to Ch 18 (AI Security Maturity) and ai-devsecops-framework/docs/maturity-model.md for AI-specific assessments
- [2026-04-07] README.md: Updated Book Series Overview link text to reference all five Techstream volumes
- Added CHANGELOG.md (this file) for version tracking
- Added "Learning Resources" section to README.md linking to Book 1, techstream-learn labs, and techstream.app
- [2026-04-07] Added Anti-Gaming Controls Quick Reference section to assessment-scorecard.md — includes red-flag detection table and link to metrics-gaming-prevention.md; updated Related Documents with direct link to gaming prevention guide
- [2026-04-07] docs/implementation.md: Added Domain 9 — Automation Capability Assessment with 6 assessment questions covering scan coverage, false positive rate maturity, mean time to detection for CVEs, finding triage automation, tooling observability, and tooling update cadence; includes 5-level scoring rubric for each question and composite score interpretation table
- [2026-04-08] Created docs/maturity-progression-tracking.md — operational model for running repeated TDMM assessments and tracking improvement: assessment cadence (initial baseline, quarterly spot assessments, semi-annual full assessments), progression metrics (domain score calculation with fractional levels, aggregate TDMM score, velocity per assessment period, dispersion index), tracking dashboard structure (assessment history table, domain progression chart, velocity heatmap), stagnation identification (technical, organizational, resource, measurement types) with intervention framework, quarterly leadership brief template, annual board summary guidance, integration of progression data with compliance posture, incident response effectiveness, AI security readiness, and DORA metrics


---

## [1.0.0] — 2026-05-17

### Added — Governance and Documentation

- `SECURITY.md` — security reporting policy and supported versions
- `CITATION.cff` — academic and industry citation metadata (CFF v1.2.0)
- `CODE_OF_CONDUCT.md` — Contributor Covenant v2.1
- `README.md` "Related Publications" section linking the TechStream article series

### Federal-standards alignment (this release)

- Continued alignment with Executive Order 14028 (Improving the Nation's Cybersecurity)
- Continued alignment with Executive Order 14306 (June 2025)
- Continued alignment with NIST SP 800-218 (SSDF) v1.1
- Acknowledgment of NIST SP 1800-44 (NCCoE DevSecOps Practices) preliminary draft, March 2026

### Related publications referenced in this release

  - "The 4-Phase DevSecOps Transformation" (Medium, April 2026)

### Changed

- Documentation cross-references updated to reflect the public TechStream framework portfolio at https://github.com/sotille

## [1.0.0] — 2024-01-15

- Initial public release of the Techstream DevSecOps Maturity Model (TDMM)
- Core framework documentation: introduction, architecture, framework, implementation, best-practices, roadmap
- 8-domain, 5-level maturity assessment model (TDMM v1.0)
- Assessment scorecard with quantitative scoring methodology
- Remediation playbooks for each maturity domain
- Metrics and KPIs framework for tracking DevSecOps progress
- Metrics gaming prevention guidance for organizations measuring maturity
- Scaling guidance for enterprise-wide TDMM adoption
- Framework navigation guide for selecting the right starting point
- Apache 2.0 license and contribution guidelines
