# Requirements

## 👤 User Roles & Permissions

| Role | Capabilities |
| :--- | :--- |
| **Tenant** | Browse listings, manage favorites, message owners, schedule visits, rate interactions, pay rent. |
| **Owner** | Create/manage listings, approve visits, message tenants, view ratings. |
| **Staff** | Content moderation, user support, visit assistance. |
| **Admin** | System configuration, analytics, ad management, user management. |

## 🚀 Non-Functional Requirements (NFRs)

### Performance
*   **Latency**: API p95 response time < 300ms for common read operations.
*   **Real-time**: WebSocket event delivery < 1s end-to-end.

### Security
*   **Authentication**: JWT (JSON Web Tokens) for stateless auth.
*   **Protection**: Helmet CSP headers, rate limiting, strong password policies.
*   **Access Control**: Role-based middleware on all protected routes.

### Scalability
*   **Statelessness**: REST APIs are stateless to support horizontal scaling.
*   **Database**: PostgreSQL connection pooling and read-replicas supported.

### Reliability
*   **Health Checks**: `/health` endpoint for load balancers.
*   **Monitoring**: Structured logging and error tracking.

### Compliance
*   **Privacy**: PII minimization and encryption in transit (TLS).
