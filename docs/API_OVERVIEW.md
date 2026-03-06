# Avano AI — API Overview

> Full API documentation is available to registered operators upon request.
> Contact: api@avanoai.ai

## Base URL

```
https://api.avanoai.ai
```

All requests require a tenant API key passed as `x-api-key` header.

---

## Core Endpoints

### Fleet

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/fleet` | List all vehicles with current status |
| GET | `/api/fleet/:id` | Get vehicle detail |
| PATCH | `/api/fleet/:id/status` | Update vehicle status |

### Bookings

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/bookings` | List bookings (filterable by status/date) |
| GET | `/api/bookings/:id` | Get booking detail with customer info |
| POST | `/api/bookings` | Create booking manually |
| PATCH | `/api/bookings/:id/status` | Update booking status |

### Customers

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/customers` | List customers with search |
| GET | `/api/customers/:id` | Get customer profile + trust score |

### Conversations

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/conversations/:phone` | Get conversation history |
| POST | `/api/takeover` | Start operator takeover |
| POST | `/api/release` | End operator takeover |
| POST | `/api/send` | Send message as operator |

---

## Webhooks

Avano AI can push real-time events to your systems:

- `booking.created` — New booking created by AI agent
- `booking.confirmed` — Booking status changed to confirmed
- `booking.completed` — Booking completed
- `customer.flagged` — Customer flagged or blacklisted
- `conversation.escalated` — AI requested human handoff

Webhook configuration is available via the operator dashboard.

---

## Rate Limits

| Tier | Requests/min |
|------|-------------|
| Starter | 60 |
| Growth | 300 |
| Enterprise | Unlimited |
