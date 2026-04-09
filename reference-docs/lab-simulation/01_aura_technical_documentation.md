# AURA Technical Documentation — EU AI Act Annex IV

> **Document Status**: DRAFT — Prepared by Meridian AI Labs for conformity assessment review
> **Document Owner**: Dr. Yuki Tanaka, VP AI & Data Science
> **Classification**: Confidential — Meridian Internal + Authorised Consultants
> **Last Updated**: March 2026
> **System**: AURA v2.4.1 (MRDN-AI-001)

This document follows the structure required by EU AI Act Article 11 and Annex IV.

---

## 1. General Description of the AI System

### 1(a) Intended Purpose

AURA (Automated Underwriting Risk Assessor) is a machine learning system designed to assess life insurance applications by producing a mortality/morbidity risk score, risk class assignment, premium recommendation, and accept/refer/decline decision. The system supports but does not fully replace human underwriting judgment — all decline decisions and 35% of applications are referred to human underwriters. 55% of applications are auto-accepted based on risk scores within predefined thresholds.

### 1(b) Provider Identity

| Field | Value |
|-------|-------|
| Provider (developer) | Meridian AI Labs, a division of Meridian Assurance Corporation |
| Address | 200 Bay Street, Suite 3400, Toronto, ON M5J 2J2, Canada |
| EU Authorised Representative | Meridian Assurance Europe GmbH, Kurfürstendamm 21, 10719 Berlin |
| Contact | Dr. Yuki Tanaka (ai-governance@meridian-assurance.com) |

### 1(c) Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0.0 | Sep 2023 | Initial model — single XGBoost, Canadian data only |
| 1.5.0 | Mar 2024 | Added LightGBM to ensemble, expanded feature set to 612 features |
| 2.0.0 | Aug 2024 | Added LSTM component for medical history sequences, features → 847 |
| 2.2.0 | Nov 2024 | Integrated SHAP explanation pipeline, added fairness monitoring |
| 2.4.0 | Jan 2025 | Production deployment (Canada), added EU reinsurance training data |
| 2.4.1 | Mar 2026 | Recalibrated risk thresholds, patched SHAP memory leak |

### 1(d) Interaction with Other Systems

AURA interfaces with:
- **Meridian Core Policy Administration System** (receives application data, returns decisions)
- **MIB Group API** (medical information bureau check — input)
- **TELUS Health / IMS Health API** (prescription history — input)
- **Equifax / Schufa API** (credit data — input)
- **Arize AI** (model monitoring — inference data sent for drift/performance tracking)
- **Meridian Data Warehouse** (training data source, reporting destination)
- **Underwriter Dashboard** (human oversight interface — presents decisions for review/override)

### 1(e) Hardware and Software Requirements

**Training Environment:**
- AWS EC2 p4d.24xlarge instances (8× NVIDIA A100 80GB)
- Region: ca-central-1 (training), with SCCs for EU data
- Storage: AWS S3 (encrypted at rest, AES-256)
- Python 3.11, CUDA 12.1, XGBoost 2.0, LightGBM 4.1, PyTorch 2.2

**Inference Environment:**
- AWS ECS Fargate (containerised)
- Region: ca-central-1 (Canada), eu-central-1 (EU — planned)
- Container image: 2.1 GB, includes all model artefacts
- RAM: 16 GB per container, CPU: 4 vCPU
- No GPU required for inference
- Latency SLA: p99 < 2 seconds

---

## 2. Detailed Description of Elements and Development Process

### 2(a) Development Methods and Techniques

**Data collection**: Historical underwriting decisions sourced from Meridian's policy administration system (2015–2024), supplemented by licensed data from the Canadian Life Insurance Association and Munich Re (reinsurance records). Synthetic augmentation via Conditional Tabular GAN (CTGAN) for underrepresented demographic groups.

**Feature engineering**: 127 raw input fields transformed into 847 engineered features through:
- One-hot encoding of categorical variables
- ICD-10 medical code embedding (trained on medical literature corpus)
- Prescription drug class mapping (ATC classification → risk category)
- Temporal feature construction (trend analysis over applicant's medical history timeline)
- Geographic risk zone mapping (postal code → actuarial risk zone)
- Interaction features (e.g., age × smoker × BMI)

**Model architecture**: Weighted ensemble of three components:
1. **XGBoost v2.0** (weight: 0.40) — gradient-boosted trees on tabular features. 1,200 trees, max depth 8, learning rate 0.01
2. **LightGBM v4.1** (weight: 0.35) — gradient-boosted trees on tabular features. 1,000 trees, max depth 7, learning rate 0.015
3. **LSTM neural network** (weight: 0.25) — processes medical history as a temporal sequence. 2 LSTM layers (256 hidden units each), dropout 0.3, trained with Adam optimizer

**Ensemble aggregation**: Weighted average of risk scores from all three components. Weights determined via Bayesian hyperparameter optimization on the validation set.

**Calibration**: Platt scaling applied to ensemble output to produce well-calibrated probability estimates.

### 2(b) Design Specifications

**Decision thresholds** (configurable per product and jurisdiction):

| Decision | Risk Score Range | Action |
|----------|:------:|--------|
| Auto-Accept | 0–450 | Policy issued without human review |
| Refer | 451–750 | Application sent to underwriter with AI recommendation |
| Auto-Decline | 751–1000 | Application declined, senior underwriter review mandatory |

**Business rules overlay**: After ML scoring, deterministic rules are applied:
- Any applicant under 18 → Decline (legal requirement)
- Coverage amount > $5M → Always Refer regardless of score
- Applicant with active fraud flag → Always Refer
- Known pre-existing condition exclusions per product type

### 2(c) System Architecture

See architecture diagram in Section "How AURA Works" of the Corporation Dossier (00_corporation_dossier.md).

### 2(d) Computational Resources

| Phase | Resource | Duration | Cost (approx.) |
|-------|----------|----------|:---:|
| Full retraining | 8× A100 GPUs | ~72 hours | $12,000 USD |
| Monthly monitoring checkpoint | 2× A100 GPUs | ~8 hours | $800 USD |
| Inference (per application) | 4 vCPU, 16 GB RAM | 340ms (median) | $0.002 USD |
| Monthly inference volume | ~45,000 applications | Continuous | $90 USD |

### 2(e) Model Card

See Model Card in Corporation Dossier (00_corporation_dossier.md).

---

## 3. Monitoring, Functioning, and Control

### 3(a) Human Oversight Measures

**Current design (Canadian operations):**

| Decision Type | Human Involvement | Review Rate |
|--------------|:---:|:---:|
| Auto-Accept | Statistical sampling | 5% of auto-accepts reviewed weekly |
| Refer | Mandatory underwriter review | 100% |
| Auto-Decline | Senior underwriter review | 100% |
| Override | Available at all levels | 8.3% override rate |

**Override workflow:**
1. Underwriter views AI decision + explanation on dashboard
2. If disagreeing, underwriter selects "Override" and must provide:
   - Override reason (dropdown: additional_info, model_error, policy_exception, customer_relationship, other)
   - Free-text justification (minimum 50 characters)
3. Override is logged to immutable audit trail
4. Monthly override report generated for VP Underwriting and VP AI

**Gap identified for EU deployment**: Auto-accept rate of 55% with only 5% sampling may not meet Article 14 human oversight requirements. Options under evaluation:
- Increase sampling rate to 15–20%
- Implement "human-on-the-loop" continuous monitoring dashboard
- Add confidence threshold: auto-accept only when confidence > 95% (currently 85%)

### 3(b) Technical Measures for Robustness

- **Input validation**: Schema enforcement on all incoming data. Out-of-range values flagged and imputed with median (logged)
- **Adversarial testing**: Quarterly adversarial input testing (perturbation of key features to test decision stability)
- **Fallback**: If AURA fails or latency exceeds 5s, application falls back to manual underwriting queue
- **Model versioning**: All model artefacts versioned in MLflow with cryptographic hashing
- **Rollback capability**: Previous model version maintained in warm standby, rollback executable in < 5 minutes

### 3(c) Logging

AURA logs the following for every inference:

| Log Field | Retention |
|-----------|:---------:|
| Application ID | 10 years |
| Timestamp (UTC) | 10 years |
| Input feature vector (pseudonymised) | 10 years |
| Raw model scores (per component) | 10 years |
| Ensemble risk score | 10 years |
| Decision (accept/refer/decline) | 10 years |
| SHAP explanation (top 20 features) | 10 years |
| Confidence interval | 10 years |
| Business rules applied | 10 years |
| Human override (if any) | 10 years |
| Model version | 10 years |
| Inference latency | 1 year |

Logs stored in AWS CloudWatch (operational) and AWS S3 (long-term archive, encrypted).

**Gap**: Current logging does not separately track logs in a format that facilitates EU regulatory access per Article 12(2). Log export functionality for national competent authorities has not been implemented.

---

## 4. Risk Management

### 4(a) Risk Management System

Meridian maintains a three-lines-of-defense model:
- **First line**: Meridian AI Labs (development & operations) — responsible for model risk controls
- **Second line**: Chief Risk Officer function — independent model risk oversight, fairness monitoring
- **Third line**: Internal Audit + External Auditor — periodic independent review

**Gap**: The risk management system was designed for Canadian regulatory requirements (OSFI E-23 guideline). It does not yet address EU AI Act Article 9 requirements specifically, including:
- Identification and analysis of known and reasonably foreseeable risks to health, safety, and fundamental rights
- Estimation and evaluation of risks arising from use in accordance with intended purpose and conditions of reasonably foreseeable misuse
- Adoption of suitable risk management measures

### 4(b) Known Risks

See Risk Register in Corporation Dossier (00_corporation_dossier.md) — 8 identified risks.

### 4(c) Residual Risk Communication

Current practice: Residual risks communicated to Meridian's underwriting leadership and CRO via quarterly model risk report.

**Gap**: No mechanism to communicate residual risks to the deployer (Meridian Europe GmbH) in the format required by Article 13 (instructions for use), nor to natural persons affected by decisions (applicants).

---

## 5. Data and Data Governance

### 5(a) Training Data Description

| Attribute | Detail |
|-----------|--------|
| Total records | 4,200,000 |
| Features (raw) | 127 |
| Features (engineered) | 847 |
| Time period | 2010–2024 |
| Geographic scope | Canada (86%), EU — DE/FR/NL (14%) |
| Label | Senior underwriter consensus decision (accept/refer/decline + risk class) |
| Label quality | 3-underwriter consensus panel for 15% holdout; production underwriter decision for remainder |

### 5(b) Data Preparation

1. **Deduplication**: Removed 23,000 duplicate applications (same applicant, same product, within 30 days)
2. **Missing value treatment**: Mean/median imputation for continuous features (<5% missing). Mode imputation for categorical. Features with >30% missing dropped (4 features removed)
3. **Outlier treatment**: Winsorization at 1st/99th percentile for continuous features
4. **PII pseudonymisation**: Names, exact dates of birth, and full addresses replaced with pseudonymous identifiers. Postal code retained (first 3 characters Canada, first 3 digits EU)
5. **Temporal split**: Train on 2010–2022 data, validate on 2023, test on 2024

### 5(c) Data Governance Gaps

- **No Data Protection Impact Assessment (DPIA)** completed for EU training data
- **Data lineage** tracked at dataset level but not at individual record level
- **Consent basis**: Original data collected under insurance contract performance (legitimate purpose). Secondary use for ML training relies on legitimate interest — no specific consent obtained. GDPR Article 6(1)(f) analysis not formally documented
- **Synthetic data governance**: CTGAN-generated records do not have documented validation against protected characteristic distributions
- **Data retention**: Training data retained indefinitely. No retention policy aligned with GDPR storage limitation principle

---

## 6. Conformity Assessment Status

### Current Status: NOT COMPLETE

| Requirement | Status | Notes |
|-------------|:------:|-------|
| Risk management system (Art. 9) | Partial | Exists for Canada (OSFI), gaps for EU-specific requirements |
| Data governance (Art. 10) | Partial | Training data documented; DPIA, consent analysis, EU representativeness gaps |
| Technical documentation (Art. 11) | In Progress | This document — under review |
| Logging (Art. 12) | Partial | Comprehensive logging exists; EU regulatory access format missing |
| Transparency (Art. 13) | Partial | SHAP explanations exist; consumer-facing explanation quality insufficient |
| Human oversight (Art. 14) | Partial | Override exists; auto-accept sampling rate may be insufficient |
| Accuracy, robustness, cybersecurity (Art. 15) | Partial | Performance monitored; EU-specific validation not completed |
| Quality management system (Art. 17) | Not Started | No QMS specific to AI — this is the ISO 42001 gap |
| Provider obligations (Art. 16) | Not Started | Formal designation of provider duties not documented |
| Post-market monitoring (Art. 72) | Partial | Monitoring exists; EU baseline not established |

**Assessment type**: Internal conformity assessment (Article 43(2) — insurance underwriting is not covered by Annex I harmonised legislation requiring third-party assessment)

---

*This document is a living artefact. Updated quarterly or upon any material change to the AURA system.*
