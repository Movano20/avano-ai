# Operator Onboarding Guide

Avano AI uses an invite-only onboarding flow to ensure every operator is verified before getting dashboard access.

## Flow

```
Admin sends invite → Operator receives link → 5-step onboarding → Pending approval → Admin approves → Full access
```

## Steps

### Step 1 — Welcome
Operator receives invite link: `https://app.avanoai.ai/onboard?token=<token>`  
Token expires after 7 days.

### Step 2 — Business Verification
- Company name is **pre-locked** from the invite — must match trade license exactly
- OCR validates the uploaded trade license against the locked name
- Mismatch = registration blocked (anti-fraud)

### Step 3 — Documents
- Trade license upload (OCR processed)
- Emirates ID of authorized signatory

### Step 4 — Contact Information
- Primary contact name, phone, email
- Office address and emirate

### Step 5 — Plan Selection
Available plans:
- **Founding Member** — AED 299/mo (invite-only, capped at 50 slots)
- **Standard** — AED 499/mo
- **Pro** — AED 4,800/year
- **Enterprise** — Custom pricing

## After Submission
- Dashboard access is **blocked** until admin manually approves
- Operator sees: "Registration received — pending approval"
- Admin receives notification in admin365 dashboard
- On approval: welcome email sent, full dashboard access granted

## Security
- No public self-registration
- Every operator tied to a specific invite with company name locked
- Tenant isolation enforced on every API query
