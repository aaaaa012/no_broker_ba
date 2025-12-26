# Testing & QA

## 🧪 Functional Testing Scope

### Authentication
*   Verify register/login flows (Success/Failure).
*   Correct error messages for invalid passwords.
*   Protected routes reject requests without Valid JWT.

### Listings
*   **Owner/Admin Only**: Create, Update, Delete listings.
*   **Public**: Search, Get Details.

### Visits
*   **Tenant**: Request visit (cannot request on own listing).
*   **Owner**: Approve/Decline handling.

### Messaging
*   Verify WebSocket connection stability.
*   Check offline message persistence (Inbox retrieval).

## 🕷️ Integration & Edge Cases
*   **Rate Limiting**: Trigger 429 after N failed login attempts.
*   **CORS**: Verify requests from unknown origins are blocked.
*   **Uploads**: Reject files larger than 5MB.
*   **Concurrency**: Two owners accepting the same tenant request (should only succeed once, though logic implies 1:1, usually race conditions in payment).

## 📂 Test Data Structure
Examples of CSV imports for seeding:
```csv
# users.csv
id, email, role
1, owner@test.com, owner
2, tenant@test.com, tenant

# listings.csv
id, owner_id, title, rent
100, 1, "Cozy 1BHK", 12000
```
