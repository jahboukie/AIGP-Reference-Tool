# Engagement Scenario — Week-by-Week Walkthrough

> **Purpose**: Step-by-step guide for running the Meridian Assurance simulation through your GRC Command Centre. Follow this sequence to build a complete, portfolio-ready governance artefact set.

---

## Phase 0: Engagement Setup (Day 1)

### In GRC Command Centre:

**Create Engagement:**
- Name: Meridian Assurance — AURA Conformity Assessment
- Client: Meridian Assurance Corporation
- Industry: Life Insurance & Financial Services
- Jurisdiction: Canada + EU (Germany, France, Netherlands, Ireland)
- Role: External AI Governance Consultant
- Start Date: April 1, 2026
- End Date: September 30, 2026

**Register AI System:**
- Name: AURA — Automated Underwriting Risk Assessor
- Version: 2.4.1
- System ID: MRDN-AI-001
- EU AI Act Classification: High-Risk (Annex III, Area 5(b))
- Purpose: Automated life insurance underwriting — risk scoring, premium recommendation, accept/refer/decline
- Provider: Meridian AI Labs (in-house)
- Deployer: Meridian Assurance Europe GmbH
- Status: Production (Canada), Pre-deployment (EU)

**Select Applicable Frameworks:**
- EU AI Act (High-Risk Requirements) — primary
- ISO/IEC 42001:2023 — certification target
- NIST AI RMF 1.0 — OSFI alignment
- ISO/IEC 23894:2023 — supplementary risk guidance

---

## Phase 1: Discovery & Classification (Weeks 1-4)

### Week 1: Inventory & Classification

**Activities:**
- Confirm AURA's high-risk classification under Article 6(2) + Annex III
- Identify Meridian AI Labs as the "provider" under Article 3(3)
- Identify Meridian Europe GmbH as the "deployer" under Article 3(4)
- Document the supply chain (third-party data providers, open-source libraries, cloud infrastructure)

**Assess these requirements (mark status in GRC tool):**
- EU AI Act Art. 6 — Classification as high-risk ✓ (Met — clear Annex III match)
- EU AI Act Art. 16 — Provider obligations (Partial — not formally documented)
- EU AI Act Art. 26 — Deployer obligations (Gap — EU entity not yet operationally ready)
- ISO 42001 Clause 4.1 — Understanding the organization and its context (Partial)
- ISO 42001 Clause 4.2 — Understanding the needs and expectations of interested parties (Gap)
- NIST GOVERN 1.1 — Legal and regulatory requirements identified (Partial)

**Upload Evidence:**
- Corporation dossier (this file set) as baseline evidence
- Meridian org chart showing AI governance reporting lines
- AURA system architecture diagram

### Week 2: Data Governance Assessment

**Activities:**
- Audit training data composition, sources, and quality
- Identify data gaps for EU deployment
- Assess GDPR compliance of data handling practices
- Review synthetic data generation methodology

**Assess these requirements:**
- EU AI Act Art. 10(1) — Data governance measures (Partial)
- EU AI Act Art. 10(2)(a)-(f) — Design choices, collection, preparation, bias examination (multiple gaps)
- EU AI Act Art. 10(3) — Representative, relevant, free of errors (Gap — EU representativeness)
- ISO 42001 A.4 — Data for AI systems (Partial)
- NIST MAP 2.1 — Determine data requirements (Partial)
- NIST MAP 2.3 — Scientific integrity of AI system assessed (Gap)

**Register Risks:**
- Risk 2 (Training Data EU gap) — Likelihood: Almost Certain, Impact: Major → Risk Score: Critical
- Risk 6 (Data Residency) — Likelihood: Likely, Impact: Moderate → Risk Score: High

**Upload Evidence:**
- Training data profile (from technical documentation)
- Data source agreements (draft table showing MIB, TELUS Health, Equifax, Munich Re)

### Weeks 3-4: Fundamental Rights Impact Assessment

**Activities:**
- Identify affected groups (insurance applicants — natural persons)
- Assess impact on fundamental rights (non-discrimination, privacy, access to services)
- Document mitigation measures for each identified impact
- Complete FRIA workflow in GRC tool

**FRIA Content:**

| Affected Group | Right Impacted | Severity | Mitigation |
|---------------|---------------|:--------:|-----------|
| All applicants | Right to non-discrimination (EU Charter Art. 21) | High | Fairness monitoring, bias audit, remediation of postal code proxy |
| Applicants aged 60-70 | Age discrimination | High | Recalibrate age-band thresholds, investigate feature interactions |
| Low-income postal code residents | Indirect socioeconomic discrimination | High | Remove or de-weight postal code feature, test alternative geographic risk measures |
| Applicants with complex medical histories | Right to explanation (Art. 86) | Medium | Improve explanation quality for multi-condition cases |
| All declined applicants | Access to essential services | High | Mandatory human review of all declines, clear appeal mechanism |
| Data subjects (training data) | Privacy (GDPR Art. 5, 6) | Medium | DPIA for training data, consent/legitimate interest analysis |

**Assess these requirements:**
- EU AI Act Art. 27 — FRIA (Gap → In Progress as you complete the FRIA)
- EU AI Act Art. 9(2)(a) — Identification of risks to fundamental rights (Gap)
- NIST MAP 1.1 — Mapping AI system purpose and context (Partial)
- NIST MAP 1.5 — Stakeholders identified (Gap)

---

## Phase 2: Technical Assessment (Weeks 5-10)

### Weeks 5-6: Risk Management System Review

**Activities:**
- Review Meridian's existing risk management framework (OSFI E-23 based)
- Map existing controls against EU AI Act Article 9 requirements
- Identify gaps between Canadian and EU risk management expectations
- Assess whether reasonably foreseeable misuse has been considered

**Assess these requirements:**
- EU AI Act Art. 9(1) — Risk management system established (Partial)
- EU AI Act Art. 9(2)(a) — Known and foreseeable risks identified (Partial)
- EU AI Act Art. 9(2)(b) — Risks estimated and evaluated (Gap — no EU-specific risk estimation)
- EU AI Act Art. 9(2)(c) — Post-market monitoring data evaluated (Gap — no EU baseline)
- EU AI Act Art. 9(4) — Testing for appropriate levels of performance (Partial)
- ISO 42001 Clause 6.1 — Actions to address AI risks (Partial)
- ISO 42001 A.3 — AI risk management (Partial)
- NIST GOVERN 1.2 — Risk management process established (Partial)
- NIST MEASURE 1.1 — Appropriate measurement approaches identified (Partial)

**Register Risks:**
- Risk 8 (No conformity assessment procedure) — Likelihood: Certain, Impact: Critical → Risk Score: Critical

### Weeks 7-8: Bias & Fairness Audit

**Activities:**
- Conduct independent review of fairness metrics
- Deep-dive into postal code proxy discrimination (Risk 1)
- Assess age-band fairness gap (demographic parity 0.87)
- Review equalized odds for ethnicity proxy (0.82)
- Evaluate synthetic data impact on fairness metrics
- Document findings and remediation recommendations

**Key Findings to Document:**

| Finding | Severity | Recommendation |
|---------|:--------:|---------------|
| Postal code correlates with ethnicity at r=0.67 in Toronto FSAs | Critical | Remove postal code from direct features; aggregate to provincial/state level only |
| Age 60-70 refer rate 23% higher than actuarial justification | High | Retrain with age-band calibration constraints; add age-fairness regularization |
| Equalized odds (ethnicity proxy) at 0.82 — below 0.85 threshold | High | Feature audit to identify proxy pathways; consider fairness-constrained optimization |
| CTGAN synthetic data shows 12% distribution drift from real data in tail demographics | Medium | Validate synthetic data with domain experts; consider removing if quality insufficient |

**Assess these requirements:**
- EU AI Act Art. 10(2)(f) — Examination for possible biases (Gap → assessed, remediation needed)
- EU AI Act Art. 9(5)(b) — Elimination or reduction of risks (Gap)
- ISO 42001 A.5 — AI system impact assessment (Partial)
- NIST MEASURE 2.6 — AI system performance evaluated for bias (Partial)
- NIST MEASURE 2.11 — Fairness assessed (Gap)

### Weeks 9-10: Transparency, Explainability & Human Oversight

**Activities:**
- Evaluate SHAP explanation quality against Article 13 requirements
- Assess whether explanations are meaningful to deployers (underwriters) and affected persons (applicants)
- Review human oversight design against Article 14
- Evaluate auto-accept sampling rate adequacy

**Assess these requirements:**
- EU AI Act Art. 13(1) — Sufficiently transparent (Partial)
- EU AI Act Art. 13(3)(b)(iv) — Human oversight measures described (Gap)
- EU AI Act Art. 14(1) — Designed for effective human oversight (Partial — auto-accept gap)
- EU AI Act Art. 14(3)(a) — Understand capabilities and limitations (Partial)
- EU AI Act Art. 14(4)(a) — Able to properly interpret output (Partial — explanation quality)
- EU AI Act Art. 14(4)(c) — Able to override system (Met — override exists)
- ISO 42001 A.6 — AI system lifecycle (Partial)
- ISO 42001 A.8 — Operation of AI systems (human oversight) (Partial)
- NIST MEASURE 2.8 — Transparency approaches identified (Partial)

---

## Phase 3: Gap Remediation & Documentation (Weeks 11-18)

### Weeks 11-12: Technical Documentation & Logging

**Activities:**
- Complete Annex IV technical documentation review
- Assess logging adequacy against Article 12
- Design EU regulatory access format for logs
- Review cybersecurity and supply chain risks

**Assess these requirements:**
- EU AI Act Art. 11 — Technical documentation (In Progress — Annex IV doc exists, gaps identified)
- EU AI Act Art. 12(1) — Automatic logging (Partial — comprehensive but EU format missing)
- EU AI Act Art. 12(2) — Traceability of functioning (Partial)
- EU AI Act Art. 15(1) — Appropriate level of accuracy (Partial — EU validation needed)
- EU AI Act Art. 15(3) — Resilient as regards errors (Met — fallback to manual exists)
- EU AI Act Art. 15(4) — Cybersecurity measures (Partial — SBOM missing)
- ISO 42001 A.7 — Data for AI systems (Partial)
- ISO 42001 A.10 — Third-party relationships (Gap — no SBOM, Arize DPA gap)

**Register Risks:**
- Risk 7 (Supply Chain Documentation) — Likelihood: Likely, Impact: Moderate → Risk Score: High

### Weeks 13-16: Remediation Planning

**Activities:**
- Compile all gaps into a prioritized remediation plan
- Assign owners, target dates, and resource estimates
- Create remediation tasks in GRC tool

**Remediation Action Items (create as tasks):**

| # | Action | Owner | Priority | Target |
|:-:|--------|-------|:--------:|:------:|
| 1 | Complete EU population validation study (1,000+ applications) | Dr. Tanaka | Critical | Month 4 |
| 2 | Remove postal code as direct feature; implement geographic risk debiasing | AI Labs | Critical | Month 4 |
| 3 | Retrain AURA with age-fairness constraints | AI Labs | High | Month 5 |
| 4 | Increase auto-accept human review sampling to 15% | Okoro | High | Month 3 |
| 5 | Develop consumer-facing explanation templates | Okoro + AI Labs | High | Month 4 |
| 6 | Complete DPIA for EU training data | Dr. Weber | High | Month 3 |
| 7 | Implement EU regulatory log export format | AI Labs | Medium | Month 5 |
| 8 | Create Software Bill of Materials (SBOM) | CTO office | Medium | Month 4 |
| 9 | Execute Arize AI Data Processing Agreement for inference data | Johal | Medium | Month 3 |
| 10 | Establish EU monitoring baseline distributions | AI Labs | High | Month 5 |
| 11 | Document GDPR Article 6 lawful basis analysis for training data | Dr. Weber | High | Month 3 |
| 12 | Designate AI Act compliance officer in EU entity | Schäfer | Critical | Month 2 |
| 13 | Draft AI system instructions for use (Art. 13 deployer package) | Your deliverable | High | Month 5 |
| 14 | Implement QMS for AI lifecycle (ISO 42001 foundation) | Johal + CTO | High | Month 5-6 |
| 15 | Conduct adversarial robustness testing for EU deployment | AI Labs | Medium | Month 5 |

### Weeks 17-18: Cross-Framework Analysis & Final Reports

**Activities:**
- Complete cross-framework compliance matrix
- Identify work that transfers across frameworks (EU AI Act evidence → ISO 42001 evidence → NIST)
- Generate ISO 42001 gap analysis and certification readiness report
- Create NIST AI RMF profile for Meridian

**Cross-reference examples to highlight:**
- EU AI Act Art. 9 (risk management) → ISO 42001 A.3 → NIST GOVERN 1.2
- EU AI Act Art. 10 (data governance) → ISO 42001 A.4 → NIST MAP 2.1
- EU AI Act Art. 13 (transparency) → ISO 42001 A.6 → NIST MEASURE 2.8
- EU AI Act Art. 14 (human oversight) → ISO 42001 A.8 → NIST MANAGE 1.3
- EU AI Act Art. 15 (cybersecurity) → ISO 42001 A.10 → NIST MANAGE 2.4

**Generate Reports in GRC Tool:**
1. **Compliance Report**: Full assessment status across all applicable requirements
2. **Gap Analysis Report**: All items marked "Gap" or "Partial" with remediation plan
3. **Risk Report**: Risk matrix with all 8+ risks, inherent vs residual scoring
4. **Executive Summary**: Board-ready overview for Meridian's CEO and board

---

## Phase 4: Portfolio Presentation (Post-Simulation)

Once you've completed the full simulation cycle, you will have:

| Artefact | Source | Interview Value |
|----------|--------|----------------|
| Complete engagement record with immutable audit trail | GRC Command Centre | Shows systematic, auditable process |
| 241 requirement assessments across 4 frameworks | Requirement Navigator | Shows framework depth |
| 8+ risks scored and tracked on risk matrix | Risk Matrix | Shows risk management capability |
| 15 remediation tasks with priorities and dates | Task Management | Shows project management capability |
| Completed FRIA with affected groups and mitigations | FRIA Module | Shows fundamental rights awareness |
| Cross-framework compliance matrix | Cross-Reference Map | Shows ability to reduce duplicate compliance work |
| 3 generated reports (compliance, gap analysis, risk) | Report Generation | Shows deliverable quality |
| Evidence vault with model card, architecture, metrics | Evidence Vault | Shows technical documentation competence |

**The pitch**: "I built a custom governance tool, then ran a complete high-risk AI system conformity assessment through it — from classification through FRIA, bias audit, technical documentation, remediation planning, to cross-framework analysis. This is not theoretical. This is what your compliance workflow would look like with me running it."

---

## Realistic Complications (Optional — For Advanced Scenarios)

If you want to increase realism, introduce these mid-engagement curveballs:

1. **Week 6 — Production incident**: AURA auto-declines a cluster of 47 applicants from a specific Toronto postal code in one day (3× normal rate). The VP Underwriting escalates. You need to investigate, document, and determine if this triggers an Article 62 serious incident report.

2. **Week 10 — Board pressure**: The CEO wants to accelerate EU deployment to Q2 instead of Q3. The CRO asks you whether the conformity assessment can be fast-tracked. Document your response (it cannot — the EU data validation gap is real).

3. **Week 14 — Vendor notification**: Arize AI notifies Meridian that their SaaS platform is migrating to a new data center in Virginia. This changes the data residency picture for inference monitoring data. Assess the GDPR impact and update your risk register.

4. **Week 16 — Regulation update**: A new EU AI Act delegated act clarifies insurance-specific requirements under Annex III Area 5. You need to assess whether any additional requirements apply and update the compliance matrix.

These scenarios generate additional tasks, evidence, and audit trail entries — making your GRC tool demonstration richer and more realistic.
