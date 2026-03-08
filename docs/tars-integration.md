# TARS Integration — Dubai RTA Compliance

Avano AI integrates with Dubai's **Transport Authority Rental System (TARS)** — built on Hyperledger Fabric — for automated rental contract submission and compliance reporting.

## Overview

Every rental creates two blockchain-anchored events:

| Event | Trigger | What it records |
|-------|---------|-----------------|
| **Hash 1** — Contract Open | Rental activation (key handover) | Vehicle, customer, contract terms, timestamp |
| **Hash 2** — Contract Close | Rental completion (key return) | Return mileage, charges, damage notes, final amount |

Hash 2 includes a cryptographic reference to Hash 1, creating a tamper-proof chain.

## Supported Emirates

| Emirate | Authority | System |
|---------|-----------|--------|
| Dubai | RTA | TARS (Hyperledger) |
| Abu Dhabi | DoT | Taqa |
| Sharjah | SPTT | Manual export |
| Other | Varies | PDF export |

## TARS API Endpoints (Staging)

Base: `https://api.stg.rta.ae/rta/tars`  
Auth: `X-IBM-Client-Id` header

- `POST /async/agencies/{agencyDid}/rentals` — New contract
- `POST /async/agencies/{agencyDid}/rentals/{did}/events/return` — Return event
- `POST /digital-signature/send-email` — E-sign trigger

## Status
- Architecture: ✅ Complete
- Hashing framework: ✅ Built
- TARS credentials: Pending (apply at developer.rta.ae)
- Activation: Pending credentials
