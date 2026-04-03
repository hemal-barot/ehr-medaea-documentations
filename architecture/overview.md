# System Architecture — Medaea EHR
## Technical Architecture Overview
## Last Updated: April 2026

---

## Architecture Diagram

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                          MEDAEA EHR — SYSTEM ARCHITECTURE                   │
└─────────────────────────────────────────────────────────────────────────────┘

  EXTERNAL USERS
  ─────────────
  
  ┌──────────────────┐    ┌──────────────────────────────────────────────────┐
  │  General Public  │    │                   Providers                      │
  │  (medaea.ai)     │    │  (Doctors, Nurses, Admins, Billing Staff)        │
  └────────┬─────────┘    └──────────────────────┬───────────────────────────┘
           │                                     │
           ▼                                     ▼
  ┌──────────────────┐    ┌──────────────────────────────────────────────────┐
  │  Marketing Site  │    │               EHR Frontend App                   │
  │  React + Vite    │    │         React 18 + Vite + TypeScript              │
  │  Tailwind CSS    │    │              Port 5000 (dev)                      │
  │  Port 3000 (dev) │    │   ehr-medaea-frontend GitHub repo (249 files)     │
  │  ehr-medaea-     │    └────────────────────────┬─────────────────────────┘
  │  website repo    │                             │
  └──────────────────┘                             │  Axios HTTP (proxied)
                                                   │  /api → :8000
                                                   ▼
  ┌──────────────────────────────────────────────────────────────────────────┐
  │                        FastAPI Backend                                    │
  │                   Python 3.11 | Port 8000 (dev)                          │
  │                ehr-medaea-backend GitHub repo (74 files)                  │
  │                                                                           │
  │  ┌────────────────────────────────────────────────────────────────────┐  │
  │  │  Domain Routers                                                     │  │
  │  │  ├── /api/v1/auth        — Signup, Login, MFA, Password Reset      │  │
  │  │  ├── /api/v1/users       — User profile management                 │  │
  │  │  ├── /api/v1/patients    — Patient registry CRUD                   │  │
  │  │  ├── /api/v1/appointments— Appointment scheduling                  │  │
  │  │  ├── /api/v1/calendar    — Calendar, rooms, PTO, on-call           │  │
  │  │  ├── /api/v1/encounters  — SOAP note encounters                    │  │
  │  │  ├── /api/v1/patients/*  — Charting (allergies/meds/problems/imm.) │  │
  │  │  ├── /api/v1/organizations— Organization membership               │  │
  │  │  └── /api/v1/audit      — Audit logs (HIPAA)                      │  │
  │  └────────────────────────────────────────────────────────────────────┘  │
  │                                                                           │
  │  ┌──────────────┐  ┌──────────────┐  ┌────────────────────────────────┐  │
  │  │  SQLAlchemy  │  │  JWT Auth    │  │  Background Services           │  │
  │  │  ORM         │  │  python-jose │  │  Twilio SMS | Gmail SMTP       │  │
  │  │  bcrypt      │  │  pyotp TOTP  │  │  pyotp TOTP verification       │  │
  │  └──────┬───────┘  └──────────────┘  └────────────────────────────────┘  │
  └─────────┼──────────────────────────────────────────────────────────────┘
            │
            ▼
  ┌──────────────────────────────────────────────────────────────────────────┐
  │                          PostgreSQL 15                                    │
  │                      19 tables | UUID PKs | TIMESTAMPTZ                  │
  │                    ehr-medaea-dbmodel repo (schema docs)                  │
  └──────────────────────────────────────────────────────────────────────────┘
  
  ┌──────────────────────────────────────────────────────────────────────────┐
  │                          Django Admin                                     │
  │                    Python 3.11 | Port 9000 (dev)                         │
  │               admin.medaea.ai — Internal operational tools                │
  └──────────────────────────────────────────────────────────────────────────┘
  
  ┌──────────────────────────────────────────────────────────────────────────┐
  │                       External Services (Phase 1)                         │
  │  Twilio (SMS MFA) | Gmail SMTP (email) | pyotp (TOTP authenticator)      │
  └──────────────────────────────────────────────────────────────────────────┘
```

---

## Domain-Driven Design

The FastAPI backend follows **Domain-Driven Design (DDD)** with each clinical domain as an isolated module:

```
backend/fastapi_app/domains/
├── identity/       # Auth, users, MFA, password reset
├── patient/        # Patient registry
├── scheduling/     # Appointments, calendar, rooms, PTO, on-call
├── encounter/      # SOAP note encounters
├── charting/       # Allergies, medications, problems, immunizations
├── organization/   # Organization membership
├── audit/          # Audit log (HIPAA)
└── documents/      # Document management (Phase 2)
```

Each domain has:
- `router.py` — FastAPI router with all endpoints
- `schemas.py` — Pydantic request/response models
- `service.py` — Business logic (where applicable)

---

## Tech Stack

### Frontend (EHR App)

| Technology | Version | Purpose |
|---|---|---|
| React | 18.x | UI framework |
| TypeScript | 5.x | Type safety |
| Vite | 5.x | Build tool + dev server |
| Tailwind CSS | 3.x | Utility-first styling |
| React Router | 6.x | Client-side routing |
| Axios | 1.x | HTTP client |
| FullCalendar | 6.x | Calendar component |
| React Hook Form | 7.x | Form management |
| Zod | 3.x | Schema validation |

### Backend (FastAPI)

| Technology | Version | Purpose |
|---|---|---|
| FastAPI | 0.110+ | API framework |
| Python | 3.11 | Language |
| SQLAlchemy | 2.x | ORM |
| PostgreSQL | 15 | Database |
| bcrypt | 5.x | Password hashing |
| python-jose | 3.x | JWT tokens |
| pyotp | 2.x | TOTP MFA |
| Twilio | 8.x | SMS MFA |
| aiosmtplib | 3.x | Async email (Gmail) |
| Pydantic | 2.x | Data validation |
| uvicorn | 0.29+ | ASGI server |

### Backend (Django Admin)

| Technology | Version | Purpose |
|---|---|---|
| Django | 4.2+ | Admin framework |
| Gunicorn | 21.x | WSGI server |
| psycopg2 | 2.x | PostgreSQL driver |

### Marketing Website

| Technology | Version | Purpose |
|---|---|---|
| React | 18.x | UI framework |
| Vite | 5.x | Build tool |
| Tailwind CSS | 3.x | Styling |
| React Router | 6.x | Routing |
| nginx | 1.25+ | Production serving |

---

## Database Architecture

See [ehr-medaea-dbmodel](https://github.com/hemal-barot/ehr-medaea-dbmodel) for full schema docs.

**Key design decisions**:
1. **UUID primary keys** — No sequential exposure, distributed-safe
2. **TIMESTAMPTZ** — All timestamps in UTC with timezone
3. **Org-scoped data** — Most clinical entities scoped to `organization_id`
4. **Soft deletes** — `is_active` flag on users and organizations (hard delete on patients currently — Phase 2 to change)
5. **JSONB** — For flexible structures: permissions, MFA backup codes
6. **Denormalization** — Patient name on appointments for billing audit trail

---

## Authentication & Authorization Flow

```
Request arrives
    │
    ▼
Extract Bearer token from Authorization header
    │
    ▼
Decode JWT → extract sub (user UUID)
    │
    ├── Invalid / Expired → 401 Unauthorized
    │
    ▼
Load User from DB by UUID
    │
    ├── Not found / Inactive → 401 Unauthorized
    │
    ▼
Role check (if required by endpoint)
    │
    ├── Insufficient role → 403 Forbidden
    │
    ▼
Execute endpoint handler
    │
    ▼
Response
```

**Role hierarchy**:
```
admin > doctor > nurse > staff > receptionist > billing
```

---

## API Design Principles

1. **RESTful** — Standard HTTP methods (GET/POST/PUT/PATCH/DELETE)
2. **Consistent responses** — Pydantic models for all requests/responses
3. **Org-scoped data** — All PHI queries filtered by organization
4. **Pagination** — `skip` + `limit` on all list endpoints
5. **HTTP status codes** — 200/201/204/400/401/403/404/409/422/500
6. **Error format** — `{"detail": "Human-readable message"}`
7. **Security-first** — No sensitive data in URL params or logs

---

## Environments

| Environment | Frontend | Backend | Admin | Website | DB |
|---|---|---|---|---|---|
| Development (Replit) | :5000 | :8000 | :9000 | :3000 | Replit managed |
| Docker (local) | :5000 | :8000 | :9000 | :3000 | postgres container |
| Staging | app-staging.medaea.ai | api-staging.medaea.ai | admin-staging.medaea.ai | staging.medaea.ai | AWS RDS |
| Production | app.medaea.ai | api.medaea.ai | admin.medaea.ai | medaea.ai | AWS RDS Multi-AZ |

---

## Security Architecture

See [security.md](./security.md) for full details.

**Summary of controls**:
- bcrypt password hashing (cost=12)
- JWT with 8-hour TTL
- MFA: TOTP + SMS + Email OTP
- CORS allowlist in production
- HTTPS/TLS 1.2+ in production
- SQLAlchemy ORM (no raw SQL — XSS/injection prevention)
- Pydantic v2 strict validation on all inputs
- Audit log for all PHI access
- Role-based access control
