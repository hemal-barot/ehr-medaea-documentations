# Medaea EHR — Product Roadmap
## Last Updated: April 2026

---

## Vision

Build the most intelligent, autonomous EHR platform in healthcare — automating the operational burden of running a medical practice through AI, enabling providers to focus entirely on patient care.

**Target market**: Independent practices, specialty clinics, multi-location groups, telehealth providers

---

## Milestone Summary

```
Q1-Q2 2026  ██████████████████████  Phase 1 — Foundation (Complete)
Q3 2026     ████████████░░░░░░░░░░  Phase 2 — Interoperability (In Progress)
Q4 2026     ░░░░░░░░░░░░░░░░░░░░░░  Phase 3 — AI + Automation
Q1 2027     ░░░░░░░░░░░░░░░░░░░░░░  Phase 4 — ONC Certification
Q2 2027     ░░░░░░░░░░░░░░░░░░░░░░  Phase 5 — Scale + Enterprise
```

---

## Phase 1 — Foundation (COMPLETE)

**Goal**: Core EHR functionality. A working clinical workflow from patient registration to signed encounter note.

### Delivered
- ✅ Authentication + MFA (TOTP, SMS, Email)
- ✅ Patient registry with USCDI demographics
- ✅ Appointment scheduling + calendar
- ✅ Room management + PTO + on-call
- ✅ SOAP note encounters
- ✅ Allergy list (SNOMED)
- ✅ Medication list (NDC + RxNorm)
- ✅ Problem list (ICD-10 + SNOMED)
- ✅ Immunization records (CVX)
- ✅ Audit logs (HIPAA §164.312(b))
- ✅ Marketing website (mirrors medaea.ai)
- ✅ Django admin portal
- ✅ 3 GitHub repos pushed (backend: 74 files, frontend: 249 files, website: 22 files)
- ✅ PostgreSQL schema — 19 tables

---

## Phase 2 — Interoperability + Revenue (Q3 2026)

**Goal**: ONC-required FHIR API, billing, and patient access features.

### Epic 1 — FHIR R4 API
- FHIR R4 Patient resource
- FHIR R4 Observation (vitals)
- FHIR R4 Condition (problems)
- FHIR R4 MedicationRequest
- FHIR R4 AllergyIntolerance
- FHIR R4 Immunization
- SMART on FHIR authorization
- ONC §170.315(g)(10) compliance

### Epic 2 — E-Prescribing (EPCS)
- Surescripts integration
- DEA-compliant controlled substance prescribing
- Drug-drug interaction alerts
- Drug-allergy interaction alerts
- Formulary checking

### Epic 3 — Billing & Claims
- CMS-1500 claim generation
- Insurance eligibility checking (270/271)
- ERA/EOB remittance posting
- Claim status tracking
- Denial management queue

### Epic 4 — Patient Portal
- Patient registration (self-service)
- View medical records
- View upcoming appointments
- Secure messaging with provider
- ONC §170.315(e)(1) compliance

### Epic 5 — Lab Orders & Results
- Lab order entry (CPOE)
- HL7 lab interface (ORU)
- Results display + trending
- Critical value alerting

---

## Phase 3 — AI + Automation (Q4 2026)

**Goal**: AI-powered clinical assistance and practice automation.

### Epic 1 — AI Clinical Documentation
- Ambient AI documentation (voice-to-SOAP)
- AI-assisted ICD-10 coding suggestion
- AI problem list reconciliation
- Template-based encounter documentation

### Epic 2 — AI Practice Automation
- Automated appointment reminders (SMS/Email)
- AI-powered appointment scheduling optimization
- Automated prior authorization
- Automated eligibility verification

### Epic 3 — Clinical Decision Support
- CDS Hooks integration
- Drug interaction alerts
- Preventive care gap alerts
- Chronic condition management alerts
- Quality measure gap notifications

### Epic 4 — Population Health
- Patient panel management
- Risk stratification
- HEDIS quality measure tracking
- CMS quality reporting (QRDA I/III)

---

## Phase 4 — ONC Certification (Q1 2027)

**Goal**: Full ONC Health IT Certification.

- ONC-ACB certification submission
- 2015 Edition Cures Update compliance
- FHIR R4 + SMART on FHIR certified
- Consolidated CDA (C-CDA) export
- ONC surveillance cooperation

---

## Phase 5 — Scale + Enterprise (Q2 2027)

**Goal**: Enterprise multi-facility support and market expansion.

### Multi-Tenant Architecture
- White-label EHR for health systems
- Multi-facility organization hierarchy
- Regional data residency

### Specialty-Specific Modules
- Mental health (PHQ-9, GAD-7, progress notes)
- OB/GYN (prenatal flowsheets)
- Ophthalmology (visual acuity, exam findings)
- Dermatology (lesion mapping)
- Cardiology (ECG viewer)

### Advanced Analytics
- AI-powered revenue cycle analytics
- Operational efficiency dashboard
- Outcome tracking and benchmarking
- Payer mix analysis

---

## KPIs by Phase

| Metric | Phase 1 | Phase 2 | Phase 3 | Phase 4 |
|---|---|---|---|---|
| API endpoints | 48 | 100+ | 150+ | 200+ |
| DB tables | 19 | 35+ | 45+ | 50+ |
| ONC criteria met | 13/75 | 35/75 | 55/75 | 75/75 |
| HIPAA controls | ~53% | 75% | 90% | 95%+ |
| GitHub repos | 6 | 6 | 6 | 6 |
| Test coverage | 0% | 40% | 70% | 85% |
