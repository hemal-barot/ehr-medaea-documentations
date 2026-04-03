# Medaea EHR — Master Documentation
## `ehr-medaea-documentations`

> **Platform**: Medaea EHR — Autonomous Healthcare Operating System  
> **Version**: Phase 1 — April 2026  
> **Status**: Active Development  
> **Compliance Targets**: HIPAA, ONC 21st Century Cures, CMS Interoperability Rule

---

## Repository Purpose

This is the **central documentation hub** for the Medaea EHR platform. It serves as:

- Single source of truth for all feature design decisions
- Compliance validation reference for HIPAA and ONC auditors
- Progress tracker for development phases
- Architecture documentation for engineers
- Cross-repository linkage guide

---

## Repository Structure

```
ehr-medaea-documentations/
│
├── README.md                           # This file — master index
├── CHANGELOG.md                        # All cross-repo changes
│
├── compliance/
│   ├── hipaa-checklist.md              # HIPAA §164.3xx compliance status
│   ├── onc-certification.md            # ONC Health IT Certification criteria
│   └── data-retention.md              # Data retention and deletion policies
│
├── features/
│   ├── auth.md                         # Authentication & MFA feature spec
│   ├── patient-management.md           # Patient registry feature spec
│   ├── scheduling.md                   # Scheduling & calendar feature spec
│   ├── encounters.md                   # SOAP note encounters feature spec
│   ├── clinical-charting.md            # Allergies, Meds, Problems, Immunizations
│   ├── billing.md                      # Billing & claims (Phase 2 planned)
│   ├── reporting.md                    # Reports & analytics (Phase 2 planned)
│   └── interoperability.md             # FHIR R4 + SMART (Phase 2 planned)
│
├── architecture/
│   ├── overview.md                     # System architecture + tech stack
│   ├── security.md                     # Security architecture + HIPAA controls
│   └── deployment.md                   # Infrastructure + deployment guide
│
├── progress/
│   ├── development-progress.md         # Phase-by-phase progress tracker
│   └── roadmap.md                      # Future phases and milestones
│
└── repos/
    ├── backend.md                       # ehr-medaea-backend repo guide
    ├── frontend.md                      # ehr-medaea-frontend repo guide
    ├── website.md                       # ehr-medaea-website repo guide
    ├── backend-apis.md                  # ehr-medaea-backend-apis repo guide
    └── dbmodel.md                       # ehr-medaea-dbmodel repo guide
```

---

## Quick Links

### By Role

| Audience | Start Here |
|---|---|
| **QA / Tester** | [Testing Guide](../api-docs/docs/testing-guide.md) · [API Reference](../api-docs/docs/api-reference/) |
| **Backend Dev** | [Architecture](./architecture/overview.md) · [API Docs](../api-docs/README.md) |
| **Frontend Dev** | [Feature Specs](./features/) · [ehr-medaea-frontend](./repos/frontend.md) |
| **Product Manager** | [Progress Tracker](./progress/development-progress.md) · [Roadmap](./progress/roadmap.md) |
| **Compliance Officer** | [HIPAA Checklist](./compliance/hipaa-checklist.md) · [ONC Certification](./compliance/onc-certification.md) |
| **DevOps / Infra** | [Deployment Guide](./architecture/deployment.md) |
| **Figma Designer** | [Feature Specs](./features/) — each spec includes UI components list |

---

## GitHub Repositories

| Repo | Purpose | Language | Status |
|---|---|---|---|
| [ehr-medaea-backend](https://github.com/hemal-barot/ehr-medaea-backend) | FastAPI + Django backend | Python | Active |
| [ehr-medaea-frontend](https://github.com/hemal-barot/ehr-medaea-frontend) | React + Vite EHR app | TypeScript | Active |
| [ehr-medaea-website](https://github.com/hemal-barot/ehr-medaea-website) | Marketing website | JavaScript | Complete |
| [ehr-medaea-backend-apis](https://github.com/hemal-barot/ehr-medaea-backend-apis) | API docs + Postman | Markdown + JSON | Active |
| [ehr-medaea-dbmodel](https://github.com/hemal-barot/ehr-medaea-dbmodel) | DB schema + ERD | SQL + Markdown | Active |
| [ehr-medaea-documentations](https://github.com/hemal-barot/ehr-medaea-documentations) | This repo | Markdown | Active |

---

## Platform Summary

```
┌─────────────────────────────────────────────────────────────────────┐
│                    MEDAEA EHR PLATFORM                              │
├──────────────────────────────┬──────────────────────────────────────┤
│  Marketing Website           │  medaea.ai / port 3000              │
│  (React + Vite + Tailwind)   │  ehr-medaea-website repo            │
├──────────────────────────────┼──────────────────────────────────────┤
│  EHR Frontend                │  app.medaea.ai / port 5000          │
│  (React 18 + Vite + TS)      │  ehr-medaea-frontend repo           │
├──────────────────────────────┼──────────────────────────────────────┤
│  FastAPI Backend             │  api.medaea.ai / port 8000          │
│  (Python 3.11)               │  ehr-medaea-backend repo            │
├──────────────────────────────┼──────────────────────────────────────┤
│  Django Admin                │  admin.medaea.ai / port 9000        │
│  (Python 3.11)               │  ehr-medaea-backend repo            │
├──────────────────────────────┼──────────────────────────────────────┤
│  PostgreSQL Database         │  Managed by Replit (dev)            │
│                              │  ehr-medaea-dbmodel repo (schema)   │
└──────────────────────────────┴──────────────────────────────────────┘
```

---

## Phase 1 Feature Summary (Complete)

| Feature | Backend | Frontend | Design | Tests |
|---|---|---|---|---|
| Authentication (JWT) | ✅ | ✅ | ✅ | 🟡 |
| Email Verification | ✅ | ✅ | ✅ | 🟡 |
| MFA (TOTP + SMS) | ✅ | ✅ | ✅ | 🟡 |
| Password Reset | ✅ | ✅ | ✅ | 🟡 |
| User Profile | ✅ | ✅ | ✅ | 🟡 |
| Patient Registry | ✅ | ✅ | ✅ | 🟡 |
| Appointment Scheduling | ✅ | ✅ | ✅ | 🟡 |
| Calendar View | ✅ | ✅ | ✅ | 🟡 |
| SOAP Encounters | ✅ | ✅ | ✅ | 🟡 |
| Allergy List | ✅ | ✅ | ✅ | 🟡 |
| Medication List | ✅ | ✅ | ✅ | 🟡 |
| Problem List | ✅ | ✅ | ✅ | 🟡 |
| Immunization Records | ✅ | ✅ | ✅ | 🟡 |
| Audit Logs | ✅ | ✅ | ✅ | 🟡 |
| Room Management | ✅ | ✅ | ✅ | 🟡 |
| Staff Scheduling | ✅ | ✅ | ✅ | 🟡 |
| On-Call Assignments | ✅ | ✅ | ✅ | 🟡 |
| Marketing Website | ✅ | N/A | ✅ | 🟡 |
| Django Admin | ✅ | N/A | N/A | 🟡 |

✅ Complete | 🟡 In Progress | ❌ Not Started

---

## Phase 2 Planned Features

| Feature | Priority | Compliance Driver |
|---|---|---|
| FHIR R4 API | High | ONC §170.315(g)(10) |
| Billing & Claims (CMS-1500) | High | Revenue |
| Patient Portal | High | ONC §170.315(e)(1) |
| E-Prescribing (EPCS) | High | DEA / State |
| Document Upload/Viewer | Medium | ONC |
| Quality Measures (HEDIS) | Medium | CMS |
| Insurance Eligibility | Medium | Revenue |
| Real-time Notifications | Medium | UX |
| Lab Orders & Results | High | Clinical |
| Referral Management | Medium | Clinical |
