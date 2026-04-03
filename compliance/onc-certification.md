# ONC Health IT Certification — Medaea EHR
## 21st Century Cures Act — ONC Criteria Status
## Last Updated: April 2026 | Phase 1

> Reference: [ONC 21st Century Cures Final Rule](https://www.healthit.gov/curesrule/)
> Certification body: ONC-Authorized Certification Body (ONC-ACB) — planned
> Certification target: ONC Health IT Certification Program (2015 Edition + Cures Update)

---

## ONC Criteria by Category

### Patient Engagement — §170.315(e)

| Criterion | Title | Status | Notes |
|---|---|---|---|
| §170.315(e)(1) | View, Download, Transmit | 🟡 Planned | Patient portal Phase 2 |
| §170.315(e)(2) | Secure Messaging | 🟡 Planned | Phase 2 |
| §170.315(e)(3) | Patient Health Data Retrieval | 🟡 Planned | Phase 2 |

### Clinical Quality Measures — §170.315(c)

| Criterion | Title | Status | Notes |
|---|---|---|---|
| §170.315(c)(1) | CQM Recording — EP/EC | 🟡 Planned | Phase 2 |
| §170.315(c)(2) | CQM Recording — EH/CAH | 🟡 Planned | Phase 2 |
| §170.315(c)(3) | CQM Reporting — EP/EC | 🟡 Planned | Phase 2 |
| §170.315(c)(4) | CQM Filter | 🟡 Planned | Phase 2 |

### Clinical Operations — §170.315(a)

| Criterion | Title | Status | Notes |
|---|---|---|---|
| §170.315(a)(1) | CPOE — Medications | 🟡 Planned | E-Prescribing Phase 2 |
| §170.315(a)(2) | CPOE — Laboratory | 🟡 Planned | Lab Orders Phase 2 |
| §170.315(a)(3) | CPOE — Diagnostic Imaging | 🟡 Planned | Phase 2 |
| §170.315(a)(4) | Drug-Drug, Drug-Allergy Interactions | 🟡 Planned | CDS integration Phase 2 |
| §170.315(a)(5) | Demographics | ✅ **Complete** | Race, ethnicity, language, DOB, gender in Patient model |
| §170.315(a)(6) | Problem List | ✅ **Complete** | ICD-10 + SNOMED in `problems` table |
| §170.315(a)(7) | Medication List | ✅ **Complete** | NDC + RxNorm in `medications` table |
| §170.315(a)(8) | Medication Allergy List | ✅ **Complete** | SNOMED in `allergies` table |
| §170.315(a)(9) | Clinical Notes | ✅ **Complete** | SOAP notes in `encounters` table |
| §170.315(a)(10) | Drug-Drug, Drug-Allergy Alert Acknowledgment | 🟡 Planned | CDS Phase 2 |
| §170.315(a)(11) | Smoking Status | 🟡 Planned | Add to patient model Phase 2 |
| §170.315(a)(12) | Family Health History | 🟡 Planned | Phase 2 |
| §170.315(a)(13) | Patient-Specific Education Resources | 🟡 Planned | Phase 2 |
| §170.315(a)(14) | Implantable Device List | 🟡 Planned | Phase 2 |
| §170.315(a)(15) | Social, Psychological, and Behavioral Data | 🟡 Planned | Phase 2 |

### Care Coordination / Transitions — §170.315(b)

| Criterion | Title | Status | Notes |
|---|---|---|---|
| §170.315(b)(1) | Transitions of Care | 🟡 Planned | CCD/CCDA export Phase 2 |
| §170.315(b)(2) | Clinical Information Reconciliation | 🟡 Planned | Phase 2 |
| §170.315(b)(6) | Data Export | 🟡 Planned | Phase 2 |
| §170.315(b)(7) | Security Tags — Summary of Care | 🟡 Planned | Phase 2 |
| §170.315(b)(9) | Care Plan | 🟡 Planned | Phase 2 |
| §170.315(b)(10) | Electronic Referral Loops — Send | 🟡 Planned | Phase 2 |
| §170.315(b)(11) | Electronic Referral Loops — Receive | 🟡 Planned | Phase 2 |

### Privacy and Security — §170.315(d)

| Criterion | Title | Status | Notes |
|---|---|---|---|
| §170.315(d)(1) | Authentication, Access Control | ✅ **Complete** | JWT, role-based access, MFA |
| §170.315(d)(2) | Auditable Events and Tamper-Resistance | ✅ **Complete** | `audit_logs` table, all PHI access logged |
| §170.315(d)(3) | Audit Report(s) | ✅ **Complete** | GET /audit/logs endpoint |
| §170.315(d)(4) | Amendments | 🟡 Planned | Encounter amendment flow Phase 2 |
| §170.315(d)(5) | Automatic Access Time-out | ✅ **Complete** | JWT 8h expiry + frontend idle timeout |
| §170.315(d)(6) | Emergency Access | 🟡 Planned | Break-the-glass Phase 2 |
| §170.315(d)(7) | End-User Device Encryption | 🟡 Planned | At-rest encryption Phase 2 |
| §170.315(d)(8) | Integrity | ✅ **Complete** | TLS in transit, DB transactions |
| §170.315(d)(9) | Trusted Connection | ✅ **Complete** | HTTPS/TLS in production |
| §170.315(d)(10) | Auditing Actions on Health Information | ✅ **Complete** | `phi_accessed` flag in audit_logs |
| §170.315(d)(11) | Accounting of Disclosures | 🟡 Planned | Phase 2 |
| §170.315(d)(12) | Encrypt Authentication Credentials | ✅ **Complete** | bcrypt + AES for MFA secrets |
| §170.315(d)(13) | Multi-Factor Authentication | ✅ **Complete** | TOTP + SMS via Twilio |

### Improved Interoperability — §170.315(g)

| Criterion | Title | Status | Notes |
|---|---|---|---|
| §170.315(g)(6) | Consolidated CDA Creation | 🟡 Planned | Phase 2 |
| §170.315(g)(7) | Application Access — Patient Selection | 🟡 Planned | FHIR Phase 2 |
| §170.315(g)(8) | Application Access — Data Category Request | 🟡 Planned | FHIR Phase 2 |
| §170.315(g)(9) | Application Access — All Data Request | 🟡 Planned | FHIR Phase 2 |
| §170.315(g)(10) | Standardized API for Patient Access | 🟡 Planned | FHIR R4 + SMART on FHIR Phase 2 |

---

## USCDI v3 — US Core Data for Interoperability

### Currently Implemented

| USCDI Data Class | Data Element | Status | Model Field |
|---|---|---|---|
| Patient Demographics | First Name | ✅ | `patients.first_name` |
| Patient Demographics | Last Name | ✅ | `patients.last_name` |
| Patient Demographics | Date of Birth | ✅ | `patients.date_of_birth` |
| Patient Demographics | Gender | ✅ | `patients.gender` |
| Patient Demographics | Race | ✅ | `patients.race` |
| Patient Demographics | Ethnicity | ✅ | `patients.ethnicity` |
| Patient Demographics | Preferred Language | ✅ | `patients.preferred_language` |
| Patient Demographics | Address | ✅ | `patients.address/city/state/zip` |
| Allergies/Intolerances | Substance | ✅ | `allergies.allergen` |
| Allergies/Intolerances | Reaction | ✅ | `allergies.reaction` |
| Allergies/Intolerances | Severity | ✅ | `allergies.severity` |
| Allergies/Intolerances | SNOMED Code | ✅ | `allergies.snomed_code` |
| Medications | Medication Name | ✅ | `medications.name` |
| Medications | RxNorm Code | ✅ | `medications.rxnorm_code` |
| Medications | NDC Code | ✅ | `medications.ndc_code` |
| Medications | Dosage | ✅ | `medications.dosage` |
| Medications | Route | ✅ | `medications.route` |
| Problems | Problem Description | ✅ | `problems.description` |
| Problems | ICD-10 Code | ✅ | `problems.icd10_code` |
| Problems | SNOMED Code | ✅ | `problems.snomed_code` |
| Immunizations | Vaccine Name | ✅ | `immunizations.vaccine_name` |
| Immunizations | CVX Code | ✅ | `immunizations.cvx_code` |
| Immunizations | Date Administered | ✅ | `immunizations.date_administered` |
| Clinical Notes | Chief Complaint | ✅ | `encounters.chief_complaint` |
| Clinical Notes | SOAP Note | ✅ | `encounters.subjective/objective/assessment/plan` |
| Unique Device Identifier | Implantable Device | 🟡 | Phase 2 |
| Vital Signs | Blood Pressure, HR, etc. | 🟡 | Phase 2 |
| Laboratory | Results | 🟡 | Phase 2 |

---

## ONC Certification Roadmap

### Phase 1 (Complete) — Foundational Criteria
- ✅ §170.315(a)(5) — Demographics
- ✅ §170.315(a)(6) — Problem List
- ✅ §170.315(a)(7) — Medication List
- ✅ §170.315(a)(8) — Medication Allergy List
- ✅ §170.315(a)(9) — Clinical Notes (SOAP)
- ✅ §170.315(d)(1) — Authentication + Access Control
- ✅ §170.315(d)(2) — Auditable Events
- ✅ §170.315(d)(3) — Audit Reports
- ✅ §170.315(d)(5) — Automatic Timeout
- ✅ §170.315(d)(8) — Integrity
- ✅ §170.315(d)(9) — Trusted Connection
- ✅ §170.315(d)(12) — Encrypted Credentials
- ✅ §170.315(d)(13) — Multi-Factor Authentication

### Phase 2 (Planned) — Interoperability + Patient Access
- 🟡 §170.315(g)(10) — FHIR R4 SMART on FHIR API
- 🟡 §170.315(b)(1) — Transitions of Care (CCD export)
- 🟡 §170.315(e)(1) — View, Download, Transmit
- 🟡 §170.315(a)(1) — E-Prescribing (CPOE Medications)

### Phase 3 (Planned) — Full Certification
- QRDA I/III reporting
- HEDIS quality measures
- Clinical Decision Support (CDS Hooks)
- Patient portal with Blue Button 2.0
