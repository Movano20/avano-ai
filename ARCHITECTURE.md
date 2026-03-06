# Avano AI — System Architecture

## Overview

Avano AI is a multi-layer intelligence platform built for mobility fleet operators. The system processes real-time customer interactions, operational data, and compliance requirements through a modular microservices architecture.

```
Customer (WhatsApp / Telegram)
        │
        ▼
┌───────────────────────┐
│  AI Conversation      │  Natural language processing, multilingual support
│  Engine (Tier 1)      │  150+ languages, tool-calling, booking flow
└──────────┬────────────┘
           │
           ▼
┌───────────────────────┐
│  Operations API       │  Booking lifecycle, fleet management,
│  (Tier 2)             │  customer profiles, financial ledger
└──────────┬────────────┘
           │
           ▼
┌───────────────────────┐
│  Compliance Layer     │  RTA/TARS integration, contract generation,
│  (Tier 3)             │  blockchain hashing, audit trails
└──────────┬────────────┘
           │
           ▼
┌───────────────────────┐
│  Operator Dashboard   │  Real-time fleet view, live ops, analytics,
│                       │  operator takeover, customer profiles
└───────────────────────┘
```

## Core Components

### AI Conversation Engine
- Multi-language AI agent (English, Arabic, Hindi, Urdu, Tagalog, and 145+ more)
- Autonomous booking creation via conversational flow
- OCR document processing (Emirates ID, passport, driving license)
- Operator takeover: human agents can intercept any conversation in real-time

### Operations API
- RESTful fleet and booking management
- Real-time vehicle availability and demand signals
- Customer trust scoring and blacklist network
- Multi-tenant architecture (isolated per operator)

### Compliance Layer
- UAE RTA/TARS integration for regulatory reporting
- Automated contract generation (PDF, signed)
- Blockchain contract hashing for tamper-proof records
- Audit trail for all booking state changes

### Operator Dashboard
- Live fleet status with clickable filter controls
- Booking management with contract signing workflow
- Customer profiles with confidence scoring
- Real-time WhatsApp/Telegram chat panel with takeover capability
- Analytics: revenue, utilization, demand patterns

## Data Flow

```
Customer Message → Language Detection → AI Processing → Tool Calls
       ↓
Booking Created → Contract Generated → Customer Notified
       ↓
Operator Dashboard ← Real-time Updates ← Event Stream
       ↓
Compliance Layer → RTA Reporting → Blockchain Hash → Audit Log
```

## Technology Stack

| Layer | Technology |
|-------|-----------|
| AI Engine | Multi-model architecture (model-agnostic) |
| Backend | Node.js, TypeScript |
| Database | PostgreSQL (multi-tenant) |
| Cache / Queues | Redis |
| Messaging | WhatsApp (Baileys), Telegram Bot API |
| Dashboard | React, Vite, TailwindCSS |
| Infrastructure | Azure Cloud |
| Compliance | RTA/TARS API, PDF generation |
