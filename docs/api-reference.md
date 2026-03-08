# Avano AI — API Reference

Base URL: `https://api.avanoai.ai`

## Authentication
All requests require `Authorization: Bearer <token>` and `x-tenant-id: <your-tenant-id>` headers.

## Fleet

### GET /api/fleet/vehicles
Returns all vehicles for the authenticated tenant.

**Response:**
```json
[
  {
    "id": "uuid",
    "plate_number": "Dubai A 12345",
    "make": "Toyota",
    "model": "Camry",
    "year": 2023,
    "category": "sedan",
    "daily_rate": 150,
    "status": "available"
  }
]
```

### POST /api/fleet/vehicles
Create a new vehicle.

## Bookings

### GET /api/bookings
Returns all bookings. Supports `?status=pending|confirmed|active|completed|cancelled`.

### POST /api/bookings
Create a new booking.

**Body:**
```json
{
  "vehicle_id": "uuid",
  "customer_id": "uuid",
  "pickup_date": "2026-03-10",
  "return_date": "2026-03-15",
  "daily_rate": 150,
  "deposit_amount": 500
}
```

### POST /api/bookings/:id/start
Activate a rental. Triggers Hash 1 (contract open event) on the TARS blockchain ledger.

### PUT /api/bookings/:id
Update booking status or charges (Salik, DARB, parking, extras).

## Customers

### GET /api/customers
Returns all customers for the tenant.

### GET /api/customers/:id
Returns customer profile with booking history and blacklist status.

## Compliance

### GET /api/compliance/authority
Returns the RTA authority routing for the tenant's emirate.

### POST /api/compliance
Submit a new TARS compliance form (new rental or closing).

## AI / Live Ops

### GET /tenants/:tenantId/conversation/:phone
Returns conversation history for a customer phone number.

### POST /tenants/:tenantId/takeover
Operator takes over an AI conversation.

### POST /tenants/:tenantId/release
Release conversation back to AI.
