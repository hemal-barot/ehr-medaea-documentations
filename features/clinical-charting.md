# Feature Spec — Clinical Charting
## Allergies | Medications | Problems | Immunizations
## Medaea EHR | Updated: April 2026

---

## Feature Overview

**Purpose**: Maintain the patient's active clinical chart — the longitudinal record of health data.  
**Status**: ✅ Phase 1 Complete  
**HIPAA**: All PHI — logged in audit_logs  
**ONC**: §170.315(a)(6) Problems, §170.315(a)(7) Medications, §170.315(a)(8) Allergies  
**USCDI v3**: Allergies, Medications, Problems/Diagnoses, Immunizations

---

## Charting Modules

### 1. Allergy & Intolerance List

**Purpose**: Track patient allergies and adverse reactions.

| Method | Path | Purpose |
|---|---|---|
| GET | /api/v1/patients/{id}/allergies | List all allergies |
| POST | /api/v1/patients/{id}/allergies | Add new allergy |

**Fields**:
- `allergen` — Name of the allergen (e.g., "Penicillin", "Peanuts")
- `allergen_type` — drug / food / environmental / latex / contrast / other
- `reaction` — Clinical reaction (e.g., "Anaphylaxis", "Urticaria")
- `severity` — mild / moderate / severe / life-threatening
- `status` — active / inactive / entered-in-error
- `onset_date` — Approximate onset (ISO date)
- `snomed_code` — SNOMED CT concept ID (ONC requirement)

**Clinical Validation Rules**:
- Life-threatening allergies must trigger drug interaction warnings (Phase 2)
- Allergy status changes must be audited
- SNOMED code required for interoperability export

---

### 2. Medication List

**Purpose**: Active and historical medication management.

| Method | Path | Purpose |
|---|---|---|
| GET | /api/v1/patients/{id}/medications | List all medications |
| POST | /api/v1/patients/{id}/medications | Add medication |

**Fields**:
- `name` — Drug name (brand or generic)
- `ndc_code` — National Drug Code (11-digit HIPAA standard)
- `rxnorm_code` — RxNorm concept identifier (interoperability)
- `dosage` — e.g., "5mg", "500mg/5mL"
- `frequency` — e.g., "Once daily", "BID", "QHS"
- `route` — Oral / IV / IM / Topical / Inhaled / Sublingual / SQ
- `status` — active / discontinued / on-hold / completed
- `start_date` / `end_date` — ISO dates
- `refills` — Number of refills authorized
- `instructions` — Patient-facing SIG instructions
- `prescribing_provider_id` — FK to users

**Clinical Rules**:
- NDC code lookup integration planned (Phase 2)
- Drug-drug interaction checking planned (Phase 2 — CDS Hooks)
- Discontinued medications preserved for history

---

### 3. Problem List (Diagnosis List)

**Purpose**: Patient's active and historical diagnoses.

| Method | Path | Purpose |
|---|---|---|
| GET | /api/v1/patients/{id}/problems | List all problems |
| POST | /api/v1/patients/{id}/problems | Add problem |

**Fields**:
- `description` — Human-readable diagnosis name
- `icd10_code` — ICD-10-CM code (required for billing)
- `snomed_code` — SNOMED CT concept ID (ONC interoperability)
- `status` — active / resolved / inactive / entered-in-error
- `onset_date` — When condition began
- `resolved_date` — When resolved (null if still active)
- `chronic` — Boolean — flags chronic conditions

**Clinical Rules**:
- ICD-10 code required for billing (CMS-1500, UB-04)
- Chronic conditions flagged for care management workflows
- Resolved problems retained for medical history

---

### 4. Immunization Records

**Purpose**: Complete vaccination history with registry-compatible data.

| Method | Path | Purpose |
|---|---|---|
| GET | /api/v1/patients/{id}/immunizations | List all immunizations |
| POST | /api/v1/patients/{id}/immunizations | Record immunization |

**Fields**:
- `vaccine_name` — Vaccine display name
- `cvx_code` — CDC CVX code (required for IIS reporting)
- `date_administered` — ISO date
- `dose_number` — Dose sequence (1, 2, 3...)
- `lot_number` — Manufacturer lot (VFC tracking, recall alerts)
- `site` — Administration site (Left deltoid, Right arm, etc.)
- `route` — IM / SC / ID / PO / IN
- `administered_by_id` — FK to users (nurse/MA who gave vaccine)
- `vis_published_date` — VIS document date (federally required)

**Clinical Rules**:
- CVX code required for immunization registry (IIS) reporting
- Lot number required for VFC program and recall tracking
- VIS date required by federal law before administration

---

## Database Tables

| Module | Table | Key Codes |
|---|---|---|
| Allergies | `allergies` | SNOMED CT |
| Medications | `medications` | NDC, RxNorm |
| Problems | `problems` | ICD-10-CM, SNOMED CT |
| Immunizations | `immunizations` | CVX (CDC) |

---

## Frontend Components

| Component | Description |
|---|---|
| `PatientChartPage.tsx` | Main chart with tabbed sections |
| `AllergyList.tsx` | Allergy table + add form |
| `MedicationList.tsx` | Medication table + add form |
| `ProblemList.tsx` | Problem list + ICD-10 picker |
| `ImmunizationList.tsx` | Immunization table + form |

---

## Figma Design Notes

**Chart layout** (suggested tabs):
1. Overview — Allergies, active meds, active problems, last encounter
2. Allergies — Table: allergen, type, reaction, severity, status + Add button
3. Medications — Table: drug, dose, frequency, route, status + Add button
4. Problems — Table: description, ICD-10, onset, chronic badge + Add button
5. Immunizations — Table: vaccine, CVX, date, dose#, lot# + Add button
6. Encounters — Timeline of SOAP notes
7. Documents — File list

**Severity badge colors** (allergies):
- `mild` → yellow
- `moderate` → orange
- `severe` → red-600
- `life-threatening` → red-900 + warning icon

**Status badges**:
- `active` → green
- `discontinued`/`resolved` → gray
- `on-hold` → yellow
- `entered-in-error` → strikethrough + red

---

## USCDI v3 Compliance Notes

All four charting modules align with **USCDI v3** required data elements:

| USCDI Data Class | Our Implementation |
|---|---|
| Allergies and Intolerances | `allergies` table with SNOMED, severity, reaction |
| Medications | `medications` table with NDC, RxNorm |
| Problems/Diagnoses | `problems` table with ICD-10, SNOMED |
| Immunizations | `immunizations` table with CVX, lot, VIS date |
