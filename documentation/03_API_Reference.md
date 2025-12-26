# API Reference

## 🔐 1. Authentication
*   **General**: Uses JWT tokens. Refresh token rotation implemented.

```http
POST /api/auth/register
Content-Type: application/json
{
  "email": "tenant@example.com",
  "password": "SecurePassword123!",
  "role": "tenant"
}
--> 201 Created { "user_id": "...", "token": "..." }

POST /api/auth/login
Content-Type: application/json
{
  "email": "tenant@example.com",
  "password": "SecurePassword123!"
}
--> 200 OK { "user_id": "...", "role": "tenant", "token": "..." }
```

## 🏠 2. Listings

```http
GET /api/listings?city=Kathmandu&minRent=10000
--> 200 OK [ { "listing_id": "1", "title": "2BHK", "rent": 15000, ... } ]

POST /api/listings
Authorization: Bearer <owner_token>
{
  "title": "Sun-facing Flat",
  "description": "24hr water...",
  "address": "Baneshwor",
  "rent": 25000,
  "rooms": 2,
  "photos": ["url1", "url2"]
}
--> 201 Created { "listing_id": "99" }
```

## 📅 3. Visits
Manage property viewings.

```http
POST /api/visits
{ "listing_id": "99", "requested_time": "2023-11-01T10:00:00Z" }
--> 201 Created { "visit_id": "505", "status": "pending" }

PUT /api/visits/505/decision
Authorization: Bearer <owner_token>
{ "decision": "approved", "note": "Call me before coming" }
--> 200 OK { "status": "approved" }
```

## 💬 4. Messaging
Real-time chat via WebSocket + REST history.

**WebSocket Events**: `send_message`, `typing_start`, `typing_stop`

```http
GET /api/messages/conversations
--> 200 OK [ { "conversation_id": "abc", "last_message": "Hello...", "unread": 2 } ]
```

## 🔔 5. Notifications

```http
GET /api/notifications
--> 200 OK [ { "type": "visit_approved", "content": "Owner approved..." } ]
```

## ⭐️ 6. Favorites
```http
POST /api/favorites { "listing_id": "99" }
DELETE /api/favorites/99
```

## 📝 7. Agreements & Payments
```http
POST /api/agreements { "listing_id": "99", "tenant_id": "user_2", "terms": "..." }
POST /api/payments { "agreement_id": "agr_1", "amount": 25000, "method": "esewa" }
```

## 🛡️ 8. Admin
```http
GET /api/admin/users
PUT /api/admin/users/{id}/role { "role": "staff" }
```
