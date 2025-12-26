# Technical Architecture

## 🏗️ System Overview
The system follows a modular microservice-like structure (or modular monolith) to separate concerns between listings, messaging, and core user management.

![System Architecture](../diagrams/system_architecture.png)

## 🗄️ Database Schema
We use PostgreSQL. Key entities include Users, Listings, Visits, Conversations, and Payments.

![Database Schema](../diagrams/database_schema.png)

## 🔄 Module Flows

### Listings Flow
User creates listing -> Admin validates (optional) -> Published to Search.
![Listings Flow](../diagrams/module_flow_listings.png)

### Visit Scheduling
Tenant Request -> Owner Notification -> Owner Action (Approve/Reject) -> Tenant Notification.
![Visits Flow](../diagrams/module_flow_visits.png)

### Messaging
Real-time socket connection handling with fallback to database persistence.
![Messaging Flow](../diagrams/module_flow_messaging.png)
