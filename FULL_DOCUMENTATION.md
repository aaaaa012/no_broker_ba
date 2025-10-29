No-Broker Kathmandu – Full Documentation

Table of Contents
- Project Overview
- Functional Requirements
- Non-Functional Requirements
- Technical Architecture
- Use Cases & User Stories
- Test Cases
- Deployment & Setup
- Appendix

Project Overview
Goals and Objectives
- Reduce brokerage friction by connecting tenants and owners directly
- Provide fast search, scheduling, and secure communication
- Enable operational oversight via admin/staff tools

Scope
- Public listing discovery, authentication, tenant-owner messaging, visit scheduling, notifications, ratings, favorites, recommendations, agreements, payments; admin/staff management and reporting

Stakeholders
- Tenants, Owners, Admins, Staff, Finance/Operations, Support

Assumptions
- PostgreSQL is the primary data store
- JWT secures APIs; roles control access (tenant, owner, staff, admin)
- Real-time messaging and notifications via Socket.IO

Functional Requirements
User Roles and Permissions
- Tenant: browse, favorite, message, schedule visits, rate, pay, manage profile
- Owner: create/manage listings, message tenants, manage visits, view ratings
- Staff: support tasks, moderate content, assist visits
- Admin: system configuration, user management, analytics, ads, recommendations oversight

Modules
1) Authentication
- Login, register, refresh, logout
- Role-based access control via middleware
API Examples
```
POST /api/auth/register
{ "email": "t@x.com", "password": "Secret123", "role": "tenant" }
→ 201 { user_id, token }

POST /api/auth/login
{ "email": "t@x.com", "password": "Secret123" }
→ 200 { user_id, role, token }
```

2) Listings
- CRUD listings; search/filter; photo uploads
API Examples
```
GET /api/listings?city=Kathmandu&minRent=10000
→ 200 [ { listing_id, title, rent, photos: [...] }, ... ]

POST /api/listings
Auth: owner/admin
{ title, description, address, rent, rooms, amenities, photos }
→ 201 { listing_id }
```

3) Visits
- Request visit, approve/decline, reschedule, record decisions
API Examples
```
POST /api/visits
{ listing_id, requested_time }
→ 201 { visit_id, status: "pending" }

PUT /api/visits/{visit_id}/decision
Auth: owner
{ decision: "approved" | "declined", note }
→ 200 { visit_id, status }
```

4) Messaging (Real-time)
- Conversations, messages, typing indicators, read receipts
WebSocket Events
```
authenticate { token }
send_message { conversationId, messageText, receiverId, listingId }
typing_start { conversationId, receiverId }
typing_stop { conversationId, receiverId }
mark_read { conversationId, senderId }
```
REST Examples
```
GET /api/messages/conversations
→ 200 [ { conversation_id, participants, last_message, unread_count }, ... ]

GET /api/messages/{conversation_id}
→ 200 [ { message_id, text, sender_id, created_at, read }, ... ]
```

5) Notifications
- Delivery via WebSocket broadcast; list, mark read
API Examples
```
GET /api/notifications
→ 200 [ { notification_id, type, content, read }, ... ]

PUT /api/notifications/{id}/read
→ 200 { success: true }
```

6) Favorites
- Add/remove favorites, list favorites
```
POST /api/favorites { listing_id }
DELETE /api/favorites/{listing_id}
GET /api/favorites
```

7) Ratings
- Rate listings/owners; list ratings
```
POST /api/ratings { listing_id, score, comment }
GET /api/ratings?listing_id=...
```

8) Recommendations
- Personalized listing recommendations
```
GET /api/recommendations
→ 200 [ listing, ... ]
```

9) Agreements & Payments
- Generate agreements; take payments; view history
```
POST /api/agreements { listing_id, tenant_id, terms }
GET /api/agreements/{id}
POST /api/payments { agreement_id, amount, method }
GET /api/payments?agreement_id=...
```

10) Admin & Staff
- User management, content moderation, reports, ads, staff operations
```
GET /api/admin/users
PUT /api/admin/users/{id}/role { role }
GET /api/ads
POST /api/ads { type, budget, start_at, end_at }
```

Non-Functional Requirements
Performance
- API p95 < 300ms for common reads; pagination for list endpoints
- WebSocket events < 1s end-to-end for delivery

Security
- JWT for auth, Helmet CSP, rate limiting, strong password policy
- Role-based middleware on all protected routes
- CORS allowlist via env

Scalability
- Stateless API; horizontal scaling of API and Socket.IO with sticky sessions
- PostgreSQL tuned connection pool, read replicas as needed

Reliability & Monitoring
- Health checks at `/api/health` and `/health`
- Structured request logging, performance metrics, error tracking

Compliance & Privacy
- PII minimization, encryption in transit, retention policy for logs

Technical Architecture
High-Level Architecture
- See `diagrams/system_architecture.mmd`

Database Schema / ERD
- See `diagrams/database_schema.mmd`

Module Logic Flows
- Listings: `diagrams/module_flow_listings.mmd`
- Visits: `diagrams/module_flow_visits.mmd`
- Messaging: `diagrams/module_flow_messaging.mmd`
- Notifications: `diagrams/module_flow_notifications.mmd`

Use Case Diagrams
- Listings: `diagrams/use_case_listings.mmd`
- Visits: `diagrams/use_case_visits.mmd`
- Messaging: `diagrams/use_case_messaging.mmd`

Use Cases & User Stories
Listings
- As a tenant, I want to filter listings by rent and location so that I can find affordable options.
Acceptance Criteria
- Filter params return matching results with pagination; no 5xx with bad input

Visits
- As an owner, I want to approve or decline visit requests so I can manage my time.
Acceptance Criteria
- Decision is persisted; tenant notified in real time and via list

Messaging
- As a tenant, I want instant messaging with owners so I can clarify details quickly.
Acceptance Criteria
- Messages appear in < 1s; typing indicators and read receipts function

Notifications
- As any user, I want to see actionable notifications of events.
Acceptance Criteria
- New notifications are visible within 2s; can be marked read

UAT Scenarios (Samples)
- Tenant registers, logs in, favorites a listing, sends a message, schedules a visit
- Owner creates a listing, receives visit request, approves it, messages tenant
- Admin views users, changes a role, reviews ads

Test Cases
Functional Tests (sample)
- Auth: register/login success and failure; protected route rejects missing/invalid JWT
- Listings: create (owner-only), get, filter, update/delete (owner-only)
- Visits: create (tenant), decision (owner), list by user
- Messaging: conversation list, message list, WebSocket message delivery
- Notifications: list, mark read
- Favorites: add/remove/list
- Ratings: create/list validations
- Recommendations: result presence and shape
- Admin: list users, change role permissions

Integration & Edge Cases
- Rate limiting triggers on excessive auth attempts
- CORS forbids unknown origins
- Large photo uploads rejected over limit
- Concurrent visit decisions handled idempotently

Test Data Examples
```
users.csv: id,email,role
listings.csv: id,owner_id,title,rent
visits.csv: id,listing_id,tenant_id,status
```

Deployment & Setup
System Requirements
- Node 18+, PostgreSQL 13+, modern browser

Installation
- See README quick start; configure environment from `.env.production`

Configuration
- Backend env
  - PORT, JWT_SECRET, CORS_ORIGINS
  - DB_HOST, DB_PORT, DB_NAME, DB_USER, DB_PASSWORD, DB_POOL_MAX/MIN
- Frontend env
  - API_BASE_URL, WS_URL

Deployment
- Build frontend, serve via CDN or static hosting
- Deploy backend behind reverse proxy; enable SSL, sticky sessions for Socket.IO
- Run DB migrations from `database/`

Appendix
Glossary
- Listing: A rental property entry created by an owner
- Visit: A scheduled appointment for viewing a listing
- Conversation: Message thread between two users

References
- `backend/server.js`, `backend/config/database.js`, route files under `backend/routes/`
- `frontend/src/*` for UI flows and Redux slices

Assumptions
- Payment provider integration will use tokenized methods with PCI-compliant provider
- Images stored on local uploads path in dev; object storage in prod


