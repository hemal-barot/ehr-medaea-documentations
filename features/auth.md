# Feature Spec — Authentication & MFA
## Medaea EHR | Updated: April 2026

---

## Feature Overview

**Purpose**: Secure provider identity verification for access to PHI.  
**Status**: ✅ Phase 1 Complete  
**HIPAA**: §164.312(a)(1) — Access Control  
**ONC**: §170.315(d)(1) — Authentication + Access Control | §170.315(d)(13) — MFA

---

## User Stories

| Story | Acceptance Criteria |
|---|---|
| As a new provider, I can create an account | Signup form → email sent → login works |
| As a provider, I can log in with email + password | JWT returned; invalid creds show error |
| As a provider, I can enable TOTP MFA | QR code shown; code verified; MFA active on next login |
| As a provider, I can enable SMS MFA | Phone verified; SMS sent on login |
| As a provider with MFA, login requires code | Second factor required after credentials |
| As a provider, I can reset my forgotten password | Email with reset link; link expires in 1h |
| As a provider, I can verify my email address | Link in email; account unlocked |
| As a provider, I can change my password | Current password required; new password validated |

---

## API Endpoints

| Method | Path | Auth | Purpose |
|---|---|---|---|
| POST | /api/v1/auth/signup | None | Create provider account |
| POST | /api/v1/auth/login | None | Get JWT or MFA challenge |
| POST | /api/v1/auth/verify-email | None | Verify email token |
| POST | /api/v1/auth/resend-verification | None | Resend verification email |
| POST | /api/v1/auth/forgot-password | None | Send reset email |
| POST | /api/v1/auth/reset-password | None | Set new password with token |
| POST | /api/v1/auth/mfa/setup | JWT | Initiate TOTP/SMS enrollment |
| POST | /api/v1/auth/mfa/finalize | JWT | Confirm TOTP enrollment |
| POST | /api/v1/auth/mfa/verify | None | Verify MFA code during login |
| GET | /api/v1/users/me | JWT | Get current user profile |
| PUT/PATCH | /api/v1/users/me | JWT | Update profile |
| POST | /api/v1/users/me/password | JWT | Change password |

---

## Database Tables

| Table | Key Fields |
|---|---|
| `users` | email, hashed_password, mfa_enabled, mfa_method, mfa_secret_encrypted, mfa_phone, email_verification_token, password_reset_token, hipaa_consent, last_login_at |

---

## Frontend Components

| Component | Path | Description |
|---|---|---|
| LoginPage | `features/auth/LoginPage.tsx` | Email + password form |
| SignupPage | `features/auth/SignupPage.tsx` | Provider registration |
| VerifyEmailPage | `features/auth/VerifyEmailPage.tsx` | Token verification |
| ForgotPasswordPage | `features/auth/ForgotPasswordPage.tsx` | Email input |
| ResetPasswordPage | `features/auth/ResetPasswordPage.tsx` | New password form |
| MfaSetupPage | `features/auth/MfaSetupPage.tsx` | QR code + method selection |
| MfaVerifyPage | `features/auth/MfaVerifyPage.tsx` | 6-digit OTP input |
| AuthContext | `context/AuthContext.tsx` | Global auth state + token |
| SettingsPage | `features/settings/` | Profile + password + MFA |

---

## Password Requirements

- Minimum 8 characters
- At least 1 uppercase letter
- At least 1 lowercase letter
- At least 1 number
- (Special characters recommended but not enforced — Phase 2)

---

## MFA Methods

| Method | Technology | Setup | Verification |
|---|---|---|---|
| Authenticator App (TOTP) | pyotp (RFC 6238) | QR code scan → verify code | 6-digit code (30s window) |
| SMS | Twilio Verify API | Phone number → SMS | 6-digit code |
| Email OTP | Gmail SMTP | Automatic | 6-digit code in email |

---

## Email Notifications

| Trigger | Template | Content |
|---|---|---|
| Signup | `welcome_email` | Welcome + verification link (if enabled) |
| Email verification | `verification_email` | Token link (24h expiry) |
| Resend verification | `resend_verification_email` | New token link |
| Password reset | `password_reset_email` | Reset link (1h expiry) |
| MFA OTP | `mfa_otp_email` | 6-digit code |

---

## Figma Design Notes

**Key screens to design / validate**:
1. Login page — Work email field, password, remember me, forgot password, create account
2. Signup page — Name, email, password, role dropdown, specialty
3. Verification pending — "Check your email" state with resend option
4. Email verified — Success state, redirect timer to login
5. Forgot password — Email input, always shows success
6. Reset password — New password + confirm, strength indicator
7. MFA setup — Method selection cards (App / SMS / Email)
8. MFA QR — QR code display with manual key, "Enter code" input
9. MFA verify — Clean 6-digit input with timer, "Didn't get it?" link
10. Settings — Security tab with MFA status, password change form

**Design tokens**:
- Primary: `#0d9488` (teal)
- Background: `#f8fafc` (light gray)
- Error: `#ef4444` (red)
- Font: System sans-serif stack
