# Simulated AI Governance Lab — Corporation Dossier

> **Purpose**: This is a fictional corporation designed as a realistic end-to-end test case for AI governance, risk, and compliance work. All entities, persons, systems, and data described herein are fabricated for training and demonstration purposes. Use this dossier to populate your GRC Command Centre, run a full conformity assessment simulation, and demonstrate professional-grade governance workflow in interviews or client presentations.

---

## Company Profile

| Field | Detail |
|-------|--------|
| **Legal Name** | Meridian Assurance Corporation |
| **Trading As** | Meridian Assurance · Meridian AI |
| **Incorporation** | Ontario, Canada (Federal incorporation under CBCA) |
| **Founded** | 2011 |
| **Headquarters** | 200 Bay Street, Suite 3400, Toronto, ON M5J 2J2 |
| **EU Office** | Kurfürstendamm 21, 10719 Berlin, Germany (opened 2024) |
| **Industry** | Life Insurance & Financial Services |
| **NAICS** | 524113 — Direct Life Insurance Carriers |
| **Employees** | ~2,200 (1,800 Canada, 400 EU) |
| **Annual Revenue** | CAD $890M (2025) |
| **Publicly Traded** | TSX: MRDN (fictional) |
| **Regulator (Canada)** | OSFI — Office of the Superintendent of Financial Institutions |
| **Regulator (EU)** | BaFin — Bundesanstalt für Finanzdienstleistungsaufsicht |
| **Data Protection** | PIPEDA (Canada), GDPR (EU), CCPA (select US operations) |

---

## Corporate Structure

```
Meridian Assurance Corporation (Toronto)
├── Meridian Life Canada — life, critical illness, disability
├── Meridian Wealth — segregated funds, annuities, GICs
├── Meridian AI Labs (Toronto) — internal AI R&D division
├── Meridian Assurance Europe GmbH (Berlin) — EU subsidiary
│   └── Licensed for life insurance in DE, FR, NL, IE
└── Meridian Digital Services Inc. — SaaS platform operations
```

---

## Key Personnel (Fictional)

| Role | Name | Relevance |
|------|------|-----------|
| **CEO** | Nadia Okonkwo | Former OSFI executive, driving EU expansion |
| **CTO** | Dr. Marcus Chen | PhD ML (University of Toronto), built Meridian AI Labs |
| **Chief Risk Officer** | Philippe Beaumont | 20 years insurance risk, leads enterprise risk function |
| **Chief Compliance Officer** | Anita Johal | CIPP/C, CIPM, oversees regulatory compliance across jurisdictions |
| **VP AI & Data Science** | Dr. Yuki Tanaka | Leads model development team (14 ML engineers, 6 data scientists) |
| **Head of Underwriting** | Daniel Okoro | 15 years underwriting, domain expert for AI system validation |
| **EU Operations Director** | Katrin Schäfer | Based in Berlin, manages EU regulatory relationships |
| **DPO (EU)** | Dr. Lukas Weber | GDPR Data Protection Officer for Meridian Europe GmbH |
| **External Auditor** | Henderson & Cole LLP | ISO 42001 certification body (proposed) |
| **External Legal Counsel** | Freshfields (EU AI Act) | Advising on conformity assessment |

---

## Business Context

Meridian Assurance is a mid-tier Canadian life insurer that has been operating profitably for 14 years in the Canadian market. In 2024, Meridian opened a European subsidiary in Berlin and obtained insurance licences in Germany, France, the Netherlands, and Ireland — targeting the European term life and critical illness markets.

To compete effectively against established European insurers and maintain underwriting margins, Meridian's board approved the deployment of an AI-powered underwriting decision engine ("**AURA**") across both Canadian and European operations.

**The problem**: AURA makes or substantially influences decisions about whether individuals can obtain life insurance and at what premium — a use case explicitly classified as **high-risk under the EU AI Act** (Annex III, Area 5(b): "AI systems intended to be used to evaluate the creditworthiness of natural persons or establish their credit score, with the exception of AI systems used for the purpose of detecting financial fraud" and by extension insurance risk assessment affecting access to essential services).

**The trigger**: Meridian must achieve EU AI Act conformity for AURA before deploying it in EU markets. Additionally, the board has directed management to pursue **ISO/IEC 42001 certification** for the AI management system governing AURA's lifecycle — both as a quality signal to EU regulators and as a competitive differentiator.

**Your engagement**: You have been retained as the external AI Governance Consultant to lead Meridian through:
1. EU AI Act high-risk conformity assessment for AURA
2. ISO/IEC 42001 AIMS certification readiness
3. NIST AI RMF alignment (requested by OSFI as best practice for Canadian operations)
4. Cross-framework gap analysis and remediation planning

---

## The AI System: AURA (Automated Underwriting Risk Assessor)

### System Identity

| Field | Detail |
|-------|--------|
| **System Name** | AURA — Automated Underwriting Risk Assessor |
| **Version** | 2.4.1 |
| **System ID** | MRDN-AI-001 |
| **Classification** | **High-Risk** (EU AI Act Article 6(2), Annex III Area 5(b)) |
| **Intended Purpose** | Automated assessment of life insurance applications — risk scoring, premium recommendation, and accept/refer/decline decision support |
| **Deployer** | Meridian Assurance Europe GmbH (EU) / Meridian Life Canada (CA) |
| **Provider** | Meridian AI Labs (in-house development) |
| **First Deployed** | January 2025 (Canada only) |
| **EU Deployment Target** | Q3 2026 |
| **Operational Status** | Production (Canada), Pre-deployment (EU) |

### What AURA Does

AURA processes life insurance applications and produces:
1. **Risk Score** (0–1000 scale): Quantified mortality/morbidity risk estimate
2. **Risk Class Assignment**: Preferred Plus, Preferred, Standard Plus, Standard, Substandard (rated), Decline
3. **Premium Recommendation**: Calculated premium based on risk class, coverage amount, and product type
4. **Decision**: Auto-accept (55% of applications), Refer-to-underwriter (35%), Auto-decline (10%)
5. **Explanation Report**: Human-readable rationale generated for every decision

### How AURA Works — Technical Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                    AURA System Architecture                      │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ┌──────────────┐   ┌──────────────┐   ┌──────────────────┐    │
│  │ Application   │   │ Medical Data │   │ External Data    │    │
│  │ Form Data     │   │ (MIB, Rx,   │   │ (Credit, MVR,   │    │
│  │               │   │  Lab Results)│   │  Public Records) │    │
│  └──────┬───────┘   └──────┬───────┘   └────────┬─────────┘    │
│         │                   │                     │              │
│         ▼                   ▼                     ▼              │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │              Data Ingestion & Validation Layer            │   │
│  │  • Schema validation  • Missing value imputation          │   │
│  │  • Data type coercion • PII pseudonymisation pipeline     │   │
│  └────────────────────────┬─────────────────────────────────┘   │
│                           │                                      │
│                           ▼                                      │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │              Feature Engineering Pipeline                 │   │
│  │  • 847 features extracted from raw inputs                 │   │
│  │  • Medical history encoding (ICD-10 → embeddings)         │   │
│  │  • Prescription risk mapping (drug classes → risk flags)  │   │
│  │  • Temporal feature construction (trend analysis)         │   │
│  │  • Geographic risk factors (postal code → risk zone)      │   │
│  └────────────────────────┬─────────────────────────────────┘   │
│                           │                                      │
│                           ▼                                      │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │              Core ML Model (Ensemble)                     │   │
│  │                                                           │   │
│  │  ┌──────────┐  ┌──────────┐  ┌────────────────────┐     │   │
│  │  │ XGBoost  │  │ LightGBM │  │ Neural Network     │     │   │
│  │  │ (tabular │  │ (tabular │  │ (medical history   │     │   │
│  │  │  features│  │  features│  │  sequences — LSTM) │     │   │
│  │  │  v3.2.1) │  │  v4.1.0) │  │  (PyTorch v2.2)   │     │   │
│  │  └────┬─────┘  └────┬─────┘  └──────┬─────────────┘     │   │
│  │       │              │                │                   │   │
│  │       ▼              ▼                ▼                   │   │
│  │  ┌────────────────────────────────────────────────────┐  │   │
│  │  │         Weighted Ensemble Aggregation               │  │   │
│  │  │  XGBoost: 0.40 · LightGBM: 0.35 · LSTM: 0.25     │  │   │
│  │  └──────────────────────┬─────────────────────────────┘  │   │
│  └─────────────────────────┬────────────────────────────────┘   │
│                            │                                     │
│                            ▼                                     │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │              Post-Processing & Decision Layer             │   │
│  │  • Risk score calibration (Platt scaling)                 │   │
│  │  • Business rules overlay (regulatory constraints)        │   │
│  │  • SHAP-based explanation generation                      │   │
│  │  • Decision: Accept / Refer / Decline                     │   │
│  │  • Confidence interval estimation                         │   │
│  └────────────────────────┬─────────────────────────────────┘   │
│                           │                                      │
│                           ▼                                      │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │              Human Oversight Interface                     │   │
│  │  • Underwriter dashboard (all Refer + sampled Accept)     │   │
│  │  • Override capability with mandatory reason logging      │   │
│  │  • Escalation workflow (decline → senior underwriter)     │   │
│  │  • Monthly model performance review panel                 │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Model Details

| Component | Specification |
|-----------|--------------|
| **Framework** | Python 3.11, scikit-learn 1.4, XGBoost 2.0, LightGBM 4.1, PyTorch 2.2 |
| **Model Type** | Weighted ensemble (2 gradient-boosted trees + 1 LSTM) |
| **Total Parameters** | XGBoost: ~12M leaf values, LightGBM: ~9M, LSTM: ~2.3M weights |
| **Feature Count** | 847 engineered features from 127 raw input fields |
| **Training Data** | 4.2 million historical Canadian underwriting decisions (2015–2024) |
| **Validation Split** | 70% train / 15% validation / 15% holdout test |
| **Training Compute** | 8× NVIDIA A100 GPUs, ~72 hours total training time |
| **Inference Latency** | p50: 340ms, p99: 1.2s per application |
| **Retraining Cadence** | Quarterly (with monthly monitoring checkpoints) |

### Training Data Profile

| Data Source | Records | Time Period | Jurisdiction |
|-------------|--------:|:----------:|:------------:|
| Meridian Life Canada underwriting decisions | 1.8M | 2015–2024 | Canada |
| Licensed historical data — Canadian Life Insurance Association | 1.6M | 2010–2023 | Canada |
| Licensed historical data — European reinsurer (Munich Re) | 0.6M | 2018–2024 | EU (DE, FR, NL) |
| Synthetic augmentation (for underrepresented demographics) | 0.2M | Generated 2024 | N/A |
| **Total** | **4.2M** | | |

**Known Data Issues:**
- Canadian data overrepresents Ontario/Quebec (68% of records) — underrepresentation of Maritime/Prairie provinces
- EU data sourced from reinsurer may not reflect direct-to-consumer application patterns
- Demographic representation: 62% male, 38% female. Age distribution skewed toward 35–55 (core market)
- Synthetic data generated using CTGAN — validated against real distributions but synthetic artefacts possible
- Historical data contains pre-2019 underwriting decisions that may reflect since-prohibited discriminatory practices (genetic information use)
- No ground-truth mortality outcomes for recent applications (right-censoring problem)

### Performance Metrics (Canadian Production — as of March 2026)

| Metric | Value | Target |
|--------|:-----:|:------:|
| Overall accuracy (vs senior underwriter panel) | 91.3% | ≥90% |
| Auto-accept accuracy | 94.7% | ≥93% |
| False decline rate | 2.1% | ≤3% |
| Demographic parity ratio (gender) | 0.94 | ≥0.90 |
| Demographic parity ratio (age bands) | 0.87 | ≥0.90 |
| Equalized odds ratio (ethnicity proxy — postal code) | 0.82 | ≥0.85 |
| Average processing time | 4.2 minutes | ≤10 minutes |
| Underwriter override rate | 8.3% | Monitored (no target) |
| Explanation completeness score | 87% | ≥85% |

**Known Performance Issues (Flagged for Remediation):**
1. **Age band fairness gap**: Applicants aged 60–70 receive disproportionately more "Refer" decisions than actuarial tables justify (demographic parity ratio 0.87, below 0.90 target)
2. **Postal code proxy discrimination**: Equalized odds for ethnicity (proxied via postal code + income) at 0.82 — below the 0.85 threshold. Urban low-income postal codes receive systematically higher risk scores
3. **Explanation quality degrades for complex cases**: When >5 medical conditions are present, SHAP explanations become less coherent (explanation completeness drops to 71%)
4. **EU data gap**: Model has not been validated on a sufficient sample of EU applicants. The 600K reinsurer records represent accepted policies only (survivorship bias)

### Third-Party Components & Supply Chain

| Component | Vendor | Relationship | Risk |
|-----------|--------|:----------:|:----:|
| Medical Information Bureau (MIB) check | MIB Group, Inc. | Data provider | High — critical input |
| Prescription history (Rx) | TELUS Health (Canada) / IMS Health (EU) | Data provider | High — critical input |
| Credit score data | Equifax (Canada) / Schufa (EU) | Data provider | Medium — secondary signal |
| Motor vehicle records | Provincial registries / EU equivalents | Data provider | Low |
| XGBoost / LightGBM | Open source | Library | Medium — supply chain |
| PyTorch | Meta (open source) | Library | Medium — supply chain |
| Cloud infrastructure | AWS (ca-central-1 Canada, eu-central-1 Frankfurt) | IaaS | High — data residency |
| Model monitoring | Arize AI | SaaS | Medium — sends inference data |
| Explainability toolkit | SHAP (open source) | Library | Low |

---

## Known Risks & Issues Register (Pre-Assessment)

These are the issues that Meridian's internal team has already identified but not yet remediated. They represent realistic gaps you would discover during a governance assessment.

### Risk 1: Proxy Discrimination via Postal Code
- **Severity**: High
- **Description**: AURA uses postal code as a feature (mapped to geographic risk zones). In Canada, postal codes correlate with ethnicity and income. In the EU (Germany specifically), Postleitzahl correlates with immigration status. The model may be making decisions that indirectly discriminate based on protected characteristics.
- **Current Mitigation**: Fairness monitoring dashboards exist but no automated intervention
- **Regulatory Exposure**: EU AI Act Article 10(2)(f) — bias examination; Article 9 — risk management; Grundgesetz Article 3 (German constitutional anti-discrimination)

### Risk 2: Training Data Does Not Represent EU Population
- **Severity**: High
- **Description**: 86% of training data is Canadian. The EU data (14%) comes from reinsurance records that only include accepted policies — introducing survivorship bias. The model has not been validated for EU demographic distributions, medical coding standards (ICD-10-GM vs ICD-10-CA), or EU-specific risk factors.
- **Current Mitigation**: None — this is the primary technical blocker for EU deployment
- **Regulatory Exposure**: EU AI Act Article 10(3) — training data shall be relevant, sufficiently representative, and to the best extent possible free of errors and complete

### Risk 3: Insufficient Human Oversight Design for EU Requirements
- **Severity**: Medium-High
- **Description**: AURA auto-accepts 55% of applications with no human review. EU AI Act Article 14 requires that high-risk AI systems are designed to allow effective human oversight. The current design may not meet the "human-in-the-loop" or "human-on-the-loop" requirements for the EU market, particularly for automatic decline decisions.
- **Current Mitigation**: All declines go to senior underwriter. But auto-accepts have only statistical sampling (5% sampled for review)
- **Regulatory Exposure**: EU AI Act Article 14(1)-(4); ISO 42001 Annex A.8 (Human oversight)

### Risk 4: Explanation Quality Insufficient for Applicant-Facing Transparency
- **Severity**: Medium
- **Description**: SHAP-based explanations are generated per decision, but they are technical (feature importance scores). EU AI Act Article 13 requires transparency measures appropriate for users. If an applicant is declined insurance, they have a right to a meaningful explanation. Current explanations would not satisfy a non-technical consumer.
- **Current Mitigation**: Underwriters manually compose explanation letters for declines/refers. Auto-accept applicants receive no explanation.
- **Regulatory Exposure**: EU AI Act Article 13(1), Article 86 (right to explanation); GDPR Article 22 (automated individual decision-making)

### Risk 5: Model Monitoring Does Not Cover Distributional Drift for EU Data
- **Severity**: Medium
- **Description**: Current monitoring (via Arize AI) tracks drift against Canadian baseline distributions. No EU baseline has been established. When AURA is deployed in EU markets, drift detection will not flag distribution shifts because no EU reference distribution exists.
- **Current Mitigation**: None — monitoring baseline is Canada-only
- **Regulatory Exposure**: EU AI Act Article 9(2)(b) — ongoing risk management; Article 72 — post-market monitoring

### Risk 6: Data Residency & Cross-Border Transfer
- **Severity**: Medium
- **Description**: AURA runs on AWS ca-central-1 (Canada) and eu-central-1 (Frankfurt). But model training occurs centrally in Canada using combined CA+EU data. EU applicant data transferred to Canada for training may require GDPR Chapter V safeguards (Adequacy decision exists for Canada under PIPEDA, but limited to commercial activities — insurance may fall under provincial regulation in some provinces).
- **Current Mitigation**: Standard Contractual Clauses (SCCs) in place with AWS. No Transfer Impact Assessment completed for CA training data flows.
- **Regulatory Exposure**: GDPR Articles 44–49; EU AI Act recital consideration on data governance

### Risk 7: Supply Chain Documentation Gaps
- **Severity**: Medium
- **Description**: AURA uses open-source ML libraries (XGBoost, LightGBM, PyTorch) without formal supply chain risk assessment. No Software Bill of Materials (SBOM) exists. Arize AI (model monitoring SaaS) receives inference data including application features — no Data Processing Agreement specifically covers AI-generated inference data.
- **Current Mitigation**: Standard vendor security reviews completed for Arize AI. No SBOM process.
- **Regulatory Exposure**: EU AI Act Article 15(4) — cybersecurity; ISO 42001 Annex A.10 (Third-party and customer relationships)

### Risk 8: No Conformity Assessment Procedure Established
- **Severity**: High
- **Description**: Meridian has never undergone an EU AI Act conformity assessment. No internal audit procedure, no quality management system specific to AI, and no designated person responsible for EU AI Act compliance within the EU entity.
- **Current Mitigation**: External legal counsel (Freshfields) engaged for advisory. Your engagement as AI Governance Consultant is the primary remediation action.
- **Regulatory Exposure**: EU AI Act Articles 16–17 (Provider obligations), Article 43 (Conformity assessment)

---

## Engagement Scope

### Your Role
**External AI Governance Consultant** retained by Meridian Assurance Corporation to lead the conformity assessment and certification readiness programme for AURA.

### Reporting Structure
You report to the **Chief Compliance Officer (Anita Johal)** with a dotted line to the **Chief Risk Officer (Philippe Beaumont)**. You have direct access to the CTO and VP AI & Data Science for technical information requests.

### Engagement Duration
6 months (April 2026 — September 2026)

### Deliverables

| # | Deliverable | Framework | Target Date |
|:-:|-------------|-----------|:-----------:|
| 1 | Initial AI System Inventory & Classification Report | EU AI Act | Month 1 |
| 2 | Data Governance Assessment (Training Data Audit) | EU AI Act Art. 10, ISO 42001 A.4 | Month 1-2 |
| 3 | Fundamental Rights Impact Assessment (FRIA) | EU AI Act Art. 27 | Month 2 |
| 4 | Risk Management System Review & Gap Analysis | EU AI Act Art. 9, NIST GOVERN/MAP | Month 2-3 |
| 5 | Bias & Fairness Audit Report | EU AI Act Art. 10(2)(f), NIST MEASURE | Month 2-3 |
| 6 | Transparency & Explainability Assessment | EU AI Act Art. 13, ISO 42001 A.6 | Month 3 |
| 7 | Human Oversight Design Review | EU AI Act Art. 14, ISO 42001 A.8 | Month 3 |
| 8 | Technical Documentation Package (Annex IV) | EU AI Act Art. 11, Annex IV | Month 3-4 |
| 9 | Logging & Monitoring Adequacy Assessment | EU AI Act Art. 12, 72 | Month 4 |
| 10 | Cybersecurity & Supply Chain Risk Assessment | EU AI Act Art. 15, ISO 42001 A.10 | Month 4 |
| 11 | Cross-Framework Compliance Matrix | All frameworks | Month 4-5 |
| 12 | Remediation Plan with Prioritised Actions | All frameworks | Month 5 |
| 13 | ISO 42001 AIMS Gap Analysis & Certification Readiness Report | ISO 42001 | Month 5-6 |
| 14 | NIST AI RMF Profile (Meridian-specific) | NIST AI RMF | Month 5-6 |
| 15 | Final Conformity Assessment Report | EU AI Act Art. 43 | Month 6 |
| 16 | Board-Ready Executive Summary | All frameworks | Month 6 |

### In GRC Command Centre Terms

Map this engagement to your tool's modules:

| GRC Module | What to Populate |
|------------|-----------------|
| **Engagement** | "Meridian Assurance — AURA Conformity Assessment" |
| **AI System** | AURA v2.4.1, High-Risk, MRDN-AI-001 |
| **Frameworks** | EU AI Act (High-Risk subset), ISO 42001, NIST AI RMF, ISO 23894 |
| **Requirement Assessment** | Assess all applicable requirements against the known risk register |
| **FRIA** | Deliverable #3 — insurance applicants as affected population |
| **Risk Matrix** | Populate with all 8 identified risks + any you discover |
| **Evidence Vault** | Upload: model card, training data documentation, fairness audit results, architecture diagrams, SHAP explanation samples, monitoring dashboards |
| **Tasks** | Create tasks for each deliverable, assign priorities and dates |
| **Cross-Reference Map** | Show how EU AI Act Article 10 maps to ISO 42001 A.4, NIST MAP-2, etc. |
| **Compliance Reports** | Generate per-deliverable and final executive summary |
| **Audit Trail** | Every assessment decision logged — this becomes your "show your work" evidence |

---

## Model Card (Draft — For Your Evidence Vault)

### Model Details
- **Name**: AURA — Automated Underwriting Risk Assessor
- **Version**: 2.4.1 (March 2026)
- **Type**: Weighted ensemble (XGBoost + LightGBM + LSTM)
- **Owner**: Meridian AI Labs
- **Contact**: Dr. Yuki Tanaka, VP AI & Data Science
- **License**: Proprietary (Meridian internal use only)

### Intended Use
- **Primary**: Automated risk assessment for life insurance underwriting
- **Users**: Meridian underwriting teams (human-on-the-loop), applicants (indirect)
- **Out of Scope**: Health insurance, property insurance, investment suitability, any use outside insurance underwriting

### Factors
- **Relevant Factors**: Age, sex, medical history, prescription history, BMI, blood pressure, cholesterol, smoking status, family medical history, occupation risk class, geographic risk zone, coverage amount, product type
- **Evaluation Factors**: Gender, age bands (18-29, 30-39, 40-49, 50-59, 60-69, 70+), geographic region, income quartile

### Metrics
- Overall accuracy: 91.3% (vs senior underwriter consensus)
- Demographic parity (gender): 0.94
- Demographic parity (age bands): 0.87 ⚠️ Below threshold
- Equalized odds (ethnicity proxy): 0.82 ⚠️ Below threshold

### Training Data
- 4.2M records (2010-2024), 86% Canadian, 14% EU (reinsurance)
- Known gap: EU direct-to-consumer data underrepresented
- Synthetic augmentation: 200K CTGAN-generated records for underrepresented demographics

### Ethical Considerations
- Postal code used as feature — proxy discrimination risk
- Historical training data includes pre-2019 decisions that may encode now-prohibited practices
- Auto-decline decisions directly affect access to essential financial services
- Explanation quality degrades for complex multi-condition cases

### Limitations
- Not validated for EU population distributions
- Right-censoring: no mortality outcome data for applications < 5 years old
- Synthetic data may introduce distribution artefacts
- SHAP explanations are post-hoc approximations, not causal

---

## Appendix: Regulatory Classification Analysis

### EU AI Act Classification

**Is AURA a high-risk AI system?**

**Yes — under Article 6(2) in conjunction with Annex III, Area 5(b).**

Annex III, Area 5 covers: *"Access to and enjoyment of essential private services and essential public services and benefits"*

Specifically, 5(b): *"AI systems intended to be used to evaluate the creditworthiness of natural persons or establish their credit score, with the exception of AI systems used for the purpose of detecting financial fraud."*

While this literally references "creditworthiness" and "credit score," Recital 59 of the EU AI Act clarifies that AI systems used in ***insurance*** that determine pricing, access, or terms for natural persons fall within the scope of high-risk classification when they affect access to essential services.

Life insurance is classified as an essential financial service under EU consumer protection directives. AURA directly determines whether individuals can obtain life insurance and at what premium — squarely within the scope.

**Obligations triggered:**
- Article 9: Risk management system
- Article 10: Data and data governance
- Article 11: Technical documentation (Annex IV)
- Article 12: Record-keeping (logging)
- Article 13: Transparency and provision of information to deployers
- Article 14: Human oversight
- Article 15: Accuracy, robustness, and cybersecurity
- Article 16: Provider obligations (Meridian AI Labs as provider)
- Article 17: Quality management system
- Article 26: Deployer obligations (Meridian Europe GmbH as deployer)
- Article 27: Fundamental rights impact assessment (deployer obligation)
- Article 43: Conformity assessment (internal — insurance is not in Annex I)
- Article 72: Post-market monitoring

### ISO/IEC 42001 Scope

Meridian is pursuing certification of its **AI Management System (AIMS)** covering the development, deployment, and operation of AURA. The scope statement:

> *"The AI Management System of Meridian AI Labs governing the development, testing, deployment, monitoring, and retirement of machine learning systems used in insurance underwriting decisions, including the AURA system (MRDN-AI-001), across Canadian and European operations."*

All Annex A controls (A.2 through A.10) are in scope.

### NIST AI RMF Application

OSFI (Canada's federal insurance regulator) has recommended — though not yet mandated — that federally regulated financial institutions align their AI risk practices with the NIST AI RMF. Meridian has adopted this voluntarily for AURA.

All four functions apply: GOVERN, MAP, MEASURE, MANAGE.

---

## How to Use This Dossier

1. **Create the engagement** in your GRC Command Centre: "Meridian Assurance — AURA Conformity Assessment"
2. **Register the AI system**: AURA v2.4.1, High-Risk classification, all details from the system identity table
3. **Select applicable frameworks**: EU AI Act (high-risk), ISO 42001, NIST AI RMF, ISO 23894
4. **Begin requirement assessment**: Walk through each of the 241 seeded requirements, assessing against the information in this dossier
5. **Register risks**: Enter all 8 identified risks into the risk matrix with severity ratings
6. **Create FRIA**: Insurance applicants (natural persons) as the affected population
7. **Upload evidence**: Use the model card, architecture diagram, performance metrics, and data profile as evidence artefacts
8. **Create tasks**: One per deliverable, with realistic dates across the 6-month engagement
9. **Run cross-framework analysis**: Identify where compliance work on one framework satisfies another
10. **Generate reports**: Compliance report, gap analysis, risk report — your portfolio pieces

This gives you a **complete, realistic, end-to-end AI governance engagement** running through your own tooling — the exact kind of demonstration that turns an interview conversation into a job offer.
