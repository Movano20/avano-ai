# Avano AI — System Architecture

## Overview

Avano AI is a multi-tenant SaaS platform built for car rental and fleet operators in the UAE. The system processes customer communications, automates bookings, enforces compliance, and anchors contracts to the TARS blockchain.

## Infrastructure

```
                        ┌─────────────────────────┐
                        │   avanoai.ai (Azure CDN) │
                        └────────────┬────────────┘
                                     │
              ┌──────────────────────┼──────────────────────┐
              │                      │                      │
    ┌─────────▼────────┐   ┌────────▼────────┐   ┌────────▼────────┐
    │ app.avanoai.ai   │   │ api.avanoai.ai  │   │ admin365        │
    │ Operator Portal  │   │ AI / Live Ops   │   │ Internal Admin  │
    │ (React + Node)   │   │ (Tier 1)        │   │ (React + Node)  │
    └─────────┬────────┘   └────────┬────────┘   └─────────────────┘
              │                      │
    ┌─────────▼────────┐   ┌────────▼────────┐
    │ Tier 2 Ops API   │   │ Telegram Bot    │
    │ Fleet/Bookings/  │   │ WhatsApp Bot    │
    │ Customers/Finance│   │ (Claude AI)     │
    └─────────┬────────┘   └─────────────────┘
              │
    ┌─────────▼────────┐
    │ PostgreSQL DB    │
    │ (Tenant isolated)│
    └──────────────────┘
```

## Services

| Service | Port | Description |
|---------|------|-------------|
| `avano-tier1` | 3001 | AI agent, conversations, takeover |
| `avano-tier2` | 3002 | Ops API: fleet, bookings, customers, compliance |
| `avano-dash` | 8443 | Operator dashboard (React, HTTPS proxy) |
| `avano-bot` | — | Telegram bot (AI-powered) |
| `avano-verify` | 4001 | Insurance contract verification portal |
| Admin API | 3003 | Internal admin panel API |

## AI Layer

- **Model:** Claude Sonnet (Azure AI Foundry)
- **Memory:** Redis (per-tenant conversation history, 20 message limit)
- **Takeover:** Operator can take over any live conversation; AI resumes on release
- **Languages:** Arabic (MSA) + English — auto-detected per customer message

## Compliance Layer

- **TARS Integration:** Hyperledger Fabric via RTA Dubai API
- **Contract Hashing:** SHA-256, dual-hash lifecycle (open + close)
- **Emirate Routing:** Dubai → TARS, Abu Dhabi → DoT Taqa, others → PDF export

## Multi-Tenancy

Every database query is scoped to `tenant_id`. No cross-tenant data access is possible at the query level. Tenant ID is validated on every API request via `x-tenant-id` header.

## Deployment

- **VM:** Azure (Ubuntu, public IP `74.162.120.4`)
- **SSL:** Let's Encrypt via Certbot
- **Process Manager:** PM2 with systemd auto-restart
- **DNS:** Cloudflare (avanoai.ai)

## Multilingual Support
Avano AI supports Arabic, English, Somali, Hindi, and Urdu natively via Whisper STT.

## RTA Integration
Traffic fines are auto-fetched from RTA per vehicle using Playwright-based scraping with Bright Data UAE residential proxy.

## Document Verification
Claude Vision API powers OCR for passports, Emirates IDs, driving licenses, and IDPs with real-time expiry validation.
